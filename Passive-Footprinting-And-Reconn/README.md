#  Passive Footprinting & Reconnaissance

##  Objective
Learn how to gather **publicly available information** about a target without actively engaging with its systems. This helps understand the initial phase of penetration testing and ethical hacking — what an attacker can know about your system before even touching it.

---

## Folder & File Structure
Organize your repository like this so anyone can follow easily:

```
Passive-Footprinting-And-Recon/
├── README.md              # Main Report for this target
├── outputs/               # Raw outputs of commands
│   ├── whois.txt
│   ├── dig.txt
│   ├── nslookup.txt
│   ├── final_subdomains.txt
│   ├── dorks.txt
│   ├── emails.txt
│   ├── urls.txt
│   ├── jsfiles.txt
│   └── metadata.txt
└── screenshots/           # Screenshots of each step
    ├── 01_domaininfo.png
    ├── 02_subs.png
    ├── 03_emails.png
    ├── 04_metadata.png
    ├── 05_dorking.png
    └── 06_urls_js.png
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

## 1️⃣ Domain & DNS Information


### **WHOIS**

**Brief Overview:**
This step collects fundamental domain and DNS information of the target. By gathering registrar details, DNS records, and IP addresses, we create a foundational understanding of how the domain is hosted, its mail setup, and its network footprint.

**What it does :**
Retrieves the domain registration details such as registrar, creation/expiry date, owner contact info, and name servers.**

**Command 1:**
```bash
whois yahoo.com > whois.txt
```

**Output file:**
[whois.txt](https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Passive-Footprinting-And-Reconn/Outputs/whois.txt)– contains all the WHOIS information for `yahoo.com`.

**Screenshot:**
<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Passive-Footprinting-And-Reconn/Screenshots/whois.png" width="80%">
</p>

**Notes**
 * Domain registered by Yahoo Assets LLC (US) using MarkMonitor.
 * First registered on 1995-01-18, last updated on 2024-12-18.
 * Domain security protections are enabled (transfer/update/delete prohibited).
 * DNS hosted on ns1-5.yahoo.com.
 * DNSSEC not enabled, which could be considered a small security gap.
---

### **DIG**

**What it does :**
Queries the DNS records of `yahoo.com`, including A, MX, NS, TXT, and other records. Gives a snapshot of how the domain is configured.

**Command 2:**
```bash
dig yahoo.com ANY @8.8.8.8 > dig.txt
```

**Output file:**
[dig.txt](https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Passive-Footprinting-And-Reconn/Outputs/dig.txt) – contains summarized DNS records.

**Screenshot:**
<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Passive-Footprinting-And-Reconn/Screenshots/dig.png" width="80%">
</p>

**Notes**
 * Yahoo has many name servers → means high reliability.
 * We got IP addresses (A + AAAA records) → tells where yahoo.com is hosted.
 * We found mail servers (MX) → shows how Yahoo handles email.
 * TXT records → have security settings (SPF, Google/Facebook verification).
 * CAA records → only certain companies can give SSL certificates (secure).

---

### ** NSLOOKUP**

**What it does :**
Finds the IP address of the domain and the DNS server being used. Useful to verify how the domain resolves to an IP.

**Command 3:**
```bash
nslookup yahoo.com > nslookup.txt
```

**Output file:**
 [nslookup.txt](https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Passive-Footprinting-And-Reconn/Outputs/dig.txt)contains the IP address and DNS server info for `yahoo.com`.

**Screenshot:**
<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/Passive-Footprinting-And-Reconn/Screenshots/nslookup.png" width="80%">
</p>

**Notes:**
 * Server: 192.168.153.2 → This is the DNS server your system asked for info.
 * Non-authoritative answer: Data came from a cache, not directly from Yahoo’s main DNS.   
   Addresses:
     * IPv4: (74.6.231.21, 74.6.143.25, etc.) → These are Yahoo’s public IPs.
     * IPv6: (2001:4998:...) → Same but for IPv6 network.
---

### 2.. Subdomain Enumeration
**Commands:**
```bash
subfinder -d yahoo.com -o outputs/final_subdomains.txt
assetfinder yahoo.com >> outputs/final_subdomains.txt
amass enum -passive -d yahoo.com >> outputs/final_subdomains.txt
```
**Explanation:** Lists publicly visible subdomains. These may reveal staging sites, APIs, or forgotten assets.

 Screenshot: `screenshots/02_subs.png`

---

### 3️.. Email & Employee Information
**Command:**
```bash
theHarvester -d yahoo.com -b google > outputs/emails.txt
```
**Explanation:** Finds public email addresses and employee data that could be exploited in phishing or social engineering.

 Screenshot: `screenshots/03_emails.png`

---

### 4️.. Metadata Extraction
**Commands:**
```bash
metagoofil -d yahoo.com -t pdf,doc,xls,ppt -l 50 -n 10 -o ./outputs -f outputs/metadata.txt
exiftool sample.pdf >> outputs/metadata.txt
```
**Explanation:** Extracts metadata (author names, software versions) from public files which can reveal tech stack or internal usernames.

 Screenshot: `screenshots/04_metadata.png`

---
### 5️.. Google Dorking
**Queries Tried:**
```
site:yahoo.com filetype:pdf
site:yahoo.com inurl:admin
site:yahoo.com intitle:index of
```
**Explanation:** Searches for exposed files, directories, admin portals, and sensitive data indexed by Google.

 Screenshot: `screenshots/05_dorking.png`

---

### 6️.. URLs & JS Files
**Commands:**
```bash
gau yahoo.com > outputs/urls.txt
cat outputs/urls.txt | grep "\.js" > outputs/jsfiles.txt
```
**Explanation:** Collects URLs from web archives and filters JavaScript files which might contain API endpoints or secrets.

 Screenshot: `screenshots/06_urls_js.png`

---

### 7️.. Social Media & OSINT (Optional)
**Tools:** Maltego CE / SpiderFoot
**Explanation:** Maps organization’s public presence (LinkedIn employees, Twitter accounts, GitHub repos).

---

### 8️..  Secret Search in JS (Optional)
**Tool:** JSLeak
```bash
jsleak -f outputs/jsfiles.txt -o outputs/jsleak.txt
```
**Explanation:** Automatically searches JS files for API keys, tokens, or passwords.

---

##  Summary
This exercise shows how much information is available about a target without performing any hacking.

- **Subdomains** may reveal staging servers
- **Emails** could be used for phishing
- **Metadata** reveals tech stack and users
- **URLs & JS files** might expose API endpoints
- **Google dorks** find hidden files or directories

**Key Takeaway:** Passive recon is a safe, legal, and essential first step in VAPT — it helps attackers plan and defenders fix leaks.

---

## ⚠️ Responsible Disclosure
Redact any sensitive information (like API keys, employee PII) before publishing results publicly.
