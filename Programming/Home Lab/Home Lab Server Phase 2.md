## Phase 1 — Raspberry Pi Control Node

|Task|Status|
|---|---|
|Static IP on ethernet (`192.168.0.65`)|✅ Done|
|Pi-hole DNS running|✅ Done|
|Local DNS records added|✅ Done|
|UFW firewall configured|✅ Done|
|Router pointing at Pi-hole|✅ Done|
|**node_exporter** (metrics agent)|⏳ Next|
|**Prometheus** (metrics collector)|⏳ Up next|
|**Grafana** (dashboards)|⏳ Up next|
|**Alertmanager** (notifications)|⏳ Up next|
|**Uptime Kuma** (service monitoring)|⏳ Up next|
|**Ansible** (automation control)|⏳ Up next|

# Prometheus + Grafana Install

## Checking Pi Architecture

command: `uname -m` = aarch64 = means 64-bit ARM
The architecture determines what we install
`wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-arm64.tar.gz`


Then we extract the files we donwloaded:
`tar xvf node_expoerter-1.8.2.linux-arm64.tar.gz`

tar xvf - unpacks a copmpress archive
- x - extract
- v - verbose (shows each file as it's extract)
- f - specifies the filename to extract 
![[Pasted image 20260328115757.png]]
![[Pasted image 20260328120230.png]]

## Creating a user 






