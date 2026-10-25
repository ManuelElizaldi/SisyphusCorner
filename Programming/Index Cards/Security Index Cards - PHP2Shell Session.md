2026-10-25
Tags: [[Security]] [[Home Lab]] [[DevOps]] [[Linux]] [[Networking]] [[WordPress]]

Index cards from the PHP2Shell security session (Oct 23–25, 2026). Each card: what it is, where it showed up on my Pi, and a command to try.
Story version: [[Home Lab Blog 2 A PHP Bug, a bot scanning my website and an update that never came]]

---

## 1. Vulnerabilities & response

### CVE (Common Vulnerabilities and Exposures)
A public ID for one specific security bug, so everyone talks about the same thing. Format: `CVE-YEAR-NUMBER`.
- On my Pi: PHP2Shell = CVE-2026-109618 + CVE-2026-109619.
- Debian's package changelog lists which CVEs a version fixes:
```sh
zcat /usr/share/doc/php8.2-common/changelog.Debian.gz | head -15
```

### CVSS (Common Vulnerability Scoring System)
Severity score from 0 to 10. 9.0+ = critical. Measures how bad the bug is in general, not how exposed *my* setup is.
- PHP2Shell scored 9.2.

### RCE (Remote Code Execution)
The worst category: an attacker on the internet makes my server run their code. With RCE they become the web server user and can read or change anything that user can.

### Zero-day / exploited before disclosure
A bug attackers use before a fix exists or before it's public. PHP2Shell attempts were seen days before the patch. Patching fast matters, and so does checking whether someone got in *before* the patch.

### Patch vs. mitigation
- **Patch** = the real fix (new version of the software).
- **Mitigation** = a workaround that lowers risk until the patch exists.
- On my Pi: CVE-2026-115560 had no patch yet, so the mitigation was turning off an unused feature in `.htaccess`:
```apache
php_flag session.upload_progress.enabled off
```

### Attack surface
Everything an attacker can reach: open ports, public pages, plugins, login forms. Smaller surface = fewer chances. Each WordPress plugin adds surface.

### Defense in depth
Layers, so one failure isn't the end: network (tunnel, no open ports) → requests (Cloudflare WAF) → software (patched PHP and WordPress) → data (backups, rotated passwords). The tunnel alone couldn't stop PHP2Shell; patching could.

---

## 2. Installed vs. running

### Installed ≠ running
`apt upgrade` replaces files on disk. A process that's already running keeps the old code in memory until it restarts.
- On my Pi: the terminal said PHP 8.2.33, while Apache (up since Aug 18) was serving 8.2.32.
- Always ask the *running* thing:
```sh
systemctl show apache2 -p ActiveEnterTimestamp   # when did it last start?
```

### CLI PHP vs. Apache PHP (SAPI)
PHP comes in several builds called SAPIs (Server APIs). `php8.2-cli` is the terminal one; `libapache2-mod-php8.2` lives inside Apache. Same version number, separate copies. `php -v` only checks the CLI one.

### mod_php + prefork workers
Apache with `mpm_prefork` keeps a pool of worker processes, and each one handles many requests in turn. One PHP2Shell bug abused leftover state from one request in the next request on the same worker.

### restart vs. reload vs. reboot
- `systemctl reload` = re-read config, keep running (good for config changes)
- `systemctl restart` = stop and start (needed to load new program code)
- `reboot` = needed for a new **kernel**
```sh
uname -r                                  # kernel running now
dpkg -l linux-image-rpi-2712 | grep ^ii   # kernel installed
```

### apt "held back" packages
`apt upgrade` skips updates that need new packages installed (on my Pi: `rpi-eeprom`). `apt full-upgrade` installs them.

---

## 3. Checking for a break-in

### Checksum / hash verification
A fingerprint of a file. If even one byte changes, the fingerprint changes. WordPress publishes the fingerprints of its official files.
```sh
wp core verify-checksums
wp plugin verify-checksums --all
```
- Lesson: 4 plugins "failed", but it was old files, not tampering. After updating, all 11 verified. **Verify, then panic.**

### IoC (Indicator of Compromise)
Evidence of a break-in. What I checked:
- PHP files in `wp-content/uploads/` (should be none)
- recently changed files in the web root
- unknown admin users
- odd processes running as `www-data`
```sh
find html/wp-content/uploads -iname '*.php*'
find html -type f -newermt 2026-10-17
wp user list
```

### Web shell
A small malicious script an attacker uploads so they can run commands through the browser. The classic hiding spot is the uploads folder, which is why PHP files there are a red flag.

### Recon scanner
A bot that knocks on common paths looking for weak spots (`/phpinfo.php`, `/.env`, `/staging/`). Not a targeted attack, just constant background noise. Friday's visitor tried about 20 paths in 5 seconds; every one got a 404.

### phpinfo() / information disclosure
`phpinfo()` prints the PHP version and settings. Gold for an attacker: it tells them which bugs to try. Never leave one public. My `expose_php = Off` hides the version from response headers too.

