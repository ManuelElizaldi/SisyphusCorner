[[Storage]] [[Network]] [[SSD]] [[Raspberry Pi]] 

# Complete Step-by-Step Guide for Setting Up SSD NAS with Raspberry Pi

---

## 1. Format and Partition the SSD

1. Connect SSD to Raspberry Pi.
2. List devices:

```bash
lsblk
```

3. Identify SSD (e.g., `/dev/sda`).
4. Create a partition (GPT recommended for larger drives):

```bash
sudo parted /dev/sda mklabel gpt
sudo parted -a opt /dev/sda mkpart primary ext4 0% 100%
```

5. Format the partition (ext4 for Linux-only, NTFS for cross-platform):

```bash
sudo mkfs.ext4 /dev/sda1   # Linux-only
sudo mkfs.ntfs /dev/sda1   # Windows/Mac compatible
```

6. Note UUID:

```bash
sudo blkid /dev/sda1
```

---

## 2. Mount SSD on Raspberry Pi

1. Create mount point:

```bash
sudo mkdir -p /mnt/ssd
```

2. Mount manually:

```bash
sudo mount /dev/sda1 /mnt/ssd
```

3. Test read/write:

```bash
touch /mnt/ssd/test.txt
ls /mnt/ssd
```

---

## 3. Install Samba and Configure Share

1. Install Samba:

```bash
sudo apt update
sudo apt install samba -y
```

2. Backup and edit config:

```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup
sudo nano /etc/samba/smb.conf
```

3. Add share:

```
[SSD]
   path = /mnt/ssd
   browseable = yes
   writable = yes
   guest ok = no
   read only = no
   create mask = 0775
   directory mask = 0775
   valid users = manu
```

4. Add Samba password for user:

```bash
sudo smbpasswd -a manu
```

5. Restart Samba:

```bash
sudo systemctl restart smbd
```

---

## 4. Mount SMB Share on Linux Host

1. Create mount point:

```bash
sudo mkdir -p /mnt/remotessd
```

2. Test manual mount:

```bash
sudo mount -t cifs //100.118.68.64/SSD /mnt/remotessd -o username=manu,password=YourPassword,uid=1000,gid=1000,vers=3.0
```

3. Verify:

```bash
ls /mnt/remotessd
```

---

## 5. Make Mount Permanent on Linux

1. Create credentials file:

```bash
sudo nano /etc/cifs-creds
```

Add:

```
username=manu
password=YourPassword
```

Set permissions:

```bash
sudo chmod 600 /etc/cifs-creds
```

2. Edit fstab:

```bash
sudo nano /etc/fstab
```

Add:

```
//100.118.68.64/SSD /mnt/remotessd cifs credentials=/etc/cifs-creds,uid=1000,gid=1000,vers=3.0 0 0
```

3. Test fstab:

```bash
sudo mount -a
ls /mnt/remotessd
```

---

## 6. Mount SMB Share on macOS Host

1. Create mount point:

```bash
mkdir -p ~/mnt/remotessd
```

2. Edit `/etc/auto_smb`:

```bash
sudo nano /etc/auto_smb
```

Add:

```
remotessd -fstype=smbfs ://manu:YourPassword@100.118.68.64/SSD
```

3. Edit `/etc/auto_master`:

```bash
sudo nano /etc/auto_master
```

Add:

```
/Users/manuelelizaldi/mnt auto_smb
```

4. Reload automount:

```bash
sudo automount -vc
```

5. Access via:

```bash
ls ~/mnt/remotessd
```

---

## 7. Access from Other Devices

* **iOS:** Files app → Connect to Server → `smb://100.118.68.64/SSD`
* **Android:** Solid Explorer → Add storage → SMB → enter IP, share, credentials
* **Windows:** File Explorer → Map Network Drive → `\\100.118.68.64\SSD`

---

## 8. Best Practices

* Use **UUIDs** for partitions when mounting on the Pi.
* Protect passwords using **credentials file** on Linux or Keychain on macOS.
* Use **Tailscale VPN** for secure remote access.
* Keep **consistent mount points** across devices.
* Always test mounts with `ls` or `df -h` before rebooting.

---

## 9. Troubleshooting

* **Permission Denied:** Check Samba user/password and mount options.
* **Device Busy:** Use `lsof` or `fuser`.
* **Empty mount folder:** Ensure Pi share is active and mounted via network.
* **macOS automount errors:** Use a home directory mount point to avoid SIP restrictions.

---

This guide consolidates formatting, sharing, mounting, and automounting SSD across Linux and macOS hosts.
