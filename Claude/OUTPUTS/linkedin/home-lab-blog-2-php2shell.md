Friday afternoon, a YouTube video about PHP2Shell: a bug that lets attackers run their own code on a server. My website runs on PHP, on a Raspberry Pi sitting on my desk.

I opened my Apache log. A bot had already been there, knocking on twenty doors in five seconds, looking for phpinfo.php.

The terminal said PHP 8.2.33. The website was running 8.2.32, an older copy Apache had held in memory since August. Installed is not running.

The real find was quieter. WordPress was eight security releases behind. Its automatic updates had been failing on every page view, rejected by Cloudflare over a missing PHP extension and three letters I had never heard of: SNI. Nothing complained. Nothing told me.

Second time my home lab has taught me the same lesson. Automatic updates are just a cron job nobody checks.

Full write-up, with the checks, the fixes and the Cloudflare rules. A home lab story, not an enterprise playbook: [link]

#LearningInPublic #HomeLab #CyberSecurity #DevOps #WordPress
