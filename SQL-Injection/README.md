# SQL Injection

SQL Injection occurs when user input is directly included in a **database query** without proper sanitization.

This allows attackers to manipulate queries and access or modify database data.

For example, an attacker can bypass login or retrieve all database records.

## Common SQL Injection Vulnerabilities

- **Login bypass** – Using payloads like `' OR 1=1--`  
- **Data extraction** – Dumping database contents  
- **Filter bypass** – Ignoring conditions like category filters  
- **Error-based injection** – Revealing database structure  

## Impact

SQL injection can allow attackers to:

- bypass authentication  
- access sensitive data  
- modify or delete database records  
- take full control of the application  

## Key Security Principle

Always use parameterized queries and never trust user input.
