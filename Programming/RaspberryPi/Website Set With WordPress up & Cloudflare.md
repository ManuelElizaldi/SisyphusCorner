I've updated the markdown file below.

I added the **HTTP Host Header** setting to section **B** (this was the hidden setting that made WordPress realize who it was) and ensured all the **debugging commands** we used (including finding your IP and checking ports) are listed at the bottom.

Markdownasda

````
# Project Log: Self-Hosted WordPress with Cloudflare Tunnel

**Date:** February 4, 2026
**Host:** Raspberry Pi 4 (Kubernetes/K3s Cluster)
**Domain:** `manuel-elizaldi.com`
**Network Stack:** Cloudflare Tunnel (Cloudflared) -> Apache (Port 80)

## 1. The Architecture
Instead of opening Port 80 on the home router (which exposes the home IP), we use **Cloudflare Tunnel**.
1.  **User** visits `https://manuel-elizaldi.com`.
2.  **Cloudflare Edge** receives the request and handles SSL/HTTPS.
3.  **Tunnel** forwards the request securely to the `cloudflared` agent running on the Raspberry Pi.
4.  **Agent** forwards traffic to the local Apache server at `192.168.0.66:80`.
5.  **WordPress** serves the site, and the Agent sends it back up the tunnel.

---

## 2. The Hurdles & Solutions

### Issue A: "Address Not Found" (DNS Mismatch)
* **Symptoms:** Phone browser showed `NXDOMAIN` or "Address Not Found."
* **Cause:** We had two conflicting CNAME records (one for `www`, one for root) pointing to different Tunnel IDs.
* **Fix:** We cleaned up the DNS records in the Cloudflare Dashboard so `manuel-elizaldi.com` pointed to the single, active Tunnel UUID.

### Issue B: "Bad Gateway" (The Loopback Trap)
* **Symptoms:** Cloudflare showed a 502 error.
* **Cause:** The Tunnel was pointed to `localhost:80` (or `127.0.0.1:80`). Because the Pi is running a Kubernetes (K3s) cluster, the network interface `cni0` hijacked the localhost traffic, preventing the Tunnel from seeing Apache.
* **Fix:** We pointed the Tunnel Route to the **LAN IP** (`192.168.0.66`) instead of `localhost`. This forced traffic through the correct network interface.

### Issue C: "Redirect Loop" (The Identity Crisis)
* **Symptoms:** `curl` showed a `301 Moved Permanently` pointing to the internal Tailscale IP (`100.118...`), causing infinite redirects or connection failures on public 5G/LTE.
* **Cause:** WordPress thought its address was still the private Tailscale IP saved in its database. Additionally, it tried to force HTTPS upgrades because it didn't know Cloudflare was already handling SSL.
* **Fix:** We injected code into `wp-config.php` to force WordPress to accept the visitor's domain name dynamically.

---

## 3. Key Configuration Files

### A. WordPress Configuration Override
**File:** `/var/www/html/wp-config.php`
**Purpose:** Handles Reverse Proxy logic (SSL termination) and dynamic Hostname resolution.

```php
/* Add this ABOVE the "That's all, stop editing" line */

// 1. Force WordPress to accept the domain the visitor typed (e.g., manuel-elizaldi.com)
define('WP_HOME', 'https://' . $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'https://' . $_SERVER['HTTP_HOST']);

// 2. Trick WordPress into knowing the connection is Secure (HTTPS)
//    (Because Cloudflare handles SSL, the traffic hits the Pi as HTTP.
//     Without this, WordPress creates an infinite redirect loop.)
$_SERVER['HTTPS'] = 'on';
````

### B. Cloudflare Tunnel Route

**Location:** Cloudflare Zero Trust Dashboard > Tunnels > Public Hostnames

**Route:** `manuel-elizaldi.com`

**1. Service Settings (The Destination)**

- **Service Type:** `HTTP`
    
- **URL:** `192.168.0.66:80`
    
    - _Note:_ We used the LAN IP (from `wlan0`) because `localhost` was hijacked by Kubernetes/Docker interfaces.
        

**2. Additional Application Settings (The Identity)**

- **Menu:** Click "Additional application settings" > "HTTP Host Header"
    
- **Origin Server Name:** `manuel-elizaldi.com`
    
    - _Note:_ This ensures WordPress receives the correct domain name header, preventing it from confusing the request with an internal IP query.
        

---

## 4. Useful Debugging Commands

**1. Find your actual LAN IP**

If `localhost` isn't working, use this to find the IP assigned to `wlan0` (WiFi) or `eth0` (Ethernet).

Bash

```
ip a
```

**2. Check what ports are listening**

This confirms if Apache/WordPress is actually running and which port (usually 80) it is on.

Bash

```
sudo ss -tulpn | grep LISTEN
# Look for: tcp LISTEN 0 511 *:80 ... users:(("apache2"...))
```

**3. Test the server locally (Bypass Cloudflare)**

Run this on the Pi to see if the website responds to internal requests.

Bash

```
curl -I [http://192.168.0.66](http://192.168.0.66)
# Success: "HTTP/1.1 200 OK" or "301 Moved Permanently"
# Failure: "Connection Refused"
```

**4. Edit the WordPress Config**

Bash

```
sudo nano /var/www/html/wp-config.php
# Use Ctrl+W to search text
# Use Ctrl+X, then Y, then Enter to save and exit
```