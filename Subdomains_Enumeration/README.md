# Subdomain Enumeration 

This folder is all about finding **hidden subdomains** of target websites — a common first step in bug bounty and pentesting.  
I used a mix of tools to collect subdomains, generate new ones, and check which ones are actually alive.

---

## What's Inside

- **Target 1** → testphp.vulnweb.com (Practice target)
- **Target 2** → zero.webappsecurity.com (Practice target)

Each target folder has:
- My commands & output files
- Screenshots of results
- Final list of live subdomains

---

## Tools I Used

- **Subfinder** → Finds real subdomains
- **Assetfinder** → Adds extra subdomains
- **AlterX** → Creates permutations/guesses
- **dnsx** → Filters only live ones

---

##  What I Learned

- Using multiple tools gives better coverage.
- dnsx helps focus only on the **active subdomains**.
- This process is reusable for any future domain I test.

---
