# File Upload

## Overview

* **File Upload Vulnerabilities** occur when applications let users upload files without proper checks.
* Attackers can upload **malicious scripts** (e.g., PHP shells) to gain control of the server.
* DVWA allows safe testing of this issue at different security levels.

---

## DVWA Security Levels Tested

| Level  | Observations                                                                           |
| ------ | -------------------------------------------------------------------------------------- |
| Low    | No checks → any file (e.g., PHP shell) can be uploaded and executed.                   |
| Medium | Relies on file extension/type reported by client → can be bypassed (e.g., `.php.png`). |
| High   | Strict checks → only valid images accepted. Execution of scripts prevented.            |

---

## Step-by-Step Testing

### Low Security

* **Payload example:** Upload `shell.php` containing simple PHP code.
* **Result:** File is accepted and can be accessed in the uploads folder → code execution possible.
* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/file_upload_low.png" width="80%">
</p>

---

### Medium Security

* **Payload example:** Rename file to `shell.php.png`.
* **Result:** DVWA message shows file uploaded (`hackable/uploads/test.php.png`), but:

  * File may not be accessible via browser (404).
  * Even if stored, `.php.png` is treated as an image, not executed as PHP.
* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/file_upload_medium.png" width="80%">
</p>

---

### High Security

* **Payload:** `shell.php.png` (same as Medium).
* **Result:** Upload blocked with error → “Only JPEG or PNG images allowed.”
* **Screenshot:**

<p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/file_upload_high.png" width="80%">
</p>

---

## Impact Analysis

* Attackers could upload **malicious scripts** and gain remote access.
* Could lead to **defacement, data theft, or complete server compromise**.

---

## Remediation

* Allow only **specific file types** and validate both extension and content.
* Store uploads **outside the webroot**.
* Rename files on upload to prevent execution.
* Use libraries to safely handle uploaded files (e.g., image processing tools).

---
