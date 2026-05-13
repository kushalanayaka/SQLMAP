# SQLMap Learning Journey – OWASP Juice Shop Exploitation

**Target Website:** `https://juice-shop.herokuapp.com`

> This lab was performed on the OWASP Juice Shop vulnerable application for educational security testing and SQL Injection learning purposes only.

---

## Step 1 – Identifying the Back-End Database

### Command Used
```bash
sqlmap -r owasp.txt --dbs
```

- Started SQL Injection testing against the OWASP Juice Shop login request using a captured HTTP request file.
- SQLMap successfully detected a boolean-based blind SQL Injection vulnerability and identified the back-end DBMS as SQLite.

<img width="1365" height="452" alt="TASK3" src="https://github.com/user-attachments/assets/4e5d9ba5-d2b1-482d-842e-e52776bbc966" />

---

## Step 2 – Identifying Database Name and  Enumerating Database Tables

### Command Used
```bash
sqlmap -r owasp.txt -D SQLite_masterdb --tables --level=3 --risk=2
```

- Enumerated tables from the `SQLite_masterdb` database to understand the application's internal database structure.
- SQLMap successfully discovered tables such as `users`, `products`, `cards`, and `addresses`
.
<img width="1341" height="503" alt="TASK3-S1" src="https://github.com/user-attachments/assets/36fffbc8-bd28-40d0-9528-c6167d4fce0b" />
<img width="1344" height="495" alt="TASK3-S2" src="https://github.com/user-attachments/assets/9322b66f-697c-4d6c-b476-949b91d228ea" />

---

---

## Step 4 – Reviewing SQLMap Output Files

### Commands Used
```bash
sqlmap -r owasp.txt -D SQLite_masterdb -T users --dump --level=3 --risk=2
cd /root/.local/share/sqlmap/output/juice-shop.herokuapp.com
ls -l
ls -R
```
- Attempted to dump records from the `users` table to retrieve stored user information from the vulnerable application.
- SQLMap stored the extracted session data, logs, and dumped content inside the local SQLMap output directory for further analysis.
- Navigated to the SQLMap output directory to inspect generated logs, session files, and dumped database content.
- Verified that SQLMap created files such as `session.sqlite`, `target.txt`, and dump directories containing extracted data.

<img width="1360" height="614" alt="TASK3-S3" src="https://github.com/user-attachments/assets/e386ee41-a87e-4f1f-ae92-7b3ea0ae92d3" />
