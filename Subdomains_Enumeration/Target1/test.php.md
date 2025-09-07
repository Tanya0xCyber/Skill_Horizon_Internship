# Subdomain Enumeration - testphp.vulnweb.com

This task is part of my Skill Horizon project, where I document my daily cybersecurity assignments.
The goal of this assignment was to find and list all possible subdomains of the target domain testphp.vulnweb.com using three different tools and then filter which ones are live.

Target: testphp.vulnweb.com
Date: 06-Sep-2025
Tools Used:

* Subfinder → for collecting real subdomains

* AlterX → for generating possible permutations of subdomains

* Assetfinder → Finds additional subdomains

---

## 1. Subfinder

**Purpose:**  
Subfinder automatically finds **real subdomains** of a domain. Think of it as a detective looking for addresses that actually exist.

**Command Used:**  
```bash
subfinder -d testphp.vulnweb.com -o subfinder.txt
```

**Output File:**
[subfinder.txt](Subdomains_Enumeration/Target1/subfinder.txt)

**Screenshot:**
<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target1/screenshots/subfinder_target1.png" width="80%">
</p>


**Notes:**

* Found initial subdomains like `www.testphp.vulnweb.com`, `blog.testphp.vulnweb.com`.
* Provides a baseline list of subdomains for further enumeration.

---

## 2. Assetfinder

**Purpose:**
Assetfinder finds **additional subdomains** using different sources than Subfinder. Think of it as another detective with a different notebook, adding more addresses that might be missed.

**Command Used:**

```bash
assetfinder --subs-only testphp.vulnweb.com > assetfinder.txt
```

**Output File:**
  [assetfinder.txt](Subdomains_Enumeration/Target1/assetfinder.txt)

**Screenshot:**
<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target1/screenshots/assetfinder_target1.png" width="80%">
</p>


**Notes:**

* Adds extra subdomains missed by Subfinder.
* Ensures a more comprehensive enumeration of the target.

---

## 3. AlterX

**Purpose:**
AlterX generates **possible subdomain permutations** based on the existing subdomains. Example: if you found `blog.testphp.vulnweb.com`, AlterX may guess `blog-dev.testphp.vulnweb.com` or `blog-test.testphp.vulnweb.com`. Think of it as a creative friend imagining other possible addresses.

**Command Used:**

```bash
cat subfinder.txt assetfinder.txt | alterx -p '{{sub}}-{{word}}.{{suffix}}' -o alterx_permutations.txt
```

**Output File:**
[permutations.txt](Subdomains_Enumeration/Target1/permutations.txt)
[live_subdomains.txt](Subdomains_Enumeration/Target1/live_subdomains.txt)

**Screenshot:**
<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target1/screenshots/alterx_target1.png" width="80%">
</p>


**Notes:**

* Creates new subdomain guesses.
* Useful to discover subdomains that are not publicly listed but may exist.

---

## 4. Summary

* Subdomains collected using **3 different tools**: Subfinder, Assetfinder, AlterX.
* Subfinder & Assetfinder → initial subdomains.
* AlterX → additional guessed subdomains.
* Total subdomains collected: Count lines from all files after removing duplicates.
* Optional Next Step: You can check which subdomains are active/live using DNS checking tools.

