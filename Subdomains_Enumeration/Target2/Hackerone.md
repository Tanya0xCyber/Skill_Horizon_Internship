

# Subdomain Enumeration – hackerone.com

**Target:** Hackerone.com 
<br>

This is the **second target** in my Subdomain Enumeration task. I followed the same process as Target 1 (Subfinder → Assetfinder → AlterX → dnsx) but applied it to `hackerone.com`.

---

## 1. Subfinder

**Command Used:**

```bash
subfinder -d hackerone.com -o subfinder.txt
```

**Output File:**
[subfinder2.txt](https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target2/subfinder2.txt)

**Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target2/screenshots2/subfinder_target2.png" width="80%">
</p>

**Notes:**

* Discovered main subdomains like `api.hackerone.com`, `docs.hackerone.com`.
* This gave me the initial baseline for further enumeration.

---

## 2. Assetfinder

**Command Used:**

```bash
assetfinder --subs-only hackerone.com > assetfinder.txt
```

**Output File:**
[assetfinder2.txt](https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target2/assetfinder2.txt)

**Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target2/screenshots2/assetfinder_target2.png" width="80%">
</p>

**Notes:**

* Found extra subdomains missed by Subfinder.
* Helped expand the coverage before generating permutations.

---

## 3. AlterX + dnsx

**Commands Used:**

```bash
cat subfinder.txt assetfinder.txt | alterx -p '{{sub}}-{{word}}.{{suffix}}' -o alterx_permutations.txt
cat alterx_permutations.txt | dnsx -o live_subdomains.txt
```

**Output Files:**

* [alterx_permutations2.txt](https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target2/alterx_permutations2.txt)
* [live_subdomains.2txt](https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target2/live_subdomains2.txt)

**Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon/blob/main/Subdomains_Enumeration/Target2/screenshots2/alterx_target2.png" width="80%">
</p>

**Notes:**

* AlterX successfully generated permutations of discovered subdomains.
* However, dnsx did not find any of these permutations to be live.
* This is common in reconnaissance — it just means no extra valid subdomains were discovered through permutations for this target.

---

## Summary

* Combining three tools increased coverage of subdomains.
* dnsx filtered live subdomains → no new live subdomains found from permutations.
* The same methodology can be reused for any domain.

---



Would you like me to rewrite **Target 1** in **this exact style** (tool → output file → screenshot → notes) so that both targets match perfectly? This will make your repo look like a polished case study rather than just an assignment.
