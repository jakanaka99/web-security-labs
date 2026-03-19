## Lab: Access Control – Method-Based Bypass

### Goal

Exploit weak access control where authorization depends on the HTTP method to perform an unauthorized action.

---

### Observation

The application has an admin panel that allows promoting users.

The request used by the admin is:

POST /admin-roles  
username=carlos&action=upgrade  

This suggests that:

- Only admins should be able to access this functionality  
- The server checks authorization based on the request  

However, improper validation of HTTP methods may allow bypassing access control.

---

### Test

I logged in as an administrator and accessed the admin panel.

Using Burp Suite, I intercepted the request responsible for promoting a user.

Then I sent the request to Burp Repeater.

Next, I logged in as a normal user (wiener) and copied the session cookie.

---

### Payload / Modification

I modified the admin request:

- Replaced admin session with normal user session  
- Changed username to wiener  

Modified request:

POST /admin-roles  
Cookie: session=WIENER  
username=wiener&action=upgrade  

---

### Result (Initial Attempt)

The server returned **Unauthorized**.

This confirms that access control is enforced for POST requests.

---

### Bypass Technique

I changed the HTTP method:

POST → GET  

Final request:

GET /admin-roles?username=wiener&action=upgrade  
Cookie: session=WIENER  

---

### Explanation of the Bypass

- The server enforces access control only for POST requests  
- GET requests are not properly protected  
- By switching the method, the authorization check is bypassed  

---

### Result

The request succeeded, and the user was promoted.

This confirms a **method-based access control bypass**.

---

### Key Concept

Access control should be enforced consistently across all HTTP methods.

If one method is protected and another is not, attackers can switch methods to bypass restrictions.

---

### Quick Notes

🔑 When URL is blocked → use X-Original-URL  
🔑 When method is blocked → change GET/POST  
🔑 Parameters → keep them in the real URL  

---

### Impact

This vulnerability allows attackers to:

- perform admin actions without privileges  
- escalate user roles  
- bypass authorization controls  

---



