# Subdomain Enumeration - testphp.vulnweb.com

This task is part of my Skill Horizon project, where I document my daily cybersecurity assignments.
The goal of this assignment was to find and list all possible subdomains of the target domain testphp.vulnweb.com using three different tools and then filter which ones are live.

Target: Testphp.vulnweb.com <br>
Date: 06-Sep-2025 <br>
Tools Used:

* Subfinder → for collecting real subdomains

* AlterX → for generating possible permutations of subdomains

* Assetfinder → Finds additional subdomains

---

## 1. Subfinder

**Purpose:**  
Finds real, publicly available subdomains of the target.

**Command Used:**  
```bash
subfinder -d testphp.vulnweb.com -o subfinder.txt
```

**Output File:**
[subfinder.txt](https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target1/subfinder.txt)

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
Finds more subdomains using different sources for better coverage.

**Command Used:**

```bash
assetfinder --subs-only testphp.vulnweb.com > assetfinder.txt
```

**Output File:**
  [assetfinder.txt](https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target1/assetfinder.txt)

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
AlterX generates possible permutations of discovered subdomains, and DNSX checks which of them are live.

**Command Used:**

```bash
cat subfinder.txt assetfinder.txt | alterx -p '{{sub}}-{{word}}.{{suffix}}' -o alterx_permutations.txt
```

**Output File:**
[permutations.txt](https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target1/permutations.txt) <br>

[live_subdomains.txt](https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target1/live_subdomains.txt)

** Verification (dnsx):**

```cat alterx_permutations.txt | dnsx -o live_subdomains.txt```

**Screenshot:**
<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target1/screenshots/alterx_target1.png" width="80%">
</p>


**Notes:**

* AlterX guessed additional subdomains like blog-dev.testphp.vulnweb.com.
* DNSX confirmed which guessed subdomains are actually active.

---

## 4. Summary

* Tools Used: Subfinder (real subdomains), Assetfinder (extra subdomains), AlterX (permutations), DNSX (live check).

* Output:

    * subfinder.txt + assetfinder.txt → initial list of subdomains.

    * alterx_permutations.txt → generated permutations.

    * live_subdomains.txt → final verified list of live subdomains.

* Key Takeaway: Enumeration + permutation + validation = complete picture of the attack surface.
