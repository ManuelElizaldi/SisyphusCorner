
_I built a bot that texts me when my homelab is healthy. In the process I found a backup that had been dead for weeks._

---

Sunday afternoon, and the plan is small: I want my Raspberry Pi to text me twice a day confirming that everything in my homelab is alive.

In my [previous post](https://www.linkedin.com/pulse/i-spent-two-hours-debugging-web-server-my-system-didnt-elizaldi-yvzdc/) I wrote about setting up the control node of my home lab, including the monitoring stack that notifies me when something breaks. Receiving those notifications turned out to be the most rewarding part of Phase 1, so I wanted to amplify it. There is also something genuinely fascinating in the mechanics: two unrelated systems, a Raspberry Pi on my desk and the phone in my pocket, holding a conversation through APIs.

Pi-hole, Prometheus, Grafana, node_exporter. Four services, one message, 8 AM and 8 PM. The kind of project that should take twenty minutes.

The pieces are simple. A bash script loops over each service and curls it, asking for one thing only: the HTTP status code.

```bash
code=$(curl -skL -o /dev/null -w "%{http_code}" --max-time 10 "$url")
```

A 200 means healthy. Anything else gets flagged. The script assembles a summary and hands it to the Telegram bot API, which delivers it to my phone. The bot token lives in its own file with `chmod 600`, readable by my user and nobody else, because a credential typed directly into a script is a credential waiting to leak.

The `-L` flag in that curl line is new knowledge, paid for with confusion. While building the script, Pi-hole kept answering my health check with a 308 instead of a 200. A 308 is a redirect: the server saying "what you want lives at a different address." Browsers chase redirects silently, which is why you never see them. curl does not; it reports exactly what the server said and stops. The `-L` flag tells curl to follow the redirect and return the status code of the final destination.

The script worked on the first manual run. My phone buzzed: four services, four OKs. All that remained was scheduling it with cron.

That's where the twenty-minute project ended and the real one began.

## The Job That Wouldn't Fire

I added a test entry to my crontab, set to run every few minutes, and waited. Nothing. Waited more. Nothing.

Cron fails silently by design, so the debugging chain matters. First, does the entry exist? `crontab -l` said: yes. Second, is cron actually launching the job? On modern Raspberry Pi OS there is no `/var/log/syslog` anymore, everything flows through the journal:

```bash
journalctl -u cron --since "15 minutes ago"
```

And there it was. Cron was firing my script on schedule. The script was failing, and the reason appeared once I redirected its output to a file:

```
/bin/sh: 1: /home/manu/scripts/daily_status.sh: Permission denied
```

A missing execute bit. One `chmod +x` command, making the file executable and the bot came alive. My phone buzzed on the next tick of the clock.

That should have been the end of the story. But the journal had shown me something else.

## The Body in the Logs

Scrolling through the cron journal log, one line kept repeating, every five minutes, like a heartbeat:

```
(manu) CMD (/home/manuel/obsidian-sync.sh)
```

That script is my Obsidian vault backup. I use Obsidian for everything: blog drafts, note taking, system organization. It is a solid tool if you work from one computer, but I don't, so my vault lives on a network SSD shared over [SMB](https://www.samba.org/samba/docs/), reachable from every machine I own, which live in a shared [Tailscale VPN mesh](https://tailscale.com/docs). The catch is that this system depends on a stable connection. If the network glitches mid-write, notes can be lost, and I learned that the painful way. So I [built a system](https://www.linkedin.com/pulse/my-pi-lost-connection-i-notes-heres-what-built-manuel-elizaldi-bwopc/) that commits the vault to a private GitHub repo every five minutes.

My username is `manu`. That path says `manuel`. The directory does not exist.

A typo. Of my own name. It doesn't matter how many years you have been programming or how sophisticated the system you designed: if you are not writing consciously, autopilot will take the whole thing down. The most careful backup architecture in the world does not survive a keyboard on autopilot.

The job had been running every five minutes, failing every five minutes, since the day I scheduled it. Weeks of failures. I never knew.

And here is the part that stings. I was blindly trusting it. I tested the bash script by hand, watched it push to GitHub once, and called the system done. The cron job, the layer actually responsible for running it forever, I never tested. I QA'd the code and skipped the system. They are not the same thing.

The reason I never knew is the most instructive line in the whole journal:

```
(CRON) info (No MTA installed, discarding output)
```

When a cron job produces output, including error messages, cron's default behavior is to email it to the user. My Pi has no mail server. So on every failure, cron composed its report, found nowhere to send it, and threw it away. The system was trying to tell me. It just had no mouth.

Maybe that mail server is the next small project. It's funny how one project keeps revealing the path to the next: the bot exposed the dead backup, the dead backup exposed the missing MTA. The to-do list writes itself.

Cron's default failure mode is discarding the evidence.

## What Went on the Index Card

I keep index cards for lessons I don't want to relearn. This session produced three.

**Silent failure is the default state of an unmonitored system.** Not the exception. The default. A scheduled job, a nightly pipeline, a backup script: unless something actively confirms it succeeded, its natural resting state is broken and quiet. I work in healthcare data, and I have lived the enterprise version of this: a Windows Task Scheduler job dies overnight, and the first alert is a person asking where their morning report went.

**If a job matters, capture its output.** The fix costs one line:

```
*/5 * * * * /home/manu/scripts/obsidian-sync.sh >> /var/log/obsidian-sync.log 2>&1
```

The `2>&1` sends errors to the same file as normal output. If I had written this on day one, the very first log entry would have said the path didn't exist.

**QA the whole system, not just the code.** I tested my new Telegram bot by scheduling a one-shot run three minutes in the future and watching for the buzz. The backup never got that treatment: I verified the script and skipped the schedule, and the schedule is where it died. A job nobody verifies is a job nobody knows is dead. Test every layer, especially the one that runs when you are not watching. The difference between those two jobs is the difference between infrastructure and hope.

## The Payoff

The crontab is fixed. The vault syncs. And twice a day now, at 8 AM and 8 PM Central (after discovering my Pi believed it lived in London, but that's its own small story about checking `timedatectl` before trusting any schedule), my phone buzzes with four green lines.

The strange part is what the bot actually did for me. I built it to watch four services. Its first real catch was a fifth thing, a job I had forgotten I owned and had been blindly trusting, dead in plain sight in the logs. Monitoring doesn't just answer the questions you ask. It surfaces the ones you didn't know to ask.

My homelab is one Raspberry Pi and, as of this week, two retired gaming laptops waiting for Proxmox. The lab keeps teaching the same lesson in different costumes: the systems you don't look at are the systems you don't know.

---

_This is the second post in a series documenting a three-node home lab build: the architecture decisions, the debugging, and the lessons that only show up when you type the commands yourself._