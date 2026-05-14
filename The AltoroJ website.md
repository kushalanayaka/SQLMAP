# SQLMap Learning Journey

**Target Website:** `https://demo.testfire.net/login.jsp`

> This target is a deliberately vulnerable demo application used for security testing and learning purposes.

---

## Step 1 – Enumerating Databases
### Command Used
```bash
sqlmap -r testfire.txt --dbs
```
- Started database enumeration using SQLMap to identify all accessible databases from the vulnerable target.
- SQLMap successfully retrieved multiple database names, confirming the SQL Injection vulnerability and database access.
<img width="1371" height="615" alt="TASK1-S2" src="https://github.com/user-attachments/assets/aecdb272-4339-48b8-89fe-7f5a9e85ae58" />

<br>
---

## Step 2 – Database Discovery Result
### Command Used
```bash
sqlmap -r testfire.txt --current-db
```
- The output displays the list of available databases extracted from the target application.
- This step helps identify the correct database for further enumeration such as tables, columns, and sensitive data.
<img width="1356" height="415" alt="TASK1-S1" src="https://github.com/user-attachments/assets/ba68a252-8c3b-45e3-be89-4773f6dabc5b" />

<br>
---

## Step 3 – Enumerating Tables from Selected Database

### Command Used
```bash
sqlmap -r testfire.txt -D AAA --tables
```
- Selected the target database and performed table enumeration to identify available tables inside it.
- SQLMap successfully discovered tables such as `ExtrinsicObject` and `partscustomer`, which can be used for further data extraction.
<img width="1374" height="551" alt="TASK1-S3" src="https://github.com/user-attachments/assets/e5858714-6da2-4585-8ed8-6caf2210c5a9" />
<br>
---
## Step 4 – Enumerating Columns from the Selected Table

### Command Used
```bash
sqlmap -r testfire.txt -D AAA -T PARTSCUSTOMER --columns 
```

- Attempted to enumerate column names from the `PARTSCUSTOMER` table inside the `AAA` database.
- Since direct column retrieval was restricted, SQLMap used a common column wordlist and successfully identified columns such as `telefono`, `box`, `mod_cssmenu`, and `id_gebruiker`.

<img width="1376" height="571" alt="TASK1-S4" src="https://github.com/user-attachments/assets/8cb0deed-3015-49ae-bd31-c2904a634724" />

