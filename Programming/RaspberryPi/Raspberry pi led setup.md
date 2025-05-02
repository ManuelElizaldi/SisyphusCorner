2025-4-30
Tags: [[Programming]] [[Automation]] [[Raspberry Pi]]

Use the [ESP 32 boards](https://www.amazon.com/dp/B09GK74F7N?ref=ppx_yo2ov_dt_b_fed_asin_title) This one does not require any previous setup 

### Connecting to Raspberry pi 
do it through vscode extension: [Remote SSH](https://marketplace.visualstudio.com/items/?itemName=ms-vscode-remote.remote-ssh)

ip address: 

### WLed Install

After installing and setting up wifi, a window should appear saying 'Visit Device' from the web address in the window that pops up you can get the IP 

Pymakr extension


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