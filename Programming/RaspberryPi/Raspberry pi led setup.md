2025-4-30
Tags: [[Programming]] [[Automation]] [[Raspberry Pi]]

Use the [ESP 32 boards](https://www.amazon.com/dp/B09GK74F7N?ref=ppx_yo2ov_dt_b_fed_asin_title) This one does not require any previous setup 

This project has been challenging for one reason. I live in an apartment that has an Enterprise Wi-Fi Set up (WPA2). This small although large in complexity hurdle made me go down the rabbit hole of Networking. My original plan was to host my web app led light controller, then connect the ESP32 board to my network and then easily control the light system through a local host web app.

Also, my raspberry pi and my computer where not able to establish a SSH connection (another term I learned while building this) so I had to set up a [Tailscale](tailscale.com) (WireGuard Protocol) VPN connection in order for me to write my raspberry scripts from my pc. Also, in the future I plan on creating a virtual server/hard drive and tailscale will allow me to use my raspberry pi for that purpose 



This project has showed me that even though you failed at first, you gain knowledge, that sooner or later can be used for future projects. 

1) Lesson: When things go bad or not according to plan, you are not really failing, you are learning. It's a simple mind shift and maybe I was already doing this unconsciously throughout my life, but during this project I became aware that projects take time, you can't just rush things and expect them to work. You will have to find work arounds and do some research to land where you want to. 

### Connecting to Raspberry pi 
do it through vscode extension: [Remote SSH](https://marketplace.visualstudio.com/items/?itemName=ms-vscode-remote.remote-ssh)

ip address: 

### WLed Install

After installing and setting up wifi, a window should appear saying 'Visit Device' from the web address in the window that pops up you can get the IP 

Pymakr extension


### Post and Get
HTTP protocols to send and extract information

### Flask 
Routes in flask determine what page the user is going to visit.
- ('/'): is home
	- For example: You can do something like ('/about') for the about page
- If the user goes to ('/') what function should python run? Example:

```python
@app.route('/')
def index():
    return "Hello, world!"
```



----
### ✅ What We Did to Enable the Hotspot (Access Point) on Your Raspberry Pi:

1. **Enabled required services**:
    
    - `hostapd`: Creates and manages the Wi-Fi hotspot.
        
    - `dnsmasq`: Assigns IP addresses (DHCP) to devices that connect to the hotspot.
        
2. **Configured NetworkManager**:
    
    - Created a new hotspot connection with `nmcli`.
        
    - Set the SSID (e.g., `WLEDNet`), password, and mode `ap`.
        
3. **Stopped the Pi from connecting to your enterprise Wi-Fi**:
    
    - Because a Wi-Fi card can’t be both an access point _and_ a client at the same time (on the same interface), we disconnected from your enterprise Wi-Fi (`WIRESTAR.NET - SECURE`).
        
4. **Manually activated the hotspot**:
    
    - Brought the `hotspot` connection up with `nmcli`.
        
    - Confirmed it switched to **AP mode** with `iw dev wlan0 info`.
        

Now your ESP32 boards can scan for Wi-Fi and connect to `WLEDNet`.

---
### Reference