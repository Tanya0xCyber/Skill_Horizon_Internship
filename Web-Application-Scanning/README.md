# Web Application Scanning — Automated Vulnerability Discovery (testphp.vulnweb.com)

## Overview

This project demonstrates **safe and legal automated vulnerability scanning** of `testphp.vulnweb.com`.
The goal is to identify open ports, services, technologies, potential misconfigurations, and security risks using **automated scanners** (light → aggressive) and generate a professional report.

## Tools Used

Nmap · WhatWeb · Dirb · Nikto · Nuclei · OWASP ZAP (Docker) · WPScan (not used, no WP detected)

---

## Step 1: Recon & Discovery

### 1.1 Host Discovery , ports and services : 

```bash
nmap -T4 --top-parts  1000 -sV testphp.vulnweb.com -oN nmap.txt
```

**Finding:** Host is alive → Target reachable (IP detected).
* Open Ports: **80 (HTTP)**
* Web Server: **Apache/2.2.8 (Ubuntu)**
* PHP Version: **5.2.4-2ubuntu5.10**

**Screenshot:**

<p align="center"><img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Web-Application-Scanning/Screenshots/nmap.png" width="80%"></p>

---

### 1.2 Web Fingerprinting

```bash
whatweb http://testphp.vulnweb.com
```

**Finding:**

* Server: Apache/2.2.8
* Powered by PHP 5.2.4
* OS: Ubuntu Linux

**Screenshot:**

<p align="center"><img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Web-Application-Scanning/Screenshots/whatweb_testphp.png" width="80%"></p>

---

### 1.3 Directory Discovery

```bash
dirb http://testphp.vulnweb.com /usr/share/wordlists/dirb/small.txt -o dirb.txt
```

**Key Findings:** Found multiple interesting directories (e.g., `/images/`, `/uploads/`, `/admin/`) that could be explored later for sensitive files.

**Screenshot:**

<p align="center"><img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Web-Application-Scanning/Screenshots/dirb_testphp.png" width="80%"></p>

---

## Step 2: Light Automated Scans

### 2.1 Nikto — Web Vulnerability Scan

```bash
nikto -h http://testphp.vulnweb.com -output nikto.txt
```

**Key Findings:**

* Missing security headers (X-Frame-Options, X-Content-Type-Options)
* Possible directory indexing
* Outdated Apache version → potential CVEs

**Screenshot:**

<p align="center"><img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Web-Application-Scanning/Screenshots/nikto_testphp.png" width="80%"></p>

---

### 2.2 Nuclei — Template-based Checks

```bash
nuclei -u http://testphp.vulnweb.com -as -o nuclei.txt -c 10
```

**Finding:** Detected several low- to medium-severity issues such as missing headers and common misconfigurations.

**Screenshot:**

<p align="center"><img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Web-Application-Scanning/Screenshots/nuclei_testphp.png" width="80%"></p>

---

### 2.3 OWASP ZAP (Baseline Scan)

```bash
sudo docker run -v $(pwd):/zap/wrk/:rw --network="host" ghcr.io/zaproxy/zaproxy:stable zap-baseline.py -t http://testphp.vulnweb.com -r zap_baseline.html
```

**Key Findings:**

* **14 warnings**, including:

  * Missing anti-clickjacking, CSP, X-Content-Type-Options headers
  * Information leak via `Server` & `X-Powered-By` headers
  * Potential XSS in `guestbook.php` & `search.php`
  * Absence of anti-CSRF tokens on key pages

**Screenshot:**

<p align="center"><img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Web-Application-Scanning/Screenshots/owasp_1.png" width="80%"></p>

---

### 2.4 WPScan — WordPress Check

```bash
wpscan --url http://testphp.vulnweb.com
```

**Output Summary:**

*  Target reachable
*  No WordPress detected → Skipped plugin/theme/user enumeration

**Screenshot:**

<p align="center"><img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Web-Application-Scanning/Screenshots/wpscan_testphp.png" width="80%"></p>

---

## Conclusion :

From this project:

* **Target is live** and running **Apache/2.2.8 with PHP 5.2.4** (outdated → risk).
* **Key issues found:**

  * Missing security headers (CSP, X-Frame-Options, HSTS)
  * Potential XSS in input fields
  * Server information disclosure (`Server`, `X-Powered-By`)
  * No anti-CSRF protections on sensitive forms
* **No WordPress detected**, so WP-specific attacks are not applicable.

**Takeaway:**
This scanning process maps the attack surface, identifies misconfigurations, and highlights priority fixes (e.g., apply latest Apache/PHP patches, implement security headers, validate input to prevent XSS).



