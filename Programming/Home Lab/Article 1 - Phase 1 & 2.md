# Notes Take Away from phase 1 and 2
This is for a linkedin and medium article

Even the most basic of knowledge, my lack of experience here made gaps shine crystal clear. Learning about linux directory structure 
![[Pasted image 20260702121216.png]]

# **Prompt 1 — The lighttpd moment:**
You ran `sudo ss -tlnp | grep pihole` and saw pihole-FTL already listening on port 443. Two hours of debugging had just become irrelevant.

This is something that if I had more knowledge of terminal commands I could've solved in a couple of minutes, but since I am a beginner in this world, I had to go through the process of troubleshooting multiple areas. 

For example, I was hosting a small blog website, the first time I tried setting up lighttpd, I got an error saying that there was already someone else using the port, my apache web server. I used the command ``sudo ss -tlnp | grep :80``

I am slowly learning that each command has a -help argument that can help me to determine how to troubleshoot.  

While troubleshooting and then finding out that pihole v6 does not require lighttpd I was a bit embarrassed, even though I have been programming for multiple years, I have to remind myself that I am a beginner in the world of dev ops and infrastructure. I had high expectations of myself, thinking setting up a home lab was going to be easy, but in reality, I have rarely used terminal commands to troubleshoot sockets, ports, etc. This is new terms for me and I should not be upset. I do have a blind spot, I spent many hours troubleshooting config files, installing and reinstalling which all of this could've been easily been solved by looking up the documentation for pihole. From this I also learned that I shouldn't just trust AI or one source. I can read multiple sources from the internet. 

**Prompt 2 — The work anchor:**

Think of a specific moment at CHS — a pipeline failed, a report was wrong, a system was down — and you (or the team) couldn't immediately see _why_. A moment of flying blind.

Write 2-3 rough sentences about that specific day. What broke, and what did not knowing feel like?
- There were times when windows task schedler failed. Snowflake automated tasks also failed, we didn't have the right monitoring tools configured to diagnose the issue so we had to re run everything, spend many hours looking at our scripts. A simple re run worked, but now we had to implement monitoring scripts to know exactly what error caused the issues 
  
  
**Prompt 3 — The connection:**

Now that Grafana is showing you live metrics from your Pi — CPU, memory, disk, every service visible — finish this sentence honestly:

_"The difference between my Pi now and [that situation at work] is..."_

the graphs, the text message when something failed, having the system operational is the reward from the struggle. I do have to be honest, I am not sure if I would've been able to stand this up with out the power of AI. Yes, relying only in AI for the lighttpd was a mistake that cost me time, but at the same time, AI can parse docuemntation and give me syntethized information. I have to work on not only relying on AI, not remove it from my tools, but learn how to balance/diversify 

---

**Draft — LinkedIn Post #1**

I spent two hours debugging a web server my system didn't need.

Setting up Pi-hole on my Raspberry Pi home lab, the admin panel wouldn't load. Every guide said Pi-hole runs on lighttpd. So I installed lighttpd. Fixed a missing php-cgi package. Created config files by hand. Debugged duplicate config keys. Restarted the service six times.

Then I ran one command:

sudo ss -tlnp | grep pihole

Pi-hole v6 doesn't use lighttpd. It ships its own web server, listening on port 443 the entire time. The battle I was fighting didn't even exist.

I've been programming for eight years. Python, SQL, data pipelines. But infrastructure is a different world. Sockets, ports, systemd, firewall rules, CLI commands. I'm a beginner here, and this was the moment that made me accept it.

Two lessons I'm carrying forward:

Check the version before assuming how software works. Pi-hole v5 and v6 have completely different architectures. Every guide I followed was written for v5.

Diversify your sources. I leaned on one source of truth instead of reading the official docs first. The answer was in Pi-hole's documentation the whole time.

The home lab is a three-node build: Raspberry Pi 5 as the control node, two repurposed gaming laptops becoming Proxmox hypervisors. Next phase: Prometheus, Grafana, and monitoring that tells me what broke before I go looking.

More lessons coming soon!

#AWS #CloudComputing #LearningInPublic #HomeLab #DevOps


---
# I Spent Two Hours Debugging a Web Server My System Didn't Need

