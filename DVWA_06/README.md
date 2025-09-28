# DVWA on Kali Linux: Installation & Web Vulnerability Discovery

## **Objective**

* Install and configure **Damn Vulnerable Web Application (DVWA)** on Kali Linux.
* Learn to **safely discover and document common web vulnerabilities** in a lab environment.
* Produce a professional report including **evidence, impact analysis, and remediation suggestions**.

---

## **Folder Structure**


```
DVWA_06/
│
├── README.md               # Clean overview (like we just made)
├── vulnerabilities/
│   ├── sql-injection.md    # Detailed writeup for SQLi
│   ├── xss.md              # Detailed writeup for XSS
│   ├── command-injection.md
│   ├── file-upload.md
│
└── screenshots/
    ├── sql-injection/
    ├── xss/
    ├── command-injection/
    ├── file-upload/
    └── ...

```



---

## **Tasks Overview**

### **1. Installation & Setup**

1. Update your system and install DVWA:

```bash
sudo apt update
sudo apt install dvwa
```

2. Start DVWA:

```bash
sudo dvwa-start
```

> **Note:** DVWA will open in your default web browser.

---

### **2. DVWA Security Levels**

* DVWA allows adjusting security levels: **Low → Medium → High**.
* **Process:**

  1. Set security to **Low**, run vulnerability tests.
  2. Increase to **Medium**, rerun tests.
  3. Set to **High**, rerun tests.
* This demonstrates **how security measures affect vulnerability exploitation**.

---

### **3. Vulnerability Exercises**

Manually explore the following vulnerabilities:

| Vulnerability                                     | Description                                                |
| ------------------------------------------------- | ---------------------------------------------------------- |
| **SQL Injection**                                 | Inject malicious SQL queries to access unauthorized data.  |
| **Cross Site Scripting (XSS)**                    | Inject scripts to manipulate or steal user session info.   |
| **Command Injection**                             | Execute system commands via vulnerable inputs.             |
| **File Upload / Unrestricted Upload**             | Upload malicious files to server.                          |
| **Insecure Direct Object Reference (IDOR)**       | Access unauthorized resources by manipulating URLs or IDs. |
| **Security Misconfigurations / Insecure Headers** | Identify incorrect server or application settings.         |
| **Sensitive Info in Source / JS**                 | Find sensitive data in HTML, JavaScript, or comments.      |
| **Session Management Weaknesses**                 | Test cookies, sessions, and authentication flaws.          |

---

### **4. Light Automation / Reconnaissance**

Use automated tools to quickly confirm vulnerabilities:

| Tool                              | Purpose                                                       |
| --------------------------------- | ------------------------------------------------------------- |
| **Nikto**                         | Scan server for misconfigurations and vulnerabilities.        |
| **WhatWeb**                       | Identify server, CMS, and software versions (fingerprinting). |
| **Dirb / Content Discovery Tool** | Discover hidden directories or files on the server.           |
| **Nuclei**                        | Run vulnerability templates for quick scanning.               |

---


### . Conclusion**

* DVWA provides a **safe environment** to practice web vulnerability testing.
* Testing across different security levels shows **how misconfigurations and weak coding can be exploited**.
