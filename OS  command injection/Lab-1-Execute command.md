## Lab: OS Command Injection – Execute whoami

### Goal

Determine whether the application is vulnerable to OS command injection and execute the `whoami` command to identify the current user.

---

### Observation

The application contains a product stock checker.

It allows users to input:

- productId  
- storeId  

The server executes a backend command:

stockreport.pl productID storeID  

Example:

stockreport.pl 381 29  

This suggests that user input is passed directly into a shell command.

The response returns raw command output, which is a strong indicator of possible command injection.

---

### Test

I entered normal values into the stock checker to observe how the application behaves.

Then I intercepted the request using Burp Suite.

The request included:

- productId  
- storeId  

I sent the request to Burp Repeater to modify the input.

---

### Payload

I injected a command using a separator.

Payload used:

productId=1;whoami  
storeId=1  

---

### Explanation of the Payload

- `;` is a command separator in the shell  
- It ends the original command and starts a new one  
- `whoami` prints the current OS user  

---

### Command Executed by Server

stockreport.pl 1;whoami 1  

---

### Shell Interpretation

stockreport.pl 1  
whoami 1  

The first command runs normally.

The second command (`whoami`) is injected and executed.

---

### Result

The response included the output of:

whoami  

Example output:

www-data  

This confirms that:

- The server executed our injected command  
- The application is vulnerable to OS command injection  

---

### Useful Commands

| Purpose of command | Linux | Windows |
|------------------|--------|---------|
| Name of current user | whoami | whoami |
| Operating system | uname -a | ver |
| Network configuration | ifconfig | ipconfig /all |
| Network connections | netstat -an | netstat -an |
| Running processes | ps -ef | tasklist |

---

### What is stockreport.pl

A backend script that checks product stock.

It takes two arguments:

- productID  
- storeID  

Example:

stockreport.pl 381 29  

Meaning:

Check stock of product 381 in store 29  

---

### Problem

User input is directly inserted into a shell command.

This allows attackers to inject arbitrary commands.

---

### Key Trick

Break the original command using a separator.

Common separators:

;  
&  
|  

---

### Impact

OS command injection can lead to:

- Remote command execution  
- Data exposure  
- Server compromise  
- Full system takeover  

---