_Phase 1 of building a three-node home lab: a Raspberry Pi, two retired gaming laptops, and the gap between knowing how to code and knowing how infrastructure works._

---
![[PXL_20260703_195617042.jpg]]

It's almost 11pm and the Pi-hole admin panel has returned 403 Forbidden for the fourth time. Frustration is real at this point. I've installed a web server, fixed a missing PHP package, hand-written a config file, debugged a duplicate config key, and restarted the service more times than I want to admit. Every guide says Pi-hole runs on lighttpd. lighttpd is running, but the page will not load.

Then I run one command recommended to me by Claude:

```bash
sudo ss -tlnp | grep pihole
```

```
LISTEN  0  32   0.0.0.0:53    users:(("pihole-FTL"))
LISTEN  0  200  0.0.0.0:443   users:(("pihole-FTL"))
```

Pi-hole v6 doesn't use lighttpd. It ships its own web server now, built directly into pihole-FTL, and it had been listening on port 443 the entire time. The battle I spent two hours fighting did not exist.

## What I'm Building

The lab is three nodes. A Raspberry Pi 5 as the always-on control node, and two Acer Nitro 5 gaming laptops I no longer game on, waiting to become Proxmox hypervisors. The end state is a small production environment in my apartment: Kubernetes across both laptops, a CI/CD pipeline, database replication, and the Pi watching all of it with Prometheus and Grafana.

The point isn't the hardware. I work in healthcare data (Python, SQL, Snowflake pipelines) and I'm moving toward cloud and infrastructure work. I passed the AWS Solutions Architect Associate exam in June. A certification proves you can reason about architecture on paper. A home lab proves you can stand one up, break it, and fix it. This series documents that second part, including the mistakes.

Phase 1 was supposed to be simple: give the Pi a permanent address, make it the DNS server for my network, and install monitoring.

## The Foundation Work

Before anything interesting can run, a server needs an identity that doesn't change. My Pi had two: WiFi on one address, ethernet on another, both handed out by the router's DHCP and both subject to change on any reboot. You can't build a lab on addresses that move.

One command showed me the whole picture:

```bash
ip route
```

The output revealed the ethernet interface at 192.168.0.65, the WiFi at .66, and the metric values Linux uses to prefer wired over wireless. We locked the ethernet address in as static, set the router as gateway, and pointed DNS at Google temporarily. The Pi was about to become a DNS server itself, and a DNS server that depends on itself before it's stable is a chicken-and-egg problem.

Then Pi-hole, so every machine in the lab gets a real hostname. `node-a.lab` instead of a memorized IP. This is the same concept as Route 53 private zones or CoreDNS in Kubernetes, scaled down to an apartment.

That's where the trouble started.

## The Wrong Battle

The admin panel wouldn't load. My first discovery was honest work: Apache was squatting on port 80, serving a half-finished WordPress site I'd built months ago. Fine. I stopped Apache and made a note to move it to another port later.

Still nothing. And here's where I made the real mistake: I assumed. Every tutorial, every forum thread, every guide said Pi-hole serves its admin panel through lighttpd. So I installed lighttpd. When it crashed, I installed php-cgi. When it complained about a missing config file, I wrote one by hand. When that file had a duplicate key, I found it and removed it. Each fix was small and satisfying and completely irrelevant.

I've been working with code for eight years. But sockets, ports, systemd services, firewall rules: this is a different world, and in this world I'm a beginner. The embarrassing part isn't that I didn't know Pi-hole v6 had changed its architecture. The embarrassing part is that the answer was in Pi-hole's official documentation the whole time, and I never checked. I followed guides written for v5 and trusted a single source of truth instead of reading the primary one.

Two hours. One `ss` command to end it.

Two lessons came out of that night, and I've written them on an index card:

**Check the version before assuming how software works.** Pi-hole v5 and v6 are architecturally different programs that share a name. Every error I debugged was real, but it was real for software I didn't need.

**Diversify your sources.** Guides, forums, AI: all of them synthesized the v5 world confidently. The official docs would have ended this in five minutes. Secondary sources are fast. Primary sources are true.

## The Payoff

Once Pi-hole was actually reachable (port 443, self-signed certificate, browser warning and all), the rest of Phase 1 moved fast.

