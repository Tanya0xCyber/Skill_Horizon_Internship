# Cross Site Scripting (XSS)

## Overview

* **XSS** allows attackers to inject scripts (usually JavaScript) into web pages.
* Scripts can **steal cookies, hijack sessions, or manipulate content**.
* Testing XSS in DVWA shows **how unvalidated input can be exploited safely**.

---

## DVWA Security Levels Tested

| Level  | Observations                                                                        |
| ------ | ----------------------------------------------------------------------------------- |
| Low    | Input not filtered → XSS works easily.                                              |
| Medium | Some filtering → simple scripts may be blocked.                                     |
| High   | Advanced filtering → `<script>` blocked, but HTML events can still execute scripts. |

---

## Step-by-Step Testing

### Security Level: Low

* **Module:** DVWA → XSS (Reflected) → Low Security
* **Payload:**

```html
<script>alert('XSS');</script>
```

* **Result:** Alert popup appears → Low security **does not filter scripts**, XSS successful.
* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/xss_low.png" width="80%">
</p>

---

### Security Level: Medium

* **Payload:**

```html
<script>alert('XSS');</script>
```

* **Result:**

  * Medium security **filters exact `<script>` tags** (case-sensitive).
  * Alert may not appear → shows **partial protection**.
* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/xss_medium.png" width="80%">
</p>

---

### Security Level: High

* **Payload (HTML event example):**

```html
<img src=x onmouseover=alert('XSS')>
```

* **Result:**

  * High security **blocks `<script>` tags**, but **HTML event attributes still execute scripts**.
  * Alert appears → High security reduces risk but does **not completely prevent XSS**.
* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/xss_high.png" width="80%">
</p>

---

## Impact Analysis

* Attackers could steal **cookies or session data**.
* Could redirect users to **malicious sites**.
* Could inject **defacing scripts** on the page.

---

## Remediation

* **Sanitize inputs** (remove or escape `<`, `>` and quotes).
* Use **Content Security Policy (CSP)** headers.
* Encode output before displaying user input.
* Avoid relying solely on `<script>` filtering; consider **all HTML events**.
