# Lab: SSRF – Local & Internal Network Access

## Goal
Determine whether the application is vulnerable to Server-Side Request Forgery (SSRF) and whether internal systems can be accessed.

## Observation
The application allowed checking product stock, which triggered an HTTP request to an internal API. By inspecting the request, I noticed a parameter (e.g., `api=`) that controlled the backend request URL.

This indicated that the server was fetching data from a user-supplied URL, which could potentially be manipulated.

## Test (SSRF Local)
While checking stock, I modified the `api` parameter to point to an internal endpoint:

```
http://localhost/admin
```

## Payload (Local SSRF)
```
api=http://localhost/admin
```

## Explanation (Local SSRF)
The application did not properly validate or restrict the URL supplied in the `api` parameter. By changing it to `localhost`, I was able to make the server send a request to its own internal admin panel.

Since the request originated from the server itself, access controls were bypassed, allowing interaction with restricted functionality.

## Result (Local SSRF)
I gained access to the internal admin panel and was able to perform administrative actions, such as deleting the user `carlos`.

---

## Test (SSRF Internal Network)
To expand the attack, I attempted to access other internal systems within the network.

I used an automated tool (Intruder) to brute-force internal IP addresses in the range:

```
192.168.0.1 - 192.168.0.255
```

on port `8080`.

## Payload (Internal SSRF)
```
api=http://192.168.0.X:8080
```

Where `X` ranged from 1 to 255.

## Explanation (Internal SSRF)
The application allowed requests to arbitrary internal IP addresses. By brute-forcing the subnet, I identified a valid internal host running a service on port 8080.

This worked because:
- there was no filtering of internal IP ranges  
- the server trusted user input for backend requests  
- internal services were accessible from the server  

## Result (Internal SSRF)
I discovered a valid internal service and was able to interact with it, potentially exposing sensitive functionality or data not intended for external users.

---

## Impact
SSRF vulnerabilities can allow attackers to:
- access internal systems and admin panels  
- bypass firewalls and access controls  
- interact with internal APIs and services  
- perform unauthorized actions (e.g., delete users)  

This can lead to full system compromise depending on what internal services are exposed.

---

## Key Learning
Applications must strictly validate and restrict user-supplied URLs.

To prevent SSRF:
- block access to internal IP ranges (e.g., 127.0.0.1, 192.168.x.x)  
- use allowlists for permitted domains  
- avoid directly using user input in server-side requests  

SSRF protections are critical to prevent exposure of internal infrastructure.
