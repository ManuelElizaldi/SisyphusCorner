# Cron Discards the Evidence

_I built a bot that texts me when my homelab is healthy. In the process I  found a backup that had been dead for some seeks_

---

Sunday afternoon, and the plan is small: I want my Raspberry Pi to text me twice a day confirming that everything in my homelab is alive.
- add something like -> I have writen in my previous [blog post](https://www.linkedin.com/pulse/i-spent-two-hours-debugging-web-server-my-system-didnt-elizaldi-yvzdc/) I started setting up a home lab, which uses a monitoring tool to notify me if my systems are online. I found this to be one of the most rewarding parts of phase 1, so I wanted to amplify that. 
- Explain after the amplify thing, that it is truly interesting how two separate systems (my raspberrypi and my cellphone) are able to communicate through apis 
	
Pi-hole, Prometheus, Grafana, node_exporter. Four services, one message, 8 AM and 8 PM. The kind of project that should take twenty minutes.

The pieces are simple. A bash script loops over each service and curls it, asking for one thing only: the HTTP status code.

```bash
code=$(curl -skL -o /dev/null -w "%{http_code}" --max-time 10 "$url")
```

A 200 means healthy. Anything else gets flagged. The script assembles a summary and hands it to the Telegram bot API, which delivers it to my phone. The bot token lives in its own file with `chmod 600`, readable by my user and nobody else, because a credential typed directly into a script is a credential waiting to leak.
- make a note about the L argument, while building the script, pihole kept giving me a 304 code, meaning it was being redirected. That's why I added that L, which was new knowledge for me. 

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

*Add something here with the hyperlink [obsidian back up system](https://www.linkedin.com/pulse/my-pi-lost-connection-i-notes-heres-what-built-manuel-elizaldi-bwopc/). I use obsidian for my blog writing, note taking, and system organization. It is a solid tool if you are working in one computer. But this is not my case, I set up a network ssd to be shared through SMB, then all of my systems had access to the obsidian notes living in that ssd. The problem is that I depend on a good internet connection. If it goes down, the read/writre operations can glitch, losing precious progress on my notes. So I designed a system that creates a backup in github every 5 minutes, if you want to learn more, check the blog post.*
- this addition does not need to be too long, only briefly explain the system I built for the backups. 

My username is `manu`. That path says `manuel`. The directory does not exist.
- Add something about a simple typo being a humbling experience, it doesn't matter how good you become at programming and building systems, if you are not paying attention to what you are doing, if you are not writing conciously, a simple automating (as in turning of your brain) typing of your name can screw up the most sophisticated systems. 

This was my Obsidian vault backup, a script I wrote months ago to sync my notes to a private GitHub repo. Everything I know is in that vault: my AWS study notes, my homelab runbook, my essay drafts. I wrote the backup after losing notes once already, scheduled it every five minutes, and never thought about it again.
- Add something like: Here I was blindly trusting my system, another lesson. Always QA everything. Since I was also manually pushing my notes to github, I blindly trusted the back up system, without probeprly testing the cron job, I only tested the bash script. QA every part of the system!!! 

It had been failing every five minutes since the day I wrote it. Thousands of failures. I never knew.

The reason I never knew is the most instructive line in the whole journal:

```
(CRON) info (No MTA installed, discarding output)
```

When a cron job produces output, including error messages, cron's default behavior is to email it to the user. My Pi has no mail server. So on every failure, cron composed its report, found nowhere to send it, and threw it away. The system was trying to tell me. It just had no mouth.
- Add something like -> perhaps this MTA server is another to do project I can build. It is funny how one project shows you the path to another project and so on. 

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

The strange part is what the bot actually did for me. I built it to watch four services. Its first real catch was a fifth thing, a job I had forgotten I owned *add: and that I was blindly trusting* , dead in plain sight in the logs. Monitoring doesn't just answer the questions you ask. It surfaces the ones you didn't know to ask.

My homelab is one Raspberry Pi and, as of this week, two retired gaming laptops waiting for Proxmox. The lab keeps teaching the same lesson in different costumes: the systems you don't look at are the systems you don't know.

---

_This is the second post in a series documenting a three-node home lab build: the architecture decisions, the debugging, and the lessons that only show up when you type the commands yourself._