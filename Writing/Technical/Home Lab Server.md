**Raspberry** pi 
# Terms
DHCP Dynamic Host Configuration Protocol -> Your router acting as a hotel receptionist. Each device that is connected gets a room (IP address). Default setting is that each device has a dynamic IP, one day you have `.65` and the next `.75`.  For home labbing that is an issue
- Why DHCP? For convenience, managing IPs is a lot of work, having a system that automatically sets IPs make it easy. If this system wasn't present you would have to add a new ip for each new device. You can think of DHCP as a parking lot. You might get the same spot each time you connect, but if a device was offline for some time some other device could've taken its place. 

Network Interface -> Physical or virtual port your computer uses to connect to a network. My Pi has 2, wifi and Ethernet. 

Static IP -> IP that never changes, the opposite of DHCP. 

Gateway -> The device that connects your local network to external networks. In a home setup this is the router. In a data center it's a dedicated network appliance. Without a gateway, your IP could talk to only devices with IP `192.168.0.x` but nothing outside of the network. 

Key term — /24 (CIDR notation): Defines the size of your network. `/24` means 254 possible devices, all sharing the `192.168.0.x` prefix. Your router is `.1`, your Pi is `.65`, your future Nitro 5s will be `.20` and `.21`.

DNS Domain name system -> The internet's phone book, translates human readable names like google.com into IP addresses. 

Upstream DNS -> When Pi-hole can't find a DNS record locally it will ask an upstream server. Google and Cloud Flare are the upstream servers for my pi-hole. They handle everything pi-hole doesn't have an answer to. 

IP routes -> lower metric = preferred route. 
- Metric: A priority score for network routes. 
```
dev end0  metric 100   ← lower number = higher priority
dev wlan0 metric 600   ← higher number = lower priority
```

**Key term — Web Server:** Software that listens on a port (usually 80 for HTTP, 443 for HTTPS) and responds to requests with web pages or data. When you type an address in your browser, a web server on the other end is what answers.

## Objective
I am an aspiring Solutions Architect/Cloud Engineer, theory + practice = great preparation. You need to have theory but having a lab that you can experiment with gives you the knowledge required. Nothing beats blowing up a node and fixing it from scratch.

## Brief summary of the architecture
I am trying to build a home lab where the brain of the operation is my raspberry pi. As of now, this little device is acting as a simple cloud storage, sharing a SSD through the my network. 

I wanted to upscale the capabilities of this device, so I pulled out 2 of my old gaming laptops that I am not using anymore, right now I appreciate being a cable, old device hoarder, even do it is a mess to keep these things organized. 

I don't come from a technical background and even though I have been gaming my entire life and know that Ethernet cable is like an IV injected directly into your bloodstream, it didn't occur to me that I had to plug everything via Ethernet cable. Before this project I had my raspberry pi connected via WIFI, but after ordering a Ethernet switch box and enough Ethernet cables for the whole set up it was time to start working. 

There's 2 concepts I had to revisit here:

- DNS: Domain Name System, the internet's phone book. DNS is a system that translated IPs (a device's phone) into readable names like Google.com 
- DNS Sinkhole: This hides your IP in the phone book, when you look up an IP you get redirected to a dead end 

First thing in our agenda install a DNS Sink Hole - Pi Hole. Pi-Hole can also work as a local DNS server, which will help us give nicknames to our nodes (other devices). If I wanted to connect to my node A, instead of typing its ip, I can just type the nickname given to it. 

Without Pi Hole I would need to manage an intricate map of IPs 

```
write here how to install pi hole
```

# Static IP & Networking 
First we need to find out which is the ethernet IP, for this we check the IP routes: 
`ip route`

Here's the output of `ip route`:
```
manu@manupi:~ $ ip route
default via 192.168.0.1 dev end0 proto static metric 100 
default via 192.168.0.1 dev wlan0 proto dhcp src 192.168.0.66 metric 600 
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown 
192.168.0.0/24 dev end0 proto kernel scope link src 192.168.0.65 metric 100 
192.168.0.0/24 dev wlan0 proto kernel scope link src 192.168.0.66 metric 600 
```

Some things to point out -> you can see the gateway ip `192.168.0.1` and also `proto static` which means it is a static IP. wlan0 is still on proto dhcp protocol. 

Then we need to modify the network profile to a static IP. Stop asking the router for a new IP 
#### CIDR Block
IP we are choosing: 192.168.0.65/24 with a cider block of /24 
- According to Claude /24 is a good CIDR size for a home network 

192.168.0.X /24 for 254 devices 

Here we are setting up the WIFI IP as our static IP
To modify the network profile: `sudo nmcli connection modify "Wired connection 1" ipv4.addresses 192.168.0.65/24`

you can double check if this worked with :
`ip addr show end0`

## Setting up gateway
Then we run : `sudo nmcli connection modify "Wired connection 1" ipv4.gateway 192.168.0.1`

we are setting up `192.168.0.1` as a gateway.  

after running: curl http://192.168.0.20
- The Pi thinks: _"Is `192.168.0.20` on my local network (`192.168.0.x`)? Yes it is."_ It sends the packet directly — no gateway involved. The router never sees it.

setting up: google and cloudflare as the DNS servers 
`sudo nmcli connection modify "Wired connection 1" ipv4.dns "8.8.8.8,1.1.1.1"`

