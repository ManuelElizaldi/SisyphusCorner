October 24, 2026

_Browsing YouTube I discovered a critical PHP bug that affected my own home server. Fixing the bug was the easy part, the challenge was finding out why my website had quietly stopped patching itself._

---

Friday, 4:46 in the afternoon. With the work week over and the weather in Austin, Texas finally improving I was ready for the weekend. So I decided to relax and opened YouTube. Browsing for something to watch I was bombarded by the algorithm with many alarming videos about the most recent AI cybersecurity extravaganza. I watched one titled [PHP situation is insane](https://www.youtube.com/watch?v=QRABrn606LE) by one of my favorite coding influencers [Low Level](https://www.youtube.com/watch?v=QRABrn606LE). 

Being a beginner Homelabber/DevOps enthusiast who recently set up a website using PHP I panicked. I had visions of all my personal information being leaked. So I had to act quickly.  

Prompted by Claude, I checked my Apache access log and I read Someone sent a POST request to the front page of [manuel-elizaldi.com](https://manuel-elizaldi.com/), my Word Press website. 

Seconds later that same visitor started asking for a file called phpinfo.php inside /wp-admin/, in /staging/, in /beta/, /qa/, /webmail/, /htdocs/, this visitor was checking every nook and cranny on my digital workshop.

About twenty doors knocked in under five seconds, every one answered with a 404 (praise the Lord), but I still felt exposed.

This is a weird way to meet a stranger, for sure. 


Last week, a pair of PHP vulnerabilities nicknamed PHP2Shell (CVE-2026-109618 and CVE-2026-109619) went public with a 9.2 severity score. Both lets an attacker run their own code on a server. According to some news I read the necessary patches shipped on October 21, and reports said exploitations started even before the patches did. 

My current set up is this: The website runs on WordPress, WordPress runs on PHP, and PHP runs on my Raspberry Pi 5 behind a Cloudflare Tunnel. What feels like protection, in reality isn't, at least for this new crafty PHP2Shell assault. The tunnel hands every request straight to Apache. So the tunnel acts like a hallway, not a wall.

Before I continue with this blog post, I need to give a disclaimer: my site is not an enterprise or production system. It's a personal digital workshop with one admin account, no customer data, no payment forms and no on-call rotation. Also, I am not a security expert and I have barely entered into this field. This is a home lab story. Companies running real infrastructure have patch management, security teams and change windows for this kind of week. I have a Pi, my own volition and a Friday afternoon.

### Patches Were Installed But Not Running

First security item on the to-do list: Check the PHP version I was running?

```
php -v
PHP 8.2.33 (cli)
```

The verdict? I was vulnerable, as expected. What I didn't expect came from asking the web server instead of my Raspberry Pi terminal. `php -v` asks my terminal what it uses. But the website was using a different copy, loaded inside Apache, and the only way to ask that one is through a web request.

So I dropped a one-line PHP file into my website, loaded it through Apache, and then deleted it immediately:

```
<?php echo PHP_VERSION;
```

8.2.32.

Sudo apt had installed 8.2.33 back in August and Apache had been up since August 18. It loads PHP into memory once when it starts up. Apache had never noticed the updated files. A patch sat on the drive for two months, unused, like the spinach you buy at the grocery store, promising yourself you would eat it this time around. 

Second item on the security to-do list: Fixing this absurd discrepancy and further occurrences of this. 

```
sudo apt update && sudo apt upgrade -y && sudo systemctl restart apache2
```

After the command ran I then asked the website again and got a glorious 8.2.35.

Other packages that were updated were: MariaDB, OpenSSL, the kernel and cloudflared came along for the ride, and a reboot later the Pi was on the new kernel.

### Checking for Footprints

Patching closed the door, but it didn't tell me if someone was already dancing and snooping in my files. Exploitation was reported before disclosure, so I went looking for footprints using the power of Claude Code running next to me. I'm a beginner at this, and a second pair of eyes that knows every wp-cli flag by heart makes a huge difference. Also, this was a critical/sensitive situation. 

WordPress publishes checksums for its core files, and wp-cli compares them:

```
wp core verify-checksums
Success: WordPress installation verifies against checksums.
```

Now, the third check in my security to-do list: Check if there are any changes to my files or new malicious files. 

- No PHP files hiding in the upload folder, the common place to drop a malicious file. 

- No files in the web root had changed since October 17. 

- Only one user account: mine. 

- Finally, nothing running as the web server user that shouldn't be.

Fourth item to check: WordPress plugins. I had read online before the PHP2Shell problem that Word Press plugins had always been prone to attacks since they are created by other users.

I have always been a bit nervous about using them, but my limited coding experience in this area leaves me no choice but to trust the creators. 

So going in to check the checksums for these programs, I found out that four of them failed. My intuition was right, I knew it, I shouldn't have trusted the plugins. My stomach dropped. Again I saw visions of hackers in possession of my social security number and stealing my identity. 

Taking a closer looker I noticed that the mismatches were a license file, a couple of icons (png files), an extra readme. Tampering doesn't usually look like a changed SVG. After updating, all eleven plugins verified clean. The mismatch was age, not an intruder, what a way to scare myself. 

Next up, the updates, where the real story was hiding.

### The Patches That Never Came

WordPress was on 6.8.3. eight releases ahead of me. The latest release in that branch was 6.8.11. 

Nine plugins were behind too (those dreaded plugins!). WordPress installs minor security releases automatically, but that was the whole reason I never worried about it. So why hadn't it?

```
wp cron event list
```

wp-cli labels any job whose scheduled time has already passed as "now". A healthy list counts down: 11 minutes, an hour.

Every scheduled event read "now". Not "in 5 minutes". Now. Version checks, plugin update checks, Everything was overdue. I was more vulnerable than what I expected. WordPress's scheduler, WP-Cron, wasn't running anything. Why? 

`wp cron test` had the answer:

```
Error: WP-Cron spawn failed ... sslv3 alert handshake failure
```

The chain took a while to untangle and if I am honest, without Claude helping me out on this one, I estimate my troubleshooting time would have taken me more time than it did. 

From my research I found out that WP-Cron doesn't run on a real clock. When I receive a vis visits the site, WordPress fires an HTTP request at itself, at https://manuel-elizaldi.com/wp-cron.php, to start its jobs in the background, and for that self-call it turns off certificate checking. My Pi didn't have PHP's curl extension, so WordPress fell back to a plainer socket connection. With verification off, that fallback also stops sending SNI, the part of the TLS handshake where the client says which website it wants. Cloudflare serves an enormous number of sites from the same IP addresses. A handshake that doesn't name a site gets rejected.

So every page view sent a request out to Cloudflare and back, every one got turned away, and nothing complained. Security updates included.

The fix:

```
sudo apt install php8.2-curl
```

After the reboot:

```
wp cron test
Success: WP-Cron spawning is working as expected.
```

This should sound familiar. In my last post, a backup cron job failed every five minutes for weeks because of a typo, and cron threw the error away because my Pi had no mail server. Different scheduler, same species of failure: something I trusted to run by itself had stopped, and the system had nowhere to say so.

### Locking the Rest of the House

With the urgent part done, I went down the list.

**The login page.** /wp-login.php was open to the whole internet. xmlrpc.php was already blocked, and the log showed bots hitting that wall with 403s all day. I added a Cloudflare WAF custom rule that puts a Managed Challenge in front of /wp-login.php and /wp-admin/. Humans pass; password-guessing scripts don't. I considered allowing only US traffic, but I log in from Mexico too, and a country lock would mostly lock out me.

**The tunnel.** The Pi also runs Grafana, Uptime Kuma and Prometheus. The tunnel is configured in Cloudflare's dashboard, not on the Pi, so the only way to know what's public is to look. Two routes: manuel-elizaldi.com and www. Everything else stays on my home network.

**An old password.** Early in this build I committed wp-config.php to git, database password included. I untracked the file later, but git remembers everything. I rotated the database password and confirmed the new one matches no version in the history. A leaked secret that has been rotated is just a string.

**A third PHP issue.** On October 23, PHP published one more advisory, CVE-2026-115560, with no fix yet and low odds of mattering. The interim advice is to switch off a session feature my site never uses, one line in .htaccess:

```
php_flag session.upload_progress.enabled off
```

Every change went in after a backup (`wp db export` plus a tarball of plugins and themes) and into git afterwards.

Still on the list: real visitor IPs. Every request in my access log comes from ::1, the tunnel itself, which means the Friday scanner is anonymous. Apache's remoteip module fixes that. Next weekend.

### What Went on the Index Card

**Installed is not running.** A package upgrade changes files on disk. A process already in memory keeps running the old code until it restarts. Ask the running thing what version it is.

**Automatic updates are a cron job too.** "WordPress patches itself" was a belief I never tested. It depended on a self-request through Cloudflare, a TLS extension, and a PHP module I didn't know I was missing. `wp cron test` takes one second.

**Verify, then panic.** Four failed checksums looked like an intrusion. They were old files. Checking before assuming saved me from rebuilding a server that was fine.

---

The Friday visitor is still out there somewhere, knocking on someone else's /staging/ folder. On my Pi, `wp cron event list` now shows times in the future: eleven minutes, an hour, twelve hours. It's the most reassuring list I've read all month.

_This is part of a series documenting a three-node home lab build: the architecture decisions, the debugging, and the lessons that only show up when I type the commands myself._
