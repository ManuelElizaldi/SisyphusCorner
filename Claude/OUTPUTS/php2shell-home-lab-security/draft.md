October 24, 2026

_A critical PHP bug sent me digging through my own server logs. The bug was the easy part. The hard part was finding out my website had quietly stopped patching itself._

---

Friday, 2:46 in the afternoon. Someone sends a POST request to the front page of manuel-elizaldi.com. Seconds later, the same visitor starts asking for a file called phpinfo.php. In /wp-admin/. In /staging/. In /beta/, /qa/, /webmail/, /htdocs/. About twenty doors knocked in under five seconds, every one answered with a 404.

I found this in my Apache access log a few hours after it happened, which is a strange way to meet a stranger.

I was in the log because of a headline. That week, a pair of PHP vulnerabilities nicknamed PHP2Shell (CVE-2026-109618 and CVE-2026-109619) went public with a 9.2 severity score. Both let an attacker run their own code on a server. Patches shipped on October 21, and reports said exploitation started before the patches did. My website runs on WordPress, WordPress runs on PHP, and PHP runs on a Raspberry Pi 5 sitting on my desk behind a Cloudflare Tunnel. A tunnel feels like protection. It isn't. The tunnel hands every request straight to Apache. It is a hallway, not a wall.

A disclaimer before going further: my site is not an enterprise or production system. It's a personal blog with one admin account, no customer data, no payment forms and no on-call rotation. This is a home lab story. Companies running real infrastructure have patch management, security teams and change windows for this kind of week. I have a Pi and a Friday afternoon.

### Installed Is Not Running

First question: which PHP am I running?

```
php -v
PHP 8.2.33 (cli)
```

The fixed version for the 8.2 branch is 8.2.35, so I was vulnerable, as expected. What I didn't expect came from asking the web server instead of the terminal. I dropped a one-line PHP file into the site, loaded it through Apache, and deleted it:

```
<?php echo PHP_VERSION;
```

8.2.32.

The terminal and the website were running two different PHPs. apt had installed 8.2.33 back in August, but Apache had been up since August 18, and it loads PHP into memory once, at startup. It never noticed the files on disk had changed. A patch sat on the drive for two months, unused, like a gym membership.

The fix is one line, and the restart at the end matters as much as the upgrade:

```
sudo apt update && sudo apt upgrade -y && sudo systemctl restart apache2
```

My first attempt failed because I ran it from inside the Claude Code prompt, where sudo has no terminal to ask for my password. Real terminal, real password, second try.

Then I asked the website again: 8.2.35. Debian's changelog for the package names both CVEs. MariaDB, OpenSSL, the kernel and cloudflared came along for the ride, and a reboot later the Pi was on the new kernel.

### Checking for Footprints

Patching closes the door. It doesn't tell me whether someone already walked through it. Exploitation was reported before disclosure, so I went looking for footprints, with Claude Code running the checks next to me. I'm a beginner at this, and a second pair of eyes that knows every wp-cli flag by heart makes a difference.

WordPress publishes checksums for its core files, and wp-cli compares them:

```
wp core verify-checksums
Success: WordPress installation verifies against checksums.
```

No PHP files hiding in the uploads folder, the classic place to drop a web shell. No files in the web root changed since October 17. One user account, mine. Nothing running as the web server user that shouldn't be.

Then the plugins. Four of them failed their checksum check, and my stomach dropped. The mismatches were a license file, a couple of icons, an extra readme. Tampering doesn't usually look like a changed SVG. After updating, all eleven plugins verified clean. The mismatch was age, not an intruder.

That update is where the real story was hiding.

### The Patches That Never Came

WordPress was on 6.8.3. The latest release in that branch was 6.8.11, eight security releases ahead of me. Nine plugins were behind too. WordPress installs minor security releases automatically; that was the whole reason I never worried about it. So why hadn't it?

```
wp cron event list
```

Every scheduled event read "now". Not "in 5 minutes". Now. Version checks, plugin update checks, all overdue. WP-Cron, WordPress's scheduler, wasn't running anything.

`wp cron test` had the answer:

```
Error: WP-Cron spawn failed ... sslv3 alert handshake failure
```

The chain took a while to untangle. WP-Cron doesn't run on a real clock. When someone visits the site, WordPress fires an HTTP request at itself, at https://manuel-elizaldi.com/wp-cron.php, to start its jobs in the background, and for that self-call it turns off certificate checking. My Pi didn't have PHP's curl extension, so WordPress fell back to a plainer socket connection. With verification off, that fallback also stops sending SNI, the part of the TLS handshake where the client says which website it wants. Cloudflare serves an enormous number of sites from the same IP addresses. A handshake that doesn't name a site gets rejected.

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
