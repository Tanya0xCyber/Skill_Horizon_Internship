# Command Injection

## Overview

* **Command Injection** occurs when an application passes user input directly to the OS.
* Attackers can **run system commands**, potentially compromising the server.
* DVWA allows safe testing of this vulnerability in a lab environment.

---



### Low Security

* **Payload example:**

```bash
127.0.0.1 && dir
```

* **Result:** Executes normal command AND `dir`. **Low security allows full command injection**.
* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/commmand_injection_low.png" width="80%">
</p>

---



## Impact Analysis

* Attackers could **execute arbitrary system commands**.
* Could **access sensitive files, modify data, or compromise the server**.

---

## Remediation

* **Validate and sanitize all inputs**.
* Avoid executing **direct OS commands** with user input.
* Use **whitelists or safe APIs** when system commands are necessary.