node_exporter went in first: a small agent that reads CPU, memory, disk, and network stats from the Pi and exposes them on port 9100. It runs as its own locked-down system user with `/bin/false` for a shell, an account that exists purely to own a process and can never be logged into. Least privilege, the same principle from every AWS course, finally implemented with my own hands.

Installing these tools by hand also forced me to learn something I had skipped for eight years: the Linux directory structure. Binaries live in `/usr/local/bin`. Configuration lives in `/etc`. Data that grows lives in `/var/lib`, and logs live in `/var/log`. This is basic knowledge, and my lack of experience here made the gaps shine crystal clear. But the layout is a map. Now when something breaks, it is easier to know which folders to look in.

![[Pasted image 20260703144914.png]]

Prometheus went in next, scraping those metrics every 15 seconds and storing them in a time-series database, specialized for metrics. Then Grafana on top, turning the database into dashboards, similar to how AWS has QuickSight. This is the work flow now:

```
node_exporter = a weather station measuring temperature
Prometheus    = the record of those readings over time
Grafana       = the app showing you the graphs
```

![[Pasted image 20260703143647.png]]
*Grafana monitoring my raspberrypi*

This follows the Unix philosophy: you choose a tool that does one thing and does it well, then compose small tools together instead of reaching for one giant program that does everything poorly. Any piece of this stack can be swapped without touching the others. And this is why this stack runs half the internet's monitoring.

The last piece was Uptime Kuma with Telegram notifications wired in. To test it, I killed node_exporter and waited. Two minutes later my phone buzzed: service down. Started it again: service recovered.

It felt exciting to have assembled a small bot that texts me when something is wrong, like having a personal digital assistant watching over the lab. By far, receiving the text that my systems are back online has been the most rewarding moment of this build.

![[Screenshot_20260703-143329~2.jpg]]

Sitting on my desk is a $80 computer that now texts me when something breaks. At work, I've lived the opposite. A Windows Task Scheduler job fails silently overnight, and the first sign of trouble is a missing report and a morning spent reading scripts line by line, guessing. The difference between those two mornings is exactly what this lab is for.

Grafana also caught something I wasn't looking for: the SD card at 57% and climbing. The culprit was systemd's journal, 2.9GB of logs growing unbounded since the day the Pi was first flashed, because nobody had ever set a cap. One config line and one vacuum command later, the disk dropped to 46% and can never silently fill again. The monitoring paid for itself before Phase 1 was even finished.

Discovering this made me realize how much I still don't know about the DevOps and monitoring world. Another challenge in this experiment isn't technical at all: imposter syndrome. I set high expectations for myself, and something as simple as noticing my disk was almost full is enough to humble me and remind me there's still much to learn.

## What's Next

I ordered ethernet cables from Amazon, now it is time for Phase 2. The two Nitro 5s: Proxmox on bare metal, a two-node cluster with the Pi as the brains and the first virtual machines. The monitoring stack is already waiting for them. Two new lines in a Prometheus config file, and both laptops appear on the same dashboard that watches the Pi.

This is week one. The lab is one node, the graphs are live, and I know exactly one more `ss` flag than I did last week.

---

_This is the first post in a series documenting a three-node home lab build: the architecture decisions, the debugging, and the lessons that only show up when you type the commands yourself._


# Cron Discards the Evidence

_I built a bot that texts me when my homelab is healthy. In the process I  found a backup that had been dead for some seeks_

---

