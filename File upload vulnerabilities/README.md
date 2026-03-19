# File Upload Vulnerabilities

File upload functionality allows users to send files to a server, such as images or documents.

If not properly secured, attackers can upload **malicious files** that may be executed by the server.

For example, uploading a script disguised as an image could lead to **remote code execution (RCE)**.

## Common File Upload Vulnerabilities

- **Unrestricted file types** – Allowing dangerous extensions like .php  
- **Content-type bypass** – Trusting only headers instead of actual file content  
- **Executable upload directories** – Uploaded files can be executed by the server  
- **File name manipulation** – Changing extensions to bypass filters  

## Impact

File upload vulnerabilities can allow attackers to:

- execute code on the server  
- gain full system access  
- upload backdoors  
- steal or modify data  

## Key Security Principle

Always validate file type, content, and store uploads securely outside the web root.
