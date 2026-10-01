_Phase 1 of building a three-node home lab: a Raspberry Pi, two retired gaming laptops, and the gap between knowing how to code and knowing how infrastructure works._

---

It's almost 11pm and the Pi-hole admin panel has returned 403 Forbidden for the fourth time. Frustration is real at this point. I've installed a web server, fixed a missing PHP package, hand-written a config file, debugged a duplicate config key, and restarted the service more times than I want to admit. Every guide says Pi-hole runs on lighttpd. lighttpd is running, but the page will not load.

Then I run one command recommended to me by Claude:

```
sudo ss -tlnp | grep pihole 
```

```
LISTEN  0  32   0.0.0.0:53    users:(("pihole-FTL"))
LISTEN  0  200  0.0.0.0:443   users:(("pihole-FTL")) 
```

Pi-hole v6 doesn't use lighttpd. It ships its own web server now, built directly into pihole-FTL, and it had been listening on port 443 the entire time. The battle I spent two hours fighting did not exist.

### What I'm Building

The lab is three nodes. A Raspberry Pi 5 as the always-on control node, and two Acer Nitro 5 gaming laptops I no longer game on, waiting to become Proxmox hypervisors. The end state is a small production environment in my apartment: Kubernetes across both laptops, a CI/CD pipeline, database replication, and the Pi watching all of it with Prometheus and Grafana.

The point isn't the hardware. I work in healthcare data (Python, SQL, Snowflake pipelines) and I'm moving toward cloud and infrastructure work. I passed the AWS Solutions Architect Associate exam in June. A certification proves you can reason about architecture on paper. A home lab proves you can stand one up, break it, and fix it. This series documents that second part, including the mistakes.

Phase 1 was supposed to be simple: give the Pi a permanent address, make it the DNS server for my network, and install monitoring.

### The Foundation Work

Before anything interesting can run, a server needs an identity that doesn't change. My Pi had two: WiFi on one address, ethernet on another, both handed out by the router's DHCP and both subject to change on any reboot. You can't build a lab on addresses that move.

One command showed me the whole picture:

```
ip route 
```

The output revealed the ethernet interface at 192.168.0.65, the WiFi at .66, and the metric values Linux uses to prefer wired over wireless. We locked the ethernet address in as static, set the router as gateway, and pointed DNS at Google temporarily. The Pi was about to become a DNS server itself, and a DNS server that depends on itself before it's stable is a chicken-and-egg problem.

Then Pi-hole, so every machine in the lab gets a real hostname. node-a.lab instead of a memorized IP. This is the same concept as Route 53 private zones or CoreDNS in Kubernetes, scaled down to an apartment.

That's where the trouble started.

### The Wrong Battle

The admin panel wouldn't load. My first discovery was honest work: Apache was squatting on port 80, serving a half-finished WordPress site I'd built months ago. Fine. I stopped Apache and made a note to move it to another port later.

Still nothing. And here's where I made the real mistake: I assumed. Every tutorial, every forum thread, every guide said Pi-hole serves its admin panel through lighttpd. So I installed lighttpd. When it crashed, I installed php-cgi. When it complained about a missing config file, I wrote one by hand. When that file had a duplicate key, I found it and removed it. Each fix was small and satisfying and completely irrelevant.

I've been working with code for eight years. But sockets, ports, systemd services, firewall rules: this is a different world, and in this world I'm a beginner. The embarrassing part isn't that I didn't know Pi-hole v6 had changed its architecture. The embarrassing part is that the answer was in Pi-hole's official documentation the whole time, and I never checked. I followed guides written for v5 and trusted a single source of truth instead of reading the primary one.

Two hours. One ss command to end it.

Two lessons came out of that night, and I've written them on an index card:

**Check the version before assuming how software works.** Pi-hole v5 and v6 are architecturally different programs that share a name. Every error I debugged was real, but it was real for software I didn't need.

**Diversify your sources.** Guides, forums, AI: all of them synthesized the v5 world confidently. The official docs would have ended this in five minutes. Secondary sources are fast. Primary sources are true.

### The Payoff

