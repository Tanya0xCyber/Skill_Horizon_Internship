# Web Application Scanning – Automated Vulnerability Discovery

##  Objective
Perform safe, legal vulnerability scanning...

##  Lab Setup
**Target:** testphp.vulnweb.com  
**Tools Used:** Nmap, WhatWeb, Dirb, Nikto, Nuclei, OWASP ZAP, WPScan  

##  Step 1: Recon & Discovery
- **Nmap Results:** (attach file/screenshot)
- **Technologies Detected:** PHP, Apache, MySQL
- **Directories Found:** /admin, /uploads

##  Step 2: Light Automated Scan
### Nikto Findings
- Outdated Apache version
- Missing X-Frame-Options header

### Nuclei Findings
- Possible XSS in `/search.php` parameter

### ZAP Baseline Report
- (attach report link or screenshot)

##  False Positives Removed
- XSS flagged in Nuclei was not reproducible.

##  Remediation Recommendations
- Upgrade Apache to latest version
- Add `X-Frame-Options: SAMEORIGIN` header

##  Conclusion
- Automated scans completed successfully
- Application has medium-risk misconfigurations
