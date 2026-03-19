# Server-Side Request Forgery (SSRF)

SSRF occurs when an application allows users to make **server-side HTTP requests** to arbitrary locations.

Attackers can exploit this to make the server send requests to internal or restricted systems.

For example, accessing internal admin panels that are not publicly exposed.

## Common SSRF Vulnerabilities

- **Unvalidated URLs** – Accepting user-controlled URLs  
- **Access to internal services** – 127.0.0.1 or internal IP ranges  
- **Cloud metadata exposure** – Accessing sensitive cloud endpoints  
- **Bypassing filters** – Using encoding or redirects  

## Impact

SSRF vulnerabilities can allow attackers to:

- access internal systems  
- bypass firewalls  
- retrieve sensitive data  
- interact with cloud infrastructure  

## Key Security Principle

Restrict and validate all outbound requests made by the server.
