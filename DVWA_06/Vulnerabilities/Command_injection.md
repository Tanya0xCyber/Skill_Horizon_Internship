# Command Injection

## Overview

* **Command Injection** occurs when an application passes user input directly to the OS.
* Attackers can **run system commands**, potentially compromising the server.
* DVWA allows safe testing of this vulnerability in a lab environment.

---

## DVWA Security Levels Tested

| Level  | Observations                                                                   |
| ------ | ------------------------------------------------------------------------------ |
| Low    | Direct OS commands allowed → attacker can chain extra commands.                |
| Medium | Partial filtering → simple chaining blocked, but syntax tricks may still work. |
| High   | Strong filtering → command injection effectively prevented.                    |

---

## Step-by-Step Testing

### Low Security

* **Payload example:**

```bash
127.0.0.1 && dir
```

* **Result:** Executes normal command AND `dir`. **Low security allows full command injection**.
* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/cmd_low.png" width="80%">
</p>

---

### Medium Security

* **Payload example:**

```bash
127.0.0.1 & ping -n 2 127.0.0.1
```

* **Result:** Some system syntax tricks still work. **Partial protection**, but chaining commands may bypass filters.
* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/cmd_medium.png" width="80%">
</p>

---

### High Security

* **Payload:** N/A
* **Result:** DVWA **blocks command injection completely**. High level is effectively secure.
* **Screenshot :**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/cmd_high.png" width="80%">
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
