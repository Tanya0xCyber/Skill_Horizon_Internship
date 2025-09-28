
# DVWA on Kali Linux: XSS & File Upload Security Comparison

## **Objective**
- Compare how DVWA handles **Cross‑Site Scripting (XSS)** and **Unrestricted File Upload** across security levels (Low → Medium → High → Impossible).  
- Capture reproducible evidence (screenshots + raw outputs).  
- Produce concise findings and remediation suggestions for each vulnerability.

---

## **Folder Structure**

```

DVWA-Security-Levels/
│
├── README.md
├── comparison/
│   ├── xss.md
│   └── file-upload.md
│
├── screenshots/
│   ├── xss/
│   │   ├── low.png
│   │   ├── medium.png
│   │   ├── high.png
│   └── file-upload/
│       ├── low.png
│       ├── medium.png
│       ├── high.png


```

---

## **Quick Setup**
1. Start DVWA on Kali and login (`admin` / `password` by default).  
2. Ensure folders above exist (`screenshots/`, `raw-output/`, `comparison/`).

---

## **Scope**
- **Target:** DVWA running locally (`http://127.0.0.1/dvwa`)  
- **Vulnerabilities:** XSS (Reflected/Stored) and File Upload (unrestricted uploads)  
- **Security levels:** Low, Medium, High, Impossible

---

## **Testing Flow (per vuln)**
1. Set DVWA security → **Low**. Run payloads, capture screenshot & raw output.  
2. Repeat for **Medium**, **High**, **Impossible**.  
3. Save evidence using the naming convention above.

---

