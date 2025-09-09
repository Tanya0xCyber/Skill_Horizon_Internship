#  Passive Footprinting & Reconnaissance

##  Objective
Learn how to gather **publicly available information** about a target without actively engaging with its systems. This helps understand the initial phase of penetration testing and ethical hacking — what an attacker can know about your system before even touching it.

---

## Folder & File Structure
Organize your repository like this so anyone can follow easily:

```
Passive-Footprinting-And-Recon/
├── README.md         # Main Report for this target
├── 01.Domain_Information_gathering.md
├── 02.Subdomains_enumeration.md
├── 03.Email_And_Emloyee_Info.md
├── 04.Metadata_Extraction.md
├── 05.Google_dorking.md
├── 06.Social_media_&_OSINT.md
├── 07.Collect_URLs_&_Filter_JS_File.md
├── outputs/               # Raw outputs of commands
│   ├── whois.txt
│   ├── dig.txt
│   ├── nslookup.txt
│   ├── final_subdomains.txt
│   ├── dorks.txt
│   ├── emails.txt
│   ├── urls.txt
│   ├── jsfiles.txt
│   └── metadata.txt ....
└── screenshots/           # Screenshots of each step
    ├── 01_domaininfo.png
    ├── 02_subs.png
    ├── 03_emails.png
    ├── 04_metadata.png
    ├── 05_dorking.png
    └── 06_urls_js.png ....
```

---

##  Tools Used
- `whois`, `dig`, `nslookup` → Domain & DNS details
- `subfinder`, `assetfinder`, `amass` (passive) → Subdomain enumeration
- `theHarvester` → Public email & employee info
- `metagoofil`, `exiftool` → Metadata extraction from public documents
- `Google Dorking` → Search engine-based reconnaissance
- `gau`, `katana`, `linkfinder` → Collect URLs & JS files
- `JSLeak` → Search secrets in JS files
- `Maltego (CE)` / `SpiderFoot` → OSINT automation (optional)



---

##**Steps Performed:**

## 1. Domain Information Gathering
**Commands:**
```bash
whois yahoo.com > whois.txt
dig yahoo.com  > dig.txt
nslookup yahoo.com > nslookup.txt
```
Explanation: Collected domain registrar, DNS records, and IP addresses.

### 2.. Subdomain Enumeration
**Commands:**
```bash
subfinder -d yahoo.com -o subfinder_yahoo.txt
assetfinder yahoo.com > assetfinder_yahoo.txt
amass enum -passive -d yahoo.com > amass_yahoo.txt
```
**Explanation:** Lists publicly visible subdomains. These may reveal staging sites, APIs, or forgotten assets.

 ---

### 3️3.. Email & Employee Information
**Command:**
```bash
theHarvester -d yahoo.com -b google,bing,linkdln > yahoo_emails.txt
```
**Explanation:** Finds public email addresses and employee data that could be exploited in phishing or social engineering.

 

---

### 4️4.. Metadata Extraction
**Commands:**
```bash

exiftool sample.pdf >> outputs/metadata.txt
```
**Explanation:** Extracts metadata (author names, software versions) from public files which can reveal tech stack or internal usernames.

 Screenshot: `screenshots/04_metadata.png`

---
### 5️5.. Google Dorking
**Queries Tried:**
```
site:yahoo.com filetype:pdf
site:yahoo.com inurl:admin
site:yahoo.com intitle:index of
```
**Explanation:** Searches for exposed files, directories, admin portals, and sensitive data indexed by Google.

---

### 6.. Social Media & OSINT 
**Tools:** Maltego CE / SpiderFoot
**Explanation:** Maps organization’s public presence (LinkedIn employees, Twitter accounts, GitHub repos).

---

### 7..7️URLs & JS Files
**Commands:**
```bash
gau yahoo.com > yahoo_urls.txt
cat yahoo_urls.txt | grep "\.js" > yahoo_jsfiles.txt
jsleak yahoo_jsfiles.txt -o yahoo_jsleak.txt
```
**Explanation:** Collects URLs from web archives and filters JavaScript files which might contain API endpoints or secrets.

---


##**Conclusion: Possible Attack Surfaces Identified:**

Passive reconnaissance of yahoo.com revealed:

* Subdomains & URLs: Few active subdomains like 2013-en-imagenes.es.yahoo.com, admin.nevec.yahoo.com, admanager.yahoo.com — potential public-facing areas.
* Domain & DNS Info: Multiple name servers (ns1-5.yahoo.com), IPv4/IPv6 addresses, MX and TXT/CAA records confirm hosting and security setup.
* Emails / Employee Info: No public employee emails found; document metadata shows company authorship and software used, with no sensitive paths.
* OSINT / Public Profiles: Minimal exposure with 4 LinkedIn profiles and 2 GitHub repos.

Key Takeaway: Even with limited findings, passive recon highlights publicly visible assets while showing a strong security posture with minimal exposed sensitive data.

---