Sunday afternoon, and the plan is small: I want my Raspberry Pi to text me twice a day confirming that everything in my homelab is alive.
- add something like -> I have writen in my previous [blog post](https://www.linkedin.com/pulse/i-spent-two-hours-debugging-web-server-my-system-didnt-elizaldi-yvzdc/) I started setting up a home lab, which uses a monitoring tool to notify me if my systems are online. I found this to be one of the most rewarding parts of phase 1, so I wanted to amplify that. 
- Explain after the amplify thing, that it is truly interesting how two seperate systems (my raspberrypi and my cellphone) are able to communicate through apis 
	
Pi-hole, Prometheus, Grafana, node_exporter. Four services, one message, 8 AM and 8 PM. The kind of project that should take twenty minutes.

The pieces are simple. A bash script loops over each service and curls it, asking for one thing only: the HTTP status code.

```bash
code=$(curl -skL -o /dev/null -w "%{http_code}" --max-time 10 "$url")
```

A 200 means healthy. Anything else gets flagged. The script assembles a summary and hands it to the Telegram bot API, which delivers it to my phone. The bot token lives in its own file with `chmod 600`, readable by my user and nobody else, because a credential typed directly into a script is a credential waiting to leak.

The script worked on the first manual run. My phone buzzed: four services, four OKs. All that remained was scheduling it with cron.

That's where the twenty-minute project ended and the real one began.

## The Job That Wouldn't Fire

I added a test entry to my crontab, set to run every few minutes, and waited. Nothing. Waited more. Nothing.

Cron fails silently by design, so the debugging chain matters. First, does the entry exist? `crontab -l` said yes. Second, is cron actually launching the job? On modern Raspberry Pi OS there is no `/var/log/syslog` anymore; everything flows through the journal:

```bash
journalctl -u cron --since "15 minutes ago"
```

And there it was. Cron was firing my script on schedule. The script was failing, and the reason appeared once I redirected its output to a file:

```
/bin/sh: 1: /home/manu/scripts/daily_status.sh: Permission denied
```

A missing execute bit. One `chmod +x` and the bot came alive. My phone buzzed on the next tick of the clock.

That should have been the end of the story. But the journal had shown me something else.

## The Body in the Logs

Scrolling through the cron entries, one line kept repeating, every five minutes, like a heartbeat:

```
(manu) CMD (/home/manuel/obsidian-sync.sh)
```

My username is `manu`. That path says `manuel`. The directory does not exist.

This was my Obsidian vault backup, a script I wrote months ago to sync my notes to a private GitHub repo. Everything I know is in that vault: my AWS study notes, my homelab runbook, my essay drafts. I wrote the backup after losing notes once already, scheduled it every five minutes, and never thought about it again.

It had been failing every five minutes since the day I wrote it. Thousands of failures. I never knew.

The reason I never knew is the most instructive line in the whole journal:

```
(CRON) info (No MTA installed, discarding output)
```

When a cron job produces output, including error messages, cron's default behavior is to email it to the user. My Pi has no mail server. So on every failure, cron composed its report, found nowhere to send it, and threw it away. The system was trying to tell me. It just had no mouth.

Cron's default failure mode is discarding the evidence.

## What Went on the Index Card

I keep index cards for lessons I don't want to relearn. This session produced three.

**Silent failure is the default state of an unmonitored system.** Not the exception. The default. A scheduled job, a nightly pipeline, a backup script: unless something actively confirms it succeeded, its natural resting state is broken and quiet. I work in healthcare data, and I have lived the enterprise version of this: a Windows Task Scheduler job dies overnight, and the first alert is a person asking where their morning report went.

**If a job matters, capture its output.** The fix costs one line:

```
*/5 * * * * /home/manu/scripts/obsidian-sync.sh >> /var/log/obsidian-sync.log 2>&1
```

The `2>&1` sends errors to the same file as normal output. If I had written this on day one, the very first log entry would have said the path didn't exist.

**A job nobody verifies is a job nobody knows is dead.** I tested my new Telegram bot by scheduling a one-shot run three minutes in the future and watching for the buzz. I never did that for the backup. The difference between those two jobs is the difference between infrastructure and hope.

## The Payoff

The crontab is fixed. The vault syncs. And twice a day now, at 8 AM and 8 PM Central (after discovering my Pi believed it lived in London, but that's its own small story about checking `timedatectl` before trusting any schedule), my phone buzzes with four green lines.

The strange part is what the bot actually did for me. I built it to watch four services. Its first real catch was a fifth thing, a job I had forgotten I owned, dead in plain sight in the logs. Monitoring doesn't just answer the questions you ask. It surfaces the ones you didn't know to ask.

My homelab is one Raspberry Pi and, as of this week, two retired gaming laptops waiting for Proxmox. The lab keeps teaching the same lesson in different costumes: the systems you don't look at are the systems you don't know.

---

_This is the second post in a series documenting a three-node home lab build: the architecture decisions, the debugging, and the lessons that only show up when you type the commands yourself._