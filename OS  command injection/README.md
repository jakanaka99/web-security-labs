# OS Command Injection

OS Command Injection occurs when an application executes **system-level commands using user input** without proper validation.

This allows attackers to inject and execute arbitrary commands on the server.

For example, instead of checking stock, an attacker could run commands like `whoami` or `ls`.

## Common Command Injection Vulnerabilities

- **Unsanitized input in shell commands**  
- **Use of dangerous functions (system, exec, etc.)**  
- **Lack of input validation**  
- **Direct command concatenation**  

## Impact

Command injection can allow attackers to:

- execute arbitrary system commands  
- access sensitive files  
- gain server control  
- escalate privileges  

## Key Security Principle

Never pass user input directly into system commands.
