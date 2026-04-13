# splunk

wget -O splunk-9.4.2-e9664af3d956-linux-amd64.deb "https://download.splunk.com/products/splunk/releases/9.4.2/linux/splunk-9.4.2-e9664af3d956-linux-amd64.deb"





# Splunk Enterprise All‑in‑One (Standalone) Install Guide

In an all‑in‑one (standalone) setup, a single server runs everything:

- Indexer  
- Search Head  
- Web UI  

This is ideal for testing, small environments, or development.

---

## Step 1 — Check System Requirements

Before installing, make sure your server meets at least these minimum specs:

| Requirement | Minimum                                    |
|------------|---------------------------------------------|
| OS         | 64‑bit Linux (Ubuntu, RHEL, CentOS, etc.)  |
| CPU        | 2 cores                                    |
| RAM        | 4 GB (8 GB+ recommended)                   |
| Disk       | 20 GB free                                 |
| Access     | Root or `sudo` privileges                  |

---

## Step 2 — Download Splunk Enterprise

Go to the official Splunk download page:

- https://www.splunk.com/en_us/download/splunk-enterprise.html

Pick the right installer for your Linux flavor:

| Package | Use For                    |
|---------|----------------------------|
| `.tgz`  | Any Linux (universal)      |
| `.rpm`  | RHEL, CentOS, Fedora       |
| `.deb`  | Ubuntu, Debian             |

Or download directly via terminal using `wget` (example):

```bash
# Example: download the .tgz installer (replace version and build as needed)
wget -O splunk.tgz 'https://download.splunk.com/products/splunk/releases/9.4.0/linux/splunk-9.4.0-<build>-Linux-x86_64.tgz'
```

> ⚠️ Always copy the exact latest URL from the Splunk download page — it changes with each release.

---

## Step 3 — Install Splunk

Choose the method that matches the package you downloaded.

### A) `.tgz` — Any Linux

```bash
tar -xvf splunk-*.tgz -C /opt
# This extracts Splunk to /opt/splunk
```

- `tar -xvf` → extract (`x`) verbosely (`v`) from file (`f`)  
- `-C /opt` → extract into the `/opt` directory

---

### B) `.rpm` — RHEL / CentOS / Fedora

```bash
sudo rpm -i splunk-*.rpm
# RPM package manager installs Splunk to /opt/splunk automatically
```

---

### C) `.deb` — Ubuntu / Debian

```bash
sudo dpkg -i splunk-*.deb
# Debian package manager installs Splunk to /opt/splunk automatically
```

---

## Step 4 — Start Splunk for the First Time

```bash
cd /opt/splunk/bin
sudo ./splunk start --accept-license
```

- `--accept-license` → automatically accepts the Splunk Enterprise License Agreement so you're not prompted to type `y`.
- During first start, you’ll be asked to create an **admin username and password** — you’ll use these to log in to the web UI.

---

## Step 5 — Enable Auto‑Start at Boot (Recommended)

```bash
sudo /opt/splunk/bin/splunk enable boot-start
```

This registers Splunk as a system service so it automatically starts when the server reboots.

---

## Step 6 — Open Firewall Port 8000

Port `8000` is Splunk’s default web UI port. Open it if you will access Splunk from another machine.

```bash
# For firewalld (RHEL/CentOS)
sudo firewall-cmd --permanent --add-port=8000/tcp
sudo firewall-cmd --reload

# For ufw (Ubuntu)
sudo ufw allow 8000/tcp
```

---

## Step 7 — Access the Splunk Web UI

Open a browser and go to:

```text
http://<your-server-ip>:8000
```

Log in with the **admin** credentials you created in Step 4. 🎉

---

## Basic Start/Stop Commands

```bash
sudo /opt/splunk/bin/splunk start    # Start Splunk
sudo /opt/splunk/bin/splunk stop     # Stop Splunk
sudo /opt/splunk/bin/splunk restart  # Restart Splunk
sudo /opt/splunk/bin/splunk status   # Check status
```
