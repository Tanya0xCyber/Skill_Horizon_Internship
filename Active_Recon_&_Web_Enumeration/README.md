
# Active Recon & Web Enumeration — ZeroBank (zero.webappsecurity.com)

## Overview
This project performs **active reconnaissance** on `zero.webappsecurity.com`.  
The goal was to identify if the target is alive, find open ports, detect running services, discover hidden directories, perform basic web fingerprinting, and identify possible misconfigurations using non-exploitative tools.

## Tools Used
- **Nmap** – Host discovery, port & service scan, OS detection  
- **Dirb/Gobuster** – Directory brute-forcing  
- **WhatWeb** – Web technology fingerprinting  
- **Nikto** – Web vulnerability scanning  
- **Kali Linux** – Operating system used for testing  

---

## Step 1: Host Discovery

### Command:
```bash
nmap -sn zero.webappsecurity.com 
````

**What it does :**
Checks if the target is alive using ping/ARP (no port scan).

**Result:** Host is alive.
**Screenshot:**

<p align="center">
  <img src="" width="80%">
</p>

---

## Step 2: Port & Service Scan

### 2.1 TCP SYN Scan (Quick)

```bash
nmap -sS zero.webappsecurity.com 
```

Finds open TCP ports quickly using SYN packets.
**Screenshot:**

<p align="center">
  <img src="" width="80%">
</p>

---

### 2.2 Service & Version Detection (Common Ports)

```bash
nmap -sV -p 22,80,443 -sC zero.webappsecurity.com 
```

Detects services, versions, and runs default NSE scripts on 22, 80, 443.
**Screenshot:**

<p align="center">
  <img src="" width="80%">
</p>

---

### 2.3 Full Port Scan

```bash
nmap -sV -p- zero.webappsecurity.com -oN scans/full_port_scan.txt
```

Scans **all 65535 ports** to ensure nothing is missed.
**Screenshot:**

<p align="center">
  <img src="" width="80%">
</p>

---

### 2.4 OS Detection

```bash
nmap -O --osscan-guess zero.webappsecurity.com -oN scans/os_detection.txt
```

Tries to guess operating system of the host.
**Screenshot:**

<p align="center">
  <img src="screenshots/os_detection.png" width="80%">
</p>

---

## Step 3: HTTP Enumeration (Directory Brute Force)

### Command:

```bash
dirb https://zero.webappsecurity.com /usr/share/wordlists/dirb/common.txt -o scans/gobuster_dirs.txt
```

**What it does :**
Brute-forces common hidden directories and files.

**Interesting Directories Found:**

* `/login.html`
* `/bank/`
* `/forgot-password.html`

**Screenshot:**

<p align="center">
  <img src="screenshots/gobuster.png" width="80%">
</p>

---

## Step 4: Web Fingerprinting & Vulnerability Scanning

### 4.1 WhatWeb

```bash
whatweb https://zero.webappsecurity.com > scans/whatweb.txt
```

Identifies web technologies (server, framework, CMS, language).
**Screenshot:**

<p align="center">
  <img src="" width="80%">
</p>

---

### 4.2 Nikto

```bash
nikto -h https://zero.webappsecurity.com -o scans/nikto_results.txt
```

Finds common misconfigurations and security headers issues.

**Screenshot:**

<p align="center">
  <img src="screenshots/nikto.png" width="80%">
</p>

---

## Conclusion

Through this assessment, I successfully:

* Confirmed that the target is alive.
* Found open ports (22, 80, 443).
* Identified the web server and possible OS.
* Discovered multiple directories like `/bank`, `/login.html`.
* Learned about missing security headers and potential risks.

This report can help security teams prioritize hardening web server configuration and securing sensitive endpoints.

---

## Deliverables

* Raw scan outputs are stored in `/scans`
* Screenshots are stored in `/screenshots`
* Final summarized report is available at `/reports/final_report.md`

```

