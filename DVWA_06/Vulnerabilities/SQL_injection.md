# SQL Injection (SQLi)

## Overview
SQL Injection is a vulnerability where an attacker can manipulate database queries through user inputs to access, modify, or delete data they shouldn't.  
It is critical because it can lead to **data breaches, unauthorized access, and database compromise**.

## DVWA Security Levels Tested
| Level  | Key Observations |
|--------|----------------|
| Low    | No input protection; SQLi works directly. |
| Medium | Partial protection with `mysql_real_escape_string()`, but exploitable via POST and UNION queries. |
| High   | Uses session variables; input harder to exploit, but still possible with advanced payloads. |

---

## Step-by-Step Testing

### Security Level: Low
1. **Input used:** `1' OR '1'='1`  
2. **Actions performed:** Entered input in the User ID field under SQL Injection module (GET request).  
3. **Screenshot:**
   <p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/sql_injection_low.png" width="80%">
</p>
  
4. **Observations / Results:**  
   - All user records were displayed instead of one.  
   - Shows that **Low security does not validate or filter inputs**.  
   

---

### Security Level: Medium
1. **Input method:** POST form with a pre-defined dropdown list.  
2. **Payload used:** `?id=a UNION SELECT 1,2;-- -&Submit=Submit`  
3. **Actions performed:** Submitted the form using the payload.  
4. **Screenshot:**  
   <p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/sql_injection_low.png" width="80%">
</p>
5. **Observations / Results:**  
   - Application uses `mysql_real_escape_string()` for basic filtering.  
   - Still vulnerable because query lacks quotes around the parameter.  
   - Some user data returned using `UNION SELECT` technique.  
   - Shows **Medium security partially protects, but can still be bypassed**.

---

### Security Level: High
1. **Input method:** Session-based input via another page.  
2. **Payload used:** `a' UNION SELECT "text1","text2";-- -&Submit=Submit`  
3. **Actions performed:** Entered payload in the session-handled field and submitted.  
4. **Screenshot:**  
  <p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/sql_injection_low.png" width="80%">
</p>
5. **Observations / Results:**  
   - Input transferred via session variables rather than direct GET request.  
   - Advanced payloads are required, but vulnerability still exists.  
   - Shows **High security makes exploitation harder but is not fully secure**.

---


## Impact Analysis
- Unauthorized access to sensitive user data.  
- Possible full database compromise.  
- Highlights the need for **secure coding practices** and **input validation**.

## Remediation / Suggestions
- Use **parameterized queries** / prepared statements.  
- Validate and sanitize all user inputs.  
- Limit database privileges for application accounts.  
