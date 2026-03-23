**Raspberry** pi 


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

### Static IP & Networking 

Then we need to modify the network profile to a static IP. Stop asking the router for a new IP 

#### CIDR Block
IP we are choosing: 192.168.0.66/24 with a cider block of /24 
- According to Claude /24 is a good CIDR size for a home network 

192.168.0.X /24 for 254 devices 


To modify the network profile: `sudo nmcli connection modify "Wired connection 1" ipv4.addresses 192.168.0.66/24`

Then we run : `sudo nmcli connection modify "Wired connection 1" ipv4.gateway 192.168.0.1`

we are setting up 192.168.0.1 as a gateway.  

after running: curl http://192.168.0.20
- The Pi thinks: _"Is `192.168.0.20` on my local network (`192.168.0.x`)? Yes it is."_ It sends the packet directly — no gateway involved. The router never sees it.

setting up: google and cloudflare as the DNS servers 
`sudo nmcli connection modify "Wired connection 1" ipv4.dns "8.8.8.8,1.1.1.1"`

Pi is getting its DNS server assigned automatically by your router via DHCP by default 

DHCP:

DNS Server: Why we need this? 
