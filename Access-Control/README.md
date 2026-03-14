# Access Control

Access Control is a security mechanism that determines **who is allowed to access or perform actions on specific resources** within an application.

It ensures that users can only access the data and functionality that they are authorized to use.

For example, a normal user should not be able to access **administrator panels**, modify other users, or perform privileged actions.

## Common Access Control Vulnerabilities

When access control is not properly implemented, attackers may be able to bypass restrictions. Some common vulnerabilities include:

- **Unprotected admin functionality** – Admin panels accessible without authentication
- **Parameter-based access control** – Privileges controlled by modifiable parameters
- **Cookie or client-side manipulation** – Authorization controlled by user-controlled values
- **Insecure direct object references (IDOR)** – Accessing other users' data by modifying IDs

## Impact

Access control vulnerabilities can allow attackers to:

- gain administrative privileges  
- access sensitive information  
- modify or delete application data  
- perform actions as other users  

## Key Security Principle

Access control must always be **enforced on the server side**.  
Client-side controls such as cookies, hidden fields, or URL parameters should **never be trusted for authorization decisions**.
