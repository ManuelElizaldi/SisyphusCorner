Here is a comprehensive technical guide based on your journey. It is structured to serve as both a summary of your specific troubleshooting steps and an educational resource for your article.
  
---

# Project Report: Sovereign Solo Mining with NerdMiner & Raspberry Pi

## 1. Executive Summary

This project involves setting up a fully sovereign, solo Bitcoin mining operation. Unlike pool mining, where hashrate is aggregated, this setup attempts to solve a block alone (a "lottery miner"). The architecture consists of three distinct layers:

1. **The Brain (Bitcoin Core):** Validates the blockchain and propagates new blocks.1
    
2. **The Translator (CKPool):** Bridges the gap between the mining hardware and the node.
    
3. **The Muscle (NerdMiner):** The ESP32-based hardware performing the SHA-256 hashing.
    

---

## 2. Component Overview

### What is a NerdMiner?

The **NerdMiner** is an open-source educational hardware project based on the **ESP32 microcontroller**.2

- **Purpose:** It allows anyone to "mine" Bitcoin for ~$20 USD. While the probability of finding a block is infinitesimally small (creating a "lottery" dynamic), its primary value is educational—teaching the user how hashing, difficulty, and stratum protocols work.
    
- **Hardware Variants:**
    
    - _LILYGO T-Display S3:_ The standard "all-in-one" board.3
        
    - _Generic ESP32 (WROOM):_ The DIY "sandwich" style with separate screen.
        
    - _CYD (Cheap Yellow Display):_4 The model used in this project (`ESP32-2432S028`), featuring a large touch screen and different display drivers.5
        
        +1
        

### What is CKPool?

**CKPool (Kano's Pool)** is a high-performance, lightweight Bitcoin mining pool server code.6

- **Why do we need it?** You cannot connect a miner directly to Bitcoin Core. Bitcoin Core removed its internal miner long ago and speaks **RPC** (Remote Procedure Call), while mining hardware speaks **Stratum Protocol**.
    
- **Function:** CKPool acts as a "Stratum Proxy." It gets work templates from Bitcoin Core, converts them into a format the NerdMiner understands (Stratum), and if the miner finds a solution, CKPool submits it back to the Core.
    

---

## 3. Configuration Files (The "Source of Truth")

These are the final, working configurations used to establish the local communication pipeline.

### A. Bitcoin Core Config (`/etc/bitcoin.conf`)

This file opens the doors for CKPool to talk to the node.

Ini, TOML

```
# --- General ---
server=1
daemon=1
txindex=1

# --- RPC Settings (The API for CKPool) ---
rpcuser=admin
rpcpassword=1234
rpcport=8332
rpcallowip=127.0.0.1
rpcbind=127.0.0.1

# --- ZMQ Settings (Instant Block Notification) ---
# Crucial for mining! CKPool needs ZMQ to know INSTANTLY when a new block
# arrives so it can stop working on the old one.
zmqpubrawblock=tcp://127.0.0.1:28332
zmqpubrawtx=tcp://127.0.0.1:28333
zmqpubhashblock=tcp://127.0.0.1:28332
```

### B. CKPool Config (`ckpool.conf`)

This file tells the pool where the node is and how to authenticate.

JSON

```
{
  "btcd" : [
    {
      "url" : "127.0.0.1:8332",
      "auth" : "admin",
      "pass" : "1234",
      "notify" : true
    }
  ],
  "btcaddress" : "YOUR_BTC_ADDRESS_HERE",
  "btcsig" : "/Mined by Manu/",
  "blockpoll" : 100,
  "startdiff" : 1, 
  "zmqblock" : "tcp://127.0.0.1:28332",
  "logdir" : "logs"
}
```

_Note on `startdiff`: Set to `1` for NerdMiners. High difficulty (e.g., 42) makes it look like the miner is dead because it takes too long to submit a share._

---

## 4. Troubleshooting Case Study

During deployment, several critical issues were encountered. This section details the symptoms and solutions.

### Issue 1: "Black Screen" on NerdMiner

- **Symptom:** After flashing, the device had power (red light) but the screen remained off.
    
- **Root Cause:** Firmware Mismatch. The user selected "T-Display S3" and "AMOLED" firmware, but the hardware was actually a **CYD (Cheap Yellow Display)** model.
    
- **Solution:** Flashed specific **`NerdMiner V2 - CYD`** firmware.
    

### Issue 2: "Connect from..." but Hashrate 0.00

- **Symptom:** Miner connected to the Pi, but sat idle.
    
- **Root Cause:** **Blockchain Desync.** The Bitcoin node was only 85% synced (`verificationprogress < 0.99`). You cannot mine on a node that doesn't know the current state of the ledger.
    
- **Solution:** Waited for `verificationprogress` to hit `0.9999` (Syncd).
    

### Issue 3: The "Zombie" Process

- **Symptom:** Running `pkill bitcoind` failed; the process ID (PID) changed instantly, indicating it was restarting immediately.
    
- **Root Cause:** A background watchdog tool called **Monit** was installed. It was detecting the "crash" (the kill command) and automatically restarting the service using the wrong config file.
    
- **Solution:**
    
    1. Stopped the watchdog: `sudo systemctl stop monit`.
        
    2. Killed the process: `sudo pkill -9 bitcoind`.
        
    3. Restarted manually with the correct config.
        

### Issue 4: Firewall Blocking Port 3333

- **Symptom:** Miner cycled through fallback pools (public-pool.io) despite correct IP settings.
    
- **Root Cause:** Linux firewall (`ufw`) was Active and blocking inbound traffic on port 3333.
    
- **Solution:** `sudo ufw allow 3333/tcp`.
    

---

## 5. Automation (The "Set It and Forget It" Script)

To ensure resilience against power outages, we implemented an `init` script that handles the dependency order (Bitcoin must start before CKPool).

**Script: `~/start_mining.sh`**

Bash

```
#!/bin/bash

# 1. Smart Start for Bitcoin Core
if ! pidof bitcoind > /dev/null; then
    echo "Starting Bitcoin Core..."
    /usr/local/bin/bitcoind -daemon -conf=/etc/bitcoin.conf
    echo "Waiting 90s for DB load..."
    sleep 90
else
    echo "Bitcoin Core already running."
fi

# 2. Start CKPool in a Detached Screen Session
echo "Launching CKPool..."
/usr/bin/screen -dmS mining /home/manu/bitcoinapp/ckpool/src/ckpool -c /home/manu/bitcoinapp/ckpool/ckpool.conf -k
```

Auto-Start Hook:

Added to crontab (crontab -e):

@reboot /home/manu/start_mining.sh

---

## 6. Key Educational Concepts for the Article

### 1. The "Stratum" Gap

Explain that Bitcoin Core is a bank vault—it only cares about verifying transactions. It doesn't care about "work." Miners are like workers who need a foreman to tell them what to dig. CKPool is that foreman (Stratum Server). It translates the Vault's requirements into a job the workers can understand.

### 2. ZMQ (ZeroMQ)

Why is this in the config? Speed. In Bitcoin mining, milliseconds matter. If a new block is found in China, your node needs to tell your miner to **stop** working on the old block immediately. ZMQ is a high-speed messaging pipe that screams "NEW BLOCK!" to CKPool the instant it arrives, preventing "Stale Shares" (work that is no longer valid).

### 3. Permission Management

A major hurdle in this project was Linux permissions (`sudo` vs user). Bitcoin Core creates lock files.7 If you run it once as `root` (sudo), it locks the files. If you later try to run it as `user`, it fails. This highlights the importance of `chown` (Change Ownership) and running services consistently as a specific user.