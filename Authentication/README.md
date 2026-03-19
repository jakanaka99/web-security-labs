# Authentication

Authentication is the process of verifying the **identity of a user** before granting access to an application.

It ensures that users are who they claim to be, typically through **usernames, passwords, or multi-factor authentication (MFA)**.

For example, only a legitimate user should be able to log into their account and access personal data.

## Common Authentication Vulnerabilities

When authentication is weak or improperly implemented, attackers may be able to bypass it. Common issues include:

- **Login bypass** – Skipping authentication using SQL injection or logic flaws  
- **Weak credentials** – Guessable or default passwords  
- **Broken session management** – Predictable or reusable session tokens  
- **2FA flaws** – Bypassing or brute-forcing second-factor authentication  

## Impact

Authentication vulnerabilities can allow attackers to:

- access other users’ accounts  
- take over administrator accounts  
- steal sensitive information  
- perform actions as legitimate users  

## Key Security Principle

Always enforce strong authentication and never trust user input.
