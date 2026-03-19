# Lab: Authentication – 2FA Bypass

## Goal
Determine whether the two-factor authentication process can be bypassed.

## Observation
The application required valid login credentials followed by a 2FA verification step. During testing, I noticed that the URL contained a parameter that identified the user account (e.g., `user=weiner`). This indicated that the application might be relying on client-controlled input to track the user during the 2FA process.

## Test
I first logged in using my own account (`weiner`) and observed the request during the 2FA step. Then, while attempting to access another account, I modified the `user` parameter in the request instead of following the normal authentication process.

## Payload
Change the `user` parameter from:

```
weiner
```

to:

```
carlos
```

## Explanation
The application relied on the `user` parameter in the request to determine which account was being verified during the 2FA step. However, it failed to properly validate that the session belonged to that user and that the correct 2FA code was provided. By modifying this parameter, I was able to switch to another user without completing their 2FA verification.

## Result
The server accepted the modified request without requiring a valid 2FA code for the victim account. This allowed successful login as the victim user.

## Impact
Bypassing two-factor authentication significantly weakens account security. An attacker with valid credentials could bypass the second authentication factor, gain unauthorized access to user accounts, and access sensitive information.

## Key Learning
2FA mechanisms must be securely tied to server-side sessions. Applications should never rely on client-controlled input (such as URL parameters) to determine authentication state and must strictly validate the user identity at every step of the login process.
