# SQL Injection (SQLi)

## Overview
SQL Injection is a vulnerability where an attacker can manipulate database queries through user inputs to access, modify, or delete data they shouldn't.  
It is critical because it can lead to **data breaches, unauthorized access, and database compromise**.


---

## Step-by-Step Testing

### Security Level: Low
* **Input used:** `1' OR '1'='1`  

* **Screenshot:**
   <p align="center">
  <img src="https://github.com/Tanya0xCyber/Skill_Horizon_Internship/blob/main/DVWA_06/screenshots/sql_injection_low.png" width="80%">
</p>
  
* **Observations:**  
   - All user records were displayed instead of one.  
   - Shows that **Low security does not validate or filter inputs**.  
   

---

## Impact Analysis
- Unauthorized access to sensitive user data.  
- Possible full database compromise.  
- Highlights the need for **secure coding practices** and **input validation**.

## Remediation 
- Use **parameterized queries** / prepared statements.  
- Validate and sanitize all user inputs.  
- Limit database privileges for application accounts.  
