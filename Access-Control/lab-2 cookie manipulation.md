# Lab: Access Control – Admin Access via Cookie Manipulation

## Goal

Determine whether administrative privileges are controlled through client-side parameters.

## Observation

After logging into the application, I inspected the cookies using Burp Suite.

One cookie contained the following parameter:

admin=false

This suggests that the application determines admin privileges based on a client-side value.

## Test

I modified the cookie value:

admin=true

and forwarded the request to the server.

## Payload

admin=true

## Explanation

Changing the cookie value attempts to escalate privileges by tricking the server into believing the user is an administrator.

## Result

After modifying the cookie, the application granted access to the admin panel.

I was able to delete the user **carlos**, which solved the lab.

## Impact

If authorization is controlled on the client side, attackers can modify values to gain elevated privileges.

This could allow attackers to:

- access admin panels  
- modify or delete users  
- perform privileged actions  

## Key Learning

Authorization decisions must always be enforced on the server side.

Client-controlled values should never determine access levels.
