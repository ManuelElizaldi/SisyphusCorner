# Installing Proxmox
Platform for running virtual machines and containers. First we need to flash my laptops, for that I downloaded the ISO from the Proxmox website. Similar to how I first downloaded and installed my flavor of Linux: Zorin OS.

We download the ISO to a clean USB drive. 

Not the ARM version, that uses ARM chips, similar to what my Raspberry Pi has. ARM chip use RISC (Reduced Instruction set computer) instruction sets, these are suited for mobile devices and embedded systems. 

Intel chips in contrast use a more complex instruction set CISC, more suited for high performance operations. 

Flashing the iso -> `sha256sum ~/Downloads/proxmox-ve_9.2-1.iso`
sha256sum creates a hash, think of it like a finger print of the contents of the file. Proxmox generates one as well. You use these to compare if you downloaded the right version. 
- checksums are also used by apt when installing software in Linux 

Now it was time to flash the iso, and for this I used a brand new USB bought specially for this purpose since I am running dd. Commonly known as disk destroy. 
- This command copies raw bytes from a source to a destination, with no file-level interpretation.


`sudo dd if=/home/manu/Downloads/proxmox-ve_9.2-1.iso of=/dev/sdb bs=4M status=progress conv=fsync`
pgrep -a dd, even though I set the argument status=progress, I didn't get any progress indicator so I got scared that maybe the process got stuck and I ruined my USB or the iso file. 

So I ran a new command I leanred. I had used grep in the past to pattern match and cut the noise out of terminal outputs, but during the flashing of the USB I learn about pgrep that helps you find running processes, indeed, the disk destroyer command was there:

```
manu  ~  pgrep -a dd  
2 kthreadd  
1812 /usr/libexec/evolution-addressbook-factory  
1547907 /usr/sbin/uuidd --socket-activation  
2285155 dd if=/home/manu/Downloads/proxmox-ve_9.2-1.iso of=/dev/sdb bs=4M status=progress conv=fsync
```

So I just waited until it was done. 

After this I ran `sync` to flush the write buffers. Another new term. A buffer is a place in memory to store data temporarily as it is moved from one place to another. In this case, we are moving data from my Desktop to the USB and the temporary data was the ISO's information. 

The dd command indicated bs=4M, so chucks of 4 mb. 
- 4 mb of ISO bytes from my disk to the USB. 

