# SQL-injection

When SQL queries use user-supplied input that is not properly sanitized the application becomes vulnerable. <br>
This can allow an attacker to interfere with database queries in ways the developer never intended.

That is not good. Contraproductive even. Since databases often containes sensetive and critical data we most of the time want to controll who can see, edit and delete it.


## What is it?

SQL injection is a vulnerability that occurse when an application builds SQL queries direectly including user inputs into a query string. <br>
  
If that input is not handled safely, an attacker may be able to:

- Read sensitive data from the database
- Modify or delete database content
- Bypass authentication mechanisms

In some cases, execute administrative database operations.<br>
The application trusts input it should never trust.



## How is it done?

SQL Injection happens when:

1. User input is accepted (URL parameters, form fields, cookies, headers)
2. That input is concatenated directly into an SQL query mixing SQL instruction and parameters
3. The database executes the query without proper safeguards
 
Instead of being treated as data, the input is interpreted as SQL code.<br>
This allows an attacker to change the logic of the query itself. 

### Examples

- Turning a restrictive query into one that always returns true (example login)
- Accessing data beyond what the user should be allowed to see (all databases on the server, tables, columns rows)
- Manipulating how the database processes requests (delete data, create new, update and so on)
 
### Examples of Unsafe SQL createion

Here are some examples of dangerous SQL-query creation.  
PHP
```php  
$sql = "SELECT firstname, lastname FROM users WHERE id = " . $_GET['id'];
$stmt = $db->query($sql);
```
Python (sqlite / psycopg / mysql style)
```python  
query = "SELECT firstname, lastname FROM users WHERE id = " + request.args["id"]
cursor.execute(query)
```
Python (f-strings)
```python  
query = f"SELECT firstname, lastname FROM users WHERE id = {user_id}"
cursor.execute(query)
```

.NET (C#)
```c#  
string sql = "SELECT firstname, lastname FROM users WHERE id = " + userInput;
SqlCommand cmd = new SqlCommand(sql, connection); 
```
Go
```go
query := "SELECT firstname, lastname FROM users WHERE id = " + userInput
rows, _ := db.Query(query)
``` 
Node.js 
```javascript
const sql = "SELECT firstname, lastname FROM users WHERE id = " + req.query.id;
connection.query(sql, callback);
```

## How do we protect agains it?

Prepared statments to the rescue. <br>
_Parameters are always treated as data, never as SQL commands._

With prepared statments we are seperating the parameters from the SQL instructions. <br>
The database will now know what is supposed to be the parameter and what are instructions.

Set [Least privilegie](../principles/least-privilege.md) on database accounts. 

### Examples

```PHP 
$stmt = $pdo->prepare("SELECT firstname, lastname FROM users WHERE id = :id");
$stmt->execute(['id' => $_GET['id']]);
```

Python (DB-API compliant)
```python
query = "SELECT firstname, lastname FROM users WHERE id = %s"
cursor.execute(query, (user_id,))
```

Python (sqlite)
```python
query = "SELECT firstname, lastname FROM users WHERE id = ?"
cursor.execute(query, (user_id,))
```

.NET (C#)
```c#  
string sql = "SELECT firstname, lastname FROM users WHERE id = @id";
SqlCommand cmd = new SqlCommand(sql, connection);
cmd.Parameters.AddWithValue("@id", userInput);
```

Go
```go
query := "SELECT firstname, lastname FROM users WHERE id = ?"
rows, err := db.Query(query, userInput)
``` 

Node.js 
```javascript
const sql = "SELECT firstname, lastname FROM users WHERE id = ?";
connection.query(sql, [req.query.id], callback);
```
 
## Questions to ponder
- Where in an application does user input enter the system?<br>
_login forms, get params and so on._
- Is input validated at the boundary, or trusted too early?<br>
_Do we trust input data in the controller and all thorugh the system? OR is the input validated?_<br>
*If a value is allowed to cross the boundary, every internal layer should be able to trust it.*
- Are database errors visible to users or logs accessible externally?<br> 
- Does the application use different database roles for different tasks?<br>
_least privilege_
- If a database dump leaked, how severe would the impact be?<br>
_I hope you are not storing plaintext passwords?<br>
And that your password complexity policy makes people very upset_ 
 
## Related resources 
[SQLMap - knock on the DB door](../tools-and-tips/sqlmap.md) 