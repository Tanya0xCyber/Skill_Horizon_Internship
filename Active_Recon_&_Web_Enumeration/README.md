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

**Finding:**  Host is alive → Target is reachable (IP: 54.82.22.214).

**Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Active_Recon_%26_Web_Enumeration/Screenshots/host_discovery.png" width="80%">
</p>

---

## Step 2: Port & Service Scan

### 2.1 TCP SYN Scan (Quick)

```bash
nmap -sS zero.webappsecurity.com 
```

Finds open TCP ports quickly using SYN packets.

**Key Findings:**
   * Open Ports: 80 (HTTP), 443 (HTTPS), 8080 (HTTP-Proxy)

**Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Active_Recon_%26_Web_Enumeration/Screenshots/TCP_syn_scan.png" width="80%">
</p>

---

### 2.2 Service & Version Detection (Common Ports)

```bash
nmap -sV -p 22,80,443 -sC zero.webappsecurity.com 
```

Detects services, versions, and runs default NSE scripts on 22, 80, 443.
**Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Active_Recon_%26_Web_Enumeration/Screenshots/service_version_scan.png" width="80%">
</p>

**Key Findings:**
   * Web Server: Apache/2.2.6 (Win32)
   * OpenSSL Version: 0.9.8e (Outdated – potential exploit path)
   * Shows SSL Certificate details & server headers.

---

### 2.3 Full Port Scan

```bash
nmap -sV -p- zero.webappsecurity.com -oN scans/full_port_scan.txt
```

Scans **all 65535 ports** to ensure nothing is missed.
**Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Active_Recon_%26_Web_Enumeration/Screenshots/service_version_scan.png" width="80%">
</p>

**Key Findings:**
   * Confirmed only 80, 443, 8080 are open.
   * No additional high-risk open ports found.
     
---

### 2.4 OS Detection

```bash
nmap -O --osscan-guess zero.webappsecurity.com -oN scans/os_detection.txt
```

Tries to guess operating system of the host.
**Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Active_Recon_%26_Web_Enumeration/Screenshots/os_scan.png" width="80%">
</p>

**Key Findings:**
   * OS Guess: Windows 7 / Windows Server 2008 (Win32)
   * Useful for choosing correct exploits & payloads later.
     

---

## Step 3: HTTP Enumeration (Directory Brute Force)

### Command:

```bash
dirb https://zero.webappsecurity.com /usr/share/wordlists/dirb/small.txt -o scans/gobuster_dirb.txt
```

**What it does :**
Brute-forces common hidden directories and files.
**Key Findings:**
   * /cgi-bin/ — Exists (403 Forbidden). This directory may contain server-side scripts (CGI programs).
   * /con — Exists (403 Forbidden). Access is restricted.
   * Even though access is denied (403), this still reveals potential attack surface for later testing.


**Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Active_Recon_%26_Web_Enumeration/Screenshots/dirb.png" width="80%">
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
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Active_Recon_%26_Web_Enumeration/Screenshots/whatweb.png" width="80%">
</p>

**Key Findings:**
    * Web Server: Apache/2.2.6 (Win32)
    * Modules: mod_ssl/2.2.6, mod_jk/1.2.40
    * OpenSSL Version: 0.9.8e (outdated)
    * OS: Windows (32-bit)
This information helps in identifying potential exploits for outdated versions.

---

### 4.2 Nikto

```bash
nikto -h https://zero.webappsecurity.com -o scans/nikto_results.txt
```

Finds common misconfigurations and security headers issues.

**Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Active_Recon_%26_Web_Enumeration/Screenshots/nikto_result.png" width="80%">
</p>

**Key Findings:**

   * ETag leaks file info → helps attackers fingerprint files
   * No X-Frame-Options → site vulnerable to clickjacking
   * No HSTS → HTTPS can be downgraded (less secure)
   * No X-Content-Type-Options → browser may misread files (possible XSS)

---

## Conclusion / Summary

From this reconnaissance, I discovered:

* Target is alive and hosted on AWS.
* Open ports: **80, 443, 8080** — main web entry points.
* Running **Apache/2.2.6 (Win32)** with outdated **OpenSSL 0.9.8e** — possible vulnerabilities.
* OS seems to be Windows 7 / 2008 Server — helps in choosing payloads for exploitation.
* Discovered `/cgi-bin/` and `/con` directories — useful for manual testing later.
* Security misconfigurations found: missing headers (X-Frame-Options, HSTS, X-Content-Type-Options) → risk of clickjacking, HTTPS downgrade, and XSS.

**Takeaway:**
This recon gives a clear picture of attack surface (ports, services, directories, vulnerabilities). These findings can guide penetration testing & exploitation in next phases.