Using a website like [BalenaEtcher](https://etcher.balena.io/) could have saved me this step. Which is what I did when I first installed Zorin Os, but now, I am learning Linux and I have to get comfortable reaching for the terminal, plus this taught me a small lesson on Buffers and `pgrep`. 

After flashing, we enter the bios boot up window.


![[PXL_20261007_204724021.jpg]]


Enabling AMD-IOMMU and AMD-SVM
![[PXL_20261007_205051525.jpg]]



After the bios winow, we choose to set up, boot up shows Proxmox:
![[PXL_20261007_205201890.jpg]]



Configuring network setting, gateway = router. IP address = the address of this computer

DNS server = Pihole
![[PXL_20261007_205704300.jpg]]


192.168.0.20:8006 -> to set up proxmox, enter here then you have the web ui to set up proxmox 
- I disabled these repos, since I don't have a subscription:
![[Pasted image 20261011140623.png]]

For now, I sshed into the computer via terminal, but this could also be done through the web UI Terminal

nslookup command, it looks up an IP inside the DNS server 

![[Pasted image 20261011140824.png]]

Now that we have this setup, first thing in the to-do list is to create a config setting that allows me to close the laptop lid, and prevent the computer from going to sleep. If it goes to sleep, the server is disconnected. This is mostly due to my aesthetics preferences. I plan on 3D printing a base for my laptops, I can also prevent overheating with the design I have in mind. Cable management here I come! 
- also to prevent overheating 

For this set up we need to make a folder inside the systemd folder. I named it `logind.conf.d`
- Naming convention for this folder -> why the dots? -> `.d` is Linux convention for a folder of config fragments
- systemd reads files from `/etc/systemd/*conf.d/` after the main boot file has been read and overwrites it. 

Then inside this new `logind.conf.d` folder we create a config file: `lid.conf`

These are the contents:
```
[Login]
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```


a new system command I learned to write this lid config file: `systemd-analyze`. At this point, following the set-up tutorial has made the --help command my best friend. I have learned to run this before I run the command to understand what I am about to do. 

`systemd-analyze cat-config systemd/logind.conf | grep -i lid`
- Was used to check confirm the settings I wrote in the lid.config at boot. 

This might deteriorate the battery on this old gaming laptop. Might need to create a script that tracks battery help using node_exporter, or something like that. This is a project for my future self. For now, the laptop works with its lid close. 

# Adding node-a to Prometheus
Remembering, Prometheus scrapes metrics, in time series. Then we can use something called PromQL to query the data then visualize it. 

I have already done this for my Raspberry Pi, so the process was similar, but first we have to confirm the computers' architecture. 

`uname` Gives us system information. The flag -m will give us the machine hardware name:
`x86_64`

This is for my Raspberry Pi:
`aarch64`

So we download -> `wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz`, same version as the Raspberry Pi. 

Check the sha256sum, which matches, extract the files, and before installing I am going to create the isolated/least privilege user who will own this service. 

Also, at this point, I ran `whoami` command to make note of the user I was logged in. I was logged in as root. Which means I don't need to type sudo before any command. It also means I have to be extra careful, I have removed the learning wheels from my bike. If I want something I shouldn't, I could do serious damage to the system. 

Now I create the user: 
```
root@node-a:~# useradd -rs /bin/false node_exporter
root@node-a:~# id node_exporter 
uid=999(node_exporter) gid=990(node_exporter) groups=990(node_exporter)
```

### Writing the node_exporter service file
Inside -> `/etc/systemd/system/node_exporter.service`

Some services only start after the network is ready. Other you wnat to start before the network. 

Service file:
```
root@node-a:/etc/systemd/system# cat node_exporter.service 
[Unit]
Description=Promethus Node Exporter
After=network.target #does not start until network is ready

[Service]
User=node_exporter #runs as this user, not as root
ExecStart=/usr/local/bin/node_exporter # Commands to run
Restart=on-failure # if it crashes, restart the node_exporter service

[Install]
WantedBy=multi-user.target # Starts automatically at normal boot 
```

Also, I moved the executable we extracted from the github repo into the bin (executbales) folder and checked the versionto make sure everything went well:

```
root@node-a:~/node_exporter-1.8.2.linux-amd64# /usr/local/bin/node_exporter --version
node_exporter, version 1.8.2 (branch: HEAD, revision: f1e0e8360aa60b6cb5e5cc1560bed348fc2c1895)
  build user:       root@03d440803209
  build date:       20240714-11:53:45
  go version:       go1.22.5
  platform:         linux/amd64
  tags:             unknown

```

After writing the config file for node_exporter and moving the executable to /usr/local/bin, we then confirm the settings:

`systemd-analyze verify /etc/systemd/system/node_exporter.service`

```
root@node-a:~# systemctl enable --now node_exporter
Created symlink '/etc/systemd/system/multi-user.target.wants/node_exporter.service' → '/etc/systemd/system/node_exporter.service'.
```


If we check port 9100, we can see that metrics are being exposed there. Doing this through the web browser:
![[Pasted image 20261011164020.png]]

![[Pasted image 20261011164036.png]]

## Connecting this to the Raspberry Pi
During phase 1, I wrote a Prometheus config file. As I type these words I have to say how grateful I am of the notes I took. If you are learning or following along this, please I implore you to take diligent notes. Cosnider it a tip for your future self. 

But any ways, I wrote a prometheus config files. Inside it, there's a section for targets. Here, we need to specify our new target to be scraped, node-a.

Our new config file now looks like this:

```
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: "pi"
    static_configs:
      - targets: ["localhost:9100","192.168.0.20:9100"]
```
Running the command: promtool check config /etc/prometheus/prometheus.yml made me realize I was grouping both the Pi and node-a into one job. *Search what would happen here* so I had to restructure my yaml file into:

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: "pi"
    static_configs:
      - targets: ["localhost:9100"] 

  - job_name: "node-a"
    static_configs:
      - targets: ["192.168.0.20:9100"]

```

Now each machine has its own section

```
promtool check config /etc/prometheus/prometheus.yml
Checking /etc/prometheus/prometheus.yml
```


`http://192.168.0.65:9090/targets` Shows our newly added node-a:

![[Pasted image 20261011171150.png]]

Grafana also shows the data for node-a:
![[Pasted image 20261011171448.png]]


### Monitoring is now up in the to-do list 
We need to add node-a to our monitoring services, this includes Uptime Kuma and our bash script were we track if our services are up and then get notified in telegram 

Adding the node-a to my bash script:

```
#!/bin/bash
source /home/manu/scripts/telegram.env

declare -A SERVICES=(
  ["Pi-hole"]="https://192.168.0.65/admin"
  ["Prometheus"]="http://192.168.0.65:9090/-/healthy"
  ["Grafana"]="http://192.168.0.65:3000/api/health"
  ["node_exporter"]="http://192.168.0.65:9100/metrics"
  ["node-a"]="http://192.168.0.20:8006/"
)

MESSAGE="Daily lab status:"$'\n'

for name in "${!SERVICES[@]}"; do
  code=$(curl -skL -o /dev/null -w "%{http_code}" --max-time 10 "${SERVICES[$name]}")
  if [ "$code" = "200" ]; then
    MESSAGE+="OK   ${name} (${code})"$'\n'
  else
    MESSAGE+="FAIL ${name} (${code})"$'\n'
  fi
done

curl -s "https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage" \
  -d chat_id="${TELEGRAM_CHAT_ID}" \
  -d text="${MESSAGE}" > /dev/null

```

Then I ran the bash script from my terminal to ensure the changes worked. 

Then adding this to Uptime Kuma was just a matter of adding a New Monitor pointing to the new IP we registered. Smooth sailing. 

# Node-B
No plan survives real life. I was planning on setting up Node-B, same as I did for Node-A. But when I plugged in the charger, and tried to turn on the laptop, I had no power.

Using my limited computer technician skills I tried to diagnose the issue to no avail. I tried unplugging the battery and relying on the charger's power. Then I tried to reset the RAM. I also removed the CMOS battery, screen and hard drive. Nothing worked. So I am going to pause this part of the build for now. 

Looking online and asking the Home Lab discord server, my best bet would be a Mini PC. Hopefully I can find something cheap on Facebook Marketplace. 

![[Pasted image 20261013111528.png]]


### Pi’s own DNS points at itself
One setting, and it makes the Pi’s name lookups use your lab records

We want to 