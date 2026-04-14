## Phase 1 — Raspberry Pi Control Node

| Task                                   | Status    |
| -------------------------------------- | --------- |
| Static IP on ethernet (`192.168.0.65`) | ✅ Done    |
| Pi-hole DNS running                    | ✅ Done    |
| Local DNS records added                | ✅ Done    |
| UFW firewall configured                | ✅ Done    |
| Router pointing at Pi-hole             | ✅ Done    |
| **node_exporter** (metrics agent)      | ⏳ Next    |
| **Prometheus** (metrics collector)     | ⏳ Up next |
| **Grafana** (dashboards)               | ⏳ Up next |
| **Alertmanager** (notifications)       | ⏳ Up next |
| **Uptime Kuma** (service monitoring)   | ⏳ Up next |
| **Ansible** (automation control)       | ⏳ Up next |
# Key Terms
**Time Series Database:** A database designed for data that changes over time. Instead of storing "CPU is 45%" once, it stores "CPU was 45% at 17:00:00, 43% at 17:00:15, 47% at 17:00:30..." — thousands of timestamped snapshots. Regular databases like MySQL aren't efficient at this. Prometheus's TSDB is purpose-built for it.

# Prometheus + Grafana Install

## Checking Pi Architecture

command: `uname -m` = aarch64 = means 64-bit ARM
The architecture determines what we install
`wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-arm64.tar.gz`


Then we extract the files we donwloaded:
`tar xvf node_expoerter-1.8.2.linux-arm64.tar.gz`

