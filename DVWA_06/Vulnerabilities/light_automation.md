# Light Automation


---

## 1) WhatWeb — fingerprinting
```bash
whatweb http://127.0.0.1:42001/dvwa
````

* **Result:** `301` → redirect to trailing-slash; `/dvwa/` returns `403 Forbidden`; Server: `nginx/1.26.3`.

* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/whatweb_dvwa.png" width="80%">
</p>

---

## 2) Dirb — directory discovery

```bash
dirb http://127.0.0.1:42001/dvwa /usr/share/wordlists/dirb/common.txt -o dirb-dvwa.txt
```

* **Result:** Found `/css/`, `/images/`, `/includes/`, `/js/`. No sensitive files with `common.txt`.

* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/dirb_dvwa.png" width="80%">
</p>

---

## 3) Nuclei — template-based quick scan

```bash
nuclei -u http://127.0.0.1/dvwa -o nuclei-dvwa.txt
```

* **Result:** Templates updated (v10.2.9). ~8297 templates executed. **No results found.**

* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/nuclei_dvwa.png" width="80%">
</p>

---

## 4) Nikto — webserver misconfiguration scan

```bash
sudo nikto -host http://127.0.0.1:42001/dvwa -output nikto-dvwa.txt
```

* **Result:** Server: `nginx/1.26.3`. Missing headers on `/dvwa/`: `X-Frame-Options` and `X-Content-Type-Options`.

* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/nikto_dvwa.png" width="80%">
</p>