### Why set up a gateway?
We are telling the Pi that if it needs to reach something outside the local network like the internet, API, software update, etc. it needs to hand the traffic to `192.168.0.1` first, which is my router. Then the router will know how to reach the internet. 

## Setting up a temporary DNS server
Pi is getting its DNS server assigned by the router via DHCP, now we are going to set this up as manual `ipv4.method manual`, we are telling the Pi -> stop asking the router for the DNS server, do it manually. If we go manual without specifying a DNS server the Pi wont be able to translate domain names. 

So right now we are pre-setting DNS servers before we cut the cord from DHCP, ensuring nothing breaks when we flip to manual.


> [!NOTE] **Why Google and Cloudflare specifically?** 
> They're fast, reliable, and universally trusted public DNS servers. Temporary choice — once Pi-hole is stable we'll swap this to `192.168.0.65` so the Pi resolves everything through itself.
## Set DNS servers - Switching from dynamic to static

`sudo nmcli connection modify "Wired connection 1" ipv4.method manual`
This is the actual command to tell the router to stop asking for an IP, gateway and DNS, use everything we just manually set instead. 

Pi is getting its DNS server assigned automatically by your router via DHCP by default. 

### DNS Server: Why we need this?
This is temporary, but if Pi-hole does not know the answer to a DNS it will ask google and cloudflare. 

# Checkpoint
identity card for your Pi on the network 

| Setting    | Value                | Purpose                     |
| ---------- | -------------------- | --------------------------- |
| IP Address | `192.168.0.65/24`    | Who the Pi is               |
| Gateway    | `192.168.0.1`        | How it reaches the internet |
| DNS        | `8.8.8.8`, `1.1.1.1` | How it resolves names       |
| Method     | `manual`             | It manages itself, no DHCP  |

## Activating the steps we just performed
`sudo nmcli connection up "Wired connection 1"`

output -> `Connection successfully activated (D-Bus active path: /org/freedesktop/NetworkManager/ActiveConnection/12)
`
# Setting up Pi-Hole
Set it up as our local DNS server

listens on port 53 - standard DNS port. Every DNS query from every device on your network lands here. 

We need to add the local DNS records for the lab. We open the pi-hole web UI. On the browser we enter: `http://192.168.0.65/admin`

One quick note -> I am also hosting a web server on this raspberry pi, which is using port 80. We couldn't open the pi-hole admin page since the port was being used by wordpress/apache. This is the command we use to investigate:
- `sudo ss -tlnp | grep :80` 
	- We stopped apache's services by running -> `sudo systemctl stop apache2` and `sudo systemctl disable apache2`

Another problem I encountered was that pihole web server was not installed on my raspberrypi. We installed `lighttpd`. and enabled it `sudo systemctl enable --now lighttpd` and checked its status `sudo systemctl status lighttpd`. Lighttpd is good for raspberrypi since RAM and memory are limited. 


> [!NOTE] What is lighttpd?
> It's a web server — the same category of software as Apache. Its whole job is to receive HTTP requests and serve web pages back.

|                  | Apache                      | lighttpd                            |
| ---------------- | --------------------------- | ----------------------------------- |
| **Designed for** | Full websites, complex apps | Lightweight, low-resource tools     |
| **RAM usage**    | Higher                      | Very low                            |
| **Best for**     | Your personal website       | Admin UIs, small tools like Pi-hole |

#### How to check if a service is listening to a port:
`sudo lsof -i :80`

I did this to check if lighttpd is actually listening for incoming requests

We also checked the php setting for lighttpd
```
manu@manupi:~ $ sudo lighttpd-enable-mod fastcgi-php
Met dependency: fastcgi
Enabling fastcgi-php: ok
Enabling fastcgi: ok
Run "service lighttpd force-reload" to enable changes
```


I needed the CGI version of PHP that goes with lighttpd 


lighttpd was taking too long to respond, so we did more troubleshooting: we checked port 80 again, and it was good , but then we checked the UFW (firewall) was blocking port 80. 
```
manu@manupi:~ $ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
22                         ALLOW       Anywhere                  
22/tcp                     ALLOW       Anywhere                  
3333/tcp                   ALLOW       Anywhere                  
22 (v6)                    ALLOW       Anywhere (v6)             
22/tcp (v6)                ALLOW       Anywhere (v6)             
3333/tcp (v6)              ALLOW       Anywhere (v6) 
```

Then we ran the command: `manu@manupi:~ $ sudo ufw allow 80/tcp` to allow this, now it showed on the output of `sudo ufw status`

#note: **On your local network — no, it's not risky.** Port 80 will only be reachable by devices on `192.168.0.x` — your home network. Your laptop, phone, the Nitro 5s. Nobody on the internet can reach it unless you explicitly forward port 80 on your router to the Pi, which we're not doing

**On the open internet — yes, it would be risky.** Port 80 with no authentication is a common target for bots that constantly scan the internet looking for exposed admin panels, login pages, and vulnerabilities. Pi-hole's admin UI on a public IP would be a problem.

The distinction that matters here:

| Scenario                               | Risk                                         |
| -------------------------------------- | -------------------------------------------- |
| Port 80 open, no router port forward   | Only your home devices can reach it — safe ✅ |
| Port 80 open + router port forwards it | The whole internet can reach it — risky ❌    |