### Access log & error log
- `/var/log/apache2/access.log` = every request: who, when, what path, which status code.
- `/var/log/apache2/error.log` = what went wrong.
```sh
grep '"POST' /var/log/apache2/access.log | tail
zcat -f /var/log/apache2/access.log* | grep -i phpinfo
```

### HTTP status codes that matter here
- `200` OK
- `301` moved (redirect)
- `403` forbidden (blocked on purpose, e.g. `xmlrpc.php`)
- `404` not found
- `400` bad request

---

## 4. WordPress

### wp-cli
WordPress from the terminal: update, verify, back up, inspect. Run it with `--path=/mnt/ssd/webpage/html`.

### WP-Cron
WordPress's scheduler. **Not a real clock**: it only runs when someone loads a page, which makes WordPress send a web request to itself. If that request fails, nothing scheduled runs, including automatic updates.
```sh
wp cron test          # does the self-request work?
wp cron event list    # "now" = overdue. Healthy = countdowns
```

### Loopback request
A server calling itself over the network. On my Pi it went out to Cloudflare and back, which is why a TLS detail could break it.

### Automatic updates
WordPress installs minor/security releases by itself, but only through WP-Cron. "Automatic" depends on the scheduler working. 6.8.3 → 6.8.11 = eight releases missed.

### Plugin supply-chain risk
Plugins are code written by other people, running with full access to my site. Keep them few, keep them updated, delete the unused ones.

---

## 5. Network & TLS

### TLS handshake
The opening exchange of an HTTPS connection: agree on encryption, check the certificate. "handshake failure" = it broke before any web page was sent.

### SNI (Server Name Indication)
In the handshake, the client says which site it wants, in plain text: "I'm here for manuel-elizaldi.com". Needed when many sites share one IP (Cloudflare).
- On my Pi: without `php8.2-curl`, WordPress's self-request sent no SNI, so Cloudflare refused it and WP-Cron died silently.
```sh
openssl s_client -connect manuel-elizaldi.com:443 -servername manuel-elizaldi.com </dev/null | head -5   # works
openssl s_client -connect manuel-elizaldi.com:443 -noservername </dev/null 2>&1 | grep -i alert   # refused
```

### Certificate verification (`sslverify`)
Checking that the certificate really belongs to the site. Turning it off is risky; WordPress does it only for self-requests.

### Reverse proxy
A server in front of my server that receives requests and passes them along. Cloudflare is my reverse proxy: visitors only ever see Cloudflare.

### Cloudflare Tunnel
`cloudflared` opens an **outbound** connection to Cloudflare, so there are no open ports on my router and my home IP stays hidden. It protects the network layer. It does **not** inspect requests: valid-looking malicious requests still reach Apache. A guarded hallway, not a wall.

### Origin
The real server behind the proxy (my Pi). Keeping the origin's address hidden is part of the point of a tunnel.

### WAF (Web Application Firewall)
Rules that inspect requests and block or challenge bad ones *before* they reach the origin. Mine puts a Managed Challenge on `/wp-login.php` and `/wp-admin/`.

### Managed Challenge
Cloudflare's "are you human?" check, judged on the browser and its behavior, not on location. Humans pass (usually without clicking); scripts don't. Better than a country block when I log in from both the US and Mexico.

### Ingress / public hostname
The tunnel's routing table: which public names go to which local service. Mine: `manuel-elizaldi.com` and `www` → `localhost:8080` only. Grafana and Uptime Kuma are not exposed.

### `::1` / localhost and `CF-Connecting-IP`
`::1` is "this machine" (IPv6 localhost). Every request in my log shows `::1` because it arrives through the tunnel. Cloudflare passes the real visitor IP in the `CF-Connecting-IP` header; Apache's `mod_remoteip` can log it.

---

## 6. Secrets & git

### Secret rotation
Replacing a password or key with a new one. A leaked secret that has been rotated is just a harmless string. Rotating beats trying to erase every copy.

### Git history never forgets
Once a secret is committed, it stays in history even after the file is deleted or ignored.

### `.gitignore` doesn't untrack
It only stops *new* files from being added. Files already tracked stay tracked until:
```sh
git rm --cached <file>
```

### One-way fingerprint comparison
To check that a new password differs from old ones without showing either: compare their hashes (sha256). Same hash = same password.

---

## 7. Habits

### Backup before change
```sh
wp db export ~/wp-backups/wp_blog-$(date +%F-%H%M).sql
```
Plus a tarball of plugins and themes. A rollback plan is what makes updating safe.

### Silent failure
The default state of an unmonitored job is broken and quiet. Three times now: the dead backup cron (typo), cron with no mail server, WP-Cron with no SNI. **If it matters, something must confirm it ran.**

### Least privilege
Each user or program gets only the access it needs. My web root is on NTFS (everything 777), so if `www-data` were compromised it could write anywhere. To fix on the ext4 SSD.

### sudo needs a TTY
sudo reads the password from a real terminal (TTY), not from piped input. That's why `! sudo …` inside Claude Code failed: no terminal to ask in.

### `&&` chaining
`a && b && c` runs the next command only if the previous one succeeded. A failed `sudo` stops the whole chain safely, with nothing half-done.