Once Pi-hole was actually reachable (port 443, self-signed certificate, browser warning and all), the rest of Phase 1 moved fast.

node_exporter went in first: a small agent that reads CPU, memory, disk, and network stats from the Pi and exposes them on port 9100. It runs as its own locked-down system user with /bin/false for a shell, an account that exists purely to own a process and can never be logged into. Least privilege, the same principle from every AWS course, finally implemented with my own hands.

Installing these tools by hand also forced me to learn something I had skipped for eight years: the Linux directory structure. Binaries live in /usr/local/bin. Configuration lives in /etc. Data that grows lives in /var/lib, and logs live in /var/log. This is basic knowledge, and my lack of experience here made the gaps shine crystal clear. But the layout is a map. Now when something breaks, it is easier to know which folders to look in.

![Article content](https://media.licdn.com/dms/image/v2/D5612AQHDpOlz0naOAg/article-inline_image-shrink_1500_2232/B56Z8plX86LAAQ-/0/1783109091556?e=1792627200&v=beta&t=NtTburUGoAtZ5XCfa1L9dUIJBBcdo8MIE6Sr3vp4X0M)

Linux directory structure

Prometheus went in next, scraping those metrics every 15 seconds and storing them in a time-series database, specialized for metrics. Then Grafana on top, turning the database into dashboards, similar to how AWS has QuickSight. This is the work flow now:

```
node_exporter = a weather station measuring temperature
Prometheus    = the record of those readings over time
Grafana       = the app showing you the graphs 
```

  

![Article content](https://media.licdn.com/dms/image/v2/D5612AQESjNPwJFDTUw/article-inline_image-shrink_1500_2232/B56Z8plyQsHIAI-/0/1783109199216?e=1792627200&v=beta&t=bbZJXjKkeTMwjwJesZzwrk55xYKpFLukhGsJGyqflA8)

Grafana monitoring my Raspberrypi

This follows the Unix philosophy: you choose a tool that does one thing and does it well, then compose small tools together instead of reaching for one giant program that does everything poorly. Any piece of this stack can be swapped without touching the others. And this is why this stack runs half the internet's monitoring.

The last piece was Uptime Kuma with Telegram notifications wired in. To test it, I killed node_exporter and waited. Two minutes later my phone buzzed: service down. Started it again: service recovered.

It felt exciting to have assembled a small bot that texts me when something is wrong, like having a personal digital assistant watching over the lab. By far, receiving the text that my systems are back online has been the most rewarding moment of this build.

![Article content](https://media.licdn.com/dms/image/v2/D5612AQG51NFTjOrZfQ/article-inline_image-shrink_1500_2232/B56Z8pl9H7IoAQ-/0/1783109243924?e=1792627200&v=beta&t=bigT-9Iie-xZd7f01KYTNZpXbnGzt-Lb3M0eSWLhFCE)

Monitoring Bot sending me messages

Sitting on my desk is a $80 computer that now texts me when something breaks. At work, I've lived the opposite. A Windows Task Scheduler job fails silently overnight, and the first sign of trouble is a missing report and a morning spent reading scripts line by line, guessing. The difference between those two mornings is exactly what this lab is for.

Grafana also caught something I wasn't aware of: My raspberrypi's SD card was at 57% and climbing. The culprit was systemd's journal, 2.9GB of logs growing uncapped since the day the Pi was flashed, because I never set a cap. One config line and one vacuum command later, the disk dropped to 46% and can never silently fill again. The monitoring paid for itself, even before Phase 1 was even finished.

Discovering this made me realize how much I still don't know about the DevOps and monitoring world. Another challenge in this experiment isn't technical at all: imposter syndrome. I set high expectations for myself, and something as simple as noticing my disk was almost full is enough to humble me and remind me there's still much to learn.

### What's Next

I ordered ethernet cables from Amazon, now it is time for Phase 2. The two Nitro 5s: Proxmox on bare metal, a two-node cluster with the Pi as the brains and the first virtual machines. The monitoring stack is already waiting for them. Two new lines in a Prometheus config file, and both laptops appear on the same dashboard that watches the Pi.

This is week one. The lab is one node, the graphs are live, and I know exactly one more ss flag than I did last week.