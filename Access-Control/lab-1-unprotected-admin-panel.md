# Lab: Access Control – Unprotected Admin Panel (robots.txt)

## Goal

Verify whether the application exposes sensitive admin functionality through publicly accessible paths.

---

## Observation

The application appears to have an admin panel, but its location is not directly visible in the interface.

Many websites use the file:

```
/robots.txt
```

This file is intended for search engines like Google to indicate which paths should not be indexed.

Sometimes developers mistakenly list sensitive directories in this file.

---

## Test

I requested the following file using Burp Suite:

```
/robots.txt
```

Inside the response, I found a hidden path pointing to an admin panel.

---

## Payload

```
/admin-path
```

---

## Explanation

The `robots.txt` file contained a hidden directory that led to the admin interface.

---

## Result

Accessing the path provided full access to the admin panel.

I was able to delete the user **carlos**, which solved the lab.

---

## Impact

If sensitive admin paths are exposed through `robots.txt`, attackers can easily discover them and gain access to restricted functionality.

This could allow attackers to:

* Access administrative interfaces
* Delete users
* Modify application data

---

## Key Learning

* Sensitive directories should never be exposed in `robots.txt`
* Access control must be enforced on the server side