tar xvf - unpacks a copmpress archive
- x - extract
- v - verbose (shows each file as it's extract)
- f - specifies the filename to extract 
![[Pasted image 20260328115757.png]]
![[Pasted image 20260328120230.png]]

## node_exporter
Installing node_exporter -> the agent that collects system metrics. CPU, memory, disk, network from the Pi and exposes them to prometheus. 

We installed it for our dedicated system version: aarch64 -> command `uname -m`
- Raspberry pi processor architecture 

using wget download them and then extract the folders. 

copied the extracted files to the binaries folder - with sudo

## Creating a user for node exporter
Least privilege principle. We don't want the root user running node exporter. We want a dedicated user for this task.

`sudo useradd -rs /bin/false node_exporter`
- useradd - creates a new user
- -r creates a system user (no home directory, not a real login account)
	- types of users ???
- -s /bin/false -> when users log in, Linux launches their shell. When we set the /bin/false it does not launch the shell, but exit immediately. 
	- I learned that depending on the /bin/ location you set, thats the shell that is launched when you log in:
		- /bin/bash -> bash, most common. 
		- /bin/zsh/ -> common on macs

If this user ever gets compromised, the hacker will not be able to do anything since no shell is launched and it gets exit after login in. 

you can also do `/bin/nologin` and it prints a message saying "this account is not available".

*System users* -> are created purely to own processes. They are not meant for human use. Every major service on linux runs as its own system user:
- www-data -> owns apache
- sshd -> owns the ssh daemon
- mariadbd -> owns the mariadb
- node_exporter -> will own the metrics agent

you can test this idea running -> `sudo ss -tlnp`: you will see each process owned by different system users

I had an idea of this from AWS courses but had never done it through linux. 

We verify that this user was created successfully with: 
`id node_exporter`


```
manu@manupi:~ $ id node_exporter 
uid=995(node_exporter) gid=990(node_exporter) groups=990(node_exporter)
```

uid -> user id
gid -> group ip (every user belongs to a group)
groups -> all groups the user belongs to

### Types of Linux users
![[Pasted image 20260405104817.png]]


## System Service File
This will tell linux to run node_exporter automatically as background service on every boot. 

We store this new file in /etc/ -> This Linux folder contains system wide configuration files used to control the system's behavior
- For example, running services on boot. 

### System Units
We are creating the file in /etc/systemd/system/node_exporter.service 
- We name it node_exporter.service because it tells Linux this is a service unit file. 

The systemd manages different types of units:
- services
- timers
- sockets
- mounts 

The systemd uses the file extension to know which type of system unit. 

Then the node_exporter is just naming convention, you name files based on what they run. 
- We are going to use commands like: `sudo systemctl start node_exporter`, `sudo systemctl stop node_exporter`
So we need the file name to be intuitive. 

### Learning Nano 
KeysAction`Ctrl+O` then `Enter`Save the file`Ctrl+X`Exit`Ctrl+X` → `Y` → `Enter`Save and exit`Ctrl+K`Cut entire line`Ctrl+U`Paste line`Ctrl+W`Search`Ctrl+G`Help

## Service File
```shell
# location -> /etc/systemd/system/node_exporter.service
[Unit]
Description=Prometheus Node Exporter
After=network.target # don't start until network is ready 

[Service]
User=node_exporter # run as this user, not root 
ExecStart=/usr/local/bin/node_exporter # commands to run 
Restart=on-failure # if it crashes, restart

[Install]
WantedBy=multi-user.target # start automatically at normal boot
```

ExecStarts -> points to the binary where the executable program lives. 
- Basically like a desktop shortcut 

After -> This tells system to not run this until network interfaces are configured. Other common examples of this:
```
After=network.target        # wait for network
After=postgresql.service    # wait for database
After=docker.service        # wait for docker
```

```
[Install]
WantedBy=multi-user.target
```
- This means, when the system reaches normal operating state, start this service automatically. 
- This only will take effect after we run `sudo systemctl enable node_exporter`

### Reloading systemd & enabling the node_exporter service
After we wrote the service file for node_exporter, we need to restart.

manu@manupi:~ $ sudo systemctl enable --now node_exporter
Created symlink /etc/systemd/system/multi-user.target.wants/node_exporter.service → /etc/systemd/system/node_exporter.service

## Opening port 9100 in UFW
We do this so prometheus can scrape it later for metrics.

If we run `curl http://localhost:9100/metrics | head -20` we can see the metrics right now

|Task|Status|
|---|---|
|Downloaded node_exporter (ARM64)|✅|
|Installed to `/usr/local/bin/`|✅|
|Created dedicated system user|✅|
|Created systemd service file|✅|
|Service running and enabled on boot|✅|
|Metrics exposed on port 9100|✅|
|Port 9100 open in UFW|✅|

node_exporter          Prometheus            Grafana
─────────────          ──────────            ───────
Collects metrics  →    Stores metrics   →    Visualizes metrics
from the OS            as time series         as dashboards
(the agent)            (the database)         (the UI)


node_exporter -> grabs metrics from CPU, memory, disk, network, etc. and exposes them at :9100/metrics 

Prometheus -> scrapes node_exporter every 15 minutes and stores data as a time series database, and lets you query it with a language called PromQL. 

Grafana -> Connects to Prometheus, queries it and and visualizes the results

### Unix Philosophy
Each tool does one thing well. These are interchangeable pieces of software. 

# Prometheus install
````bash
wget https://github.com/prometheus/prometheus/releases/download/v2.51.0/prometheus-2.51.0.linux-arm64.tar.gz
````

> - `/etc/prometheus` — stores Prometheus config files
> - `/var/lib/prometheus` — stores the time series database (all the metrics data)
> - `prometheus` — the main binary
> - `promtool` — a helper tool for validating config files
> - `consoles` + `console_libraries` — built-in web UI templates

Extracted files then moved them to their corresponding folder 

We also create a configuration file for prometheus. This file tells prometheus what to scrape. 

Notice that it is pointed to the port we opened - 9100

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: "pi"
    static_configs:
      - targets: ["localhost:9100"]
```

Prometheus wakes up
      ↓
visits localhost:9100/metrics
      ↓
downloads all metrics from node_exporter
      ↓
stores them in /var/lib/prometheus with a timestamp
      ↓
goes back to sleep for 15 seconds


After we create the yaml file we run: `promtool check config /etc/prometheus/prometheus.yml` to ensure it as set up properly

## Creating the Prometheus service unit
same principle as the node_explorer 

Directory -> /etc/systemd/system/prometheus.service

full service file for prometheus:
```shell
manu@manupi:~ $ cat /etc/systemd/system/prometheus.service
[Unit]
Description=Prometheus
After=network.target

[Service]
User=prometheus
ExecStart=/usr/local/bin/prometheus \
  --config.file=/etc/prometheus/prometheus.yml \
  --storage.tsdb.path=/var/lib/prometheus \
  --storage.tsdb.retention.time=15d \
  --web.listen-address=0.0.0.0:9090
Restart=on-failure

[Install]
WantedBy=multi-user.target

```

config -> yaml we wrote
storage -> where prometheus stores its time series database on disk. Every metric scraped form every target gets written here. 
- TSDB -> stands for time series database 
storage -> retention time -> how long we are going to keep the data for. For a Raspberry pi 15 days is a good number, but for production you might want to bump up the number
- You can also ship old data to object storage (S3) using a tool called Thanos 

web -> set the listen address to all networks (0.0.0.0) in the network interface. This way prometheus is reachable from your laptop, nitro 5s and any device on the network via por 9090
- port 9090 is prometheus default - memorize it
