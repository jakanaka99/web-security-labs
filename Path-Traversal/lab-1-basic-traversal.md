# Lab: Directory Traversal – Accessing /etc/passwd

## Goal

Verify whether the application allows access to files outside the intended directory.

---

## Observation

The application loads images using the following parameter:

/image?filename=<file>

This indicates that the server reads files directly from the filesystem based on the value of `filename`.

If the application does not properly validate this parameter, it may be possible to access files outside the intended directory.

---

## Test

I attempted to move outside the images directory by using directory traversal sequences:

../

The sequence `../` moves **one directory up** in the filesystem.

By chaining multiple `../`, an attacker may reach sensitive system directories.

---

## Payload

/image?filename=../../../etc/passwd

Explanation:

../../../

Moves up multiple directories until reaching the root of the filesystem.

/etc/passwd

This is a system file on **** that stores user account information and is commonly used to confirm a directory traversal vulnerability.

---

## Result

The server returned the contents of `/etc/passwd`.

This confirms that the application does **not properly restrict file paths**, allowing attackers to access files outside the intended directory.

---

## Impact

An attacker could potentially read sensitive files from the server such as:

* configuration files
* application source code
* credentials
* system files

This could lead to further compromise of the application or server.

---

## Key Learning

User-controlled file paths must always be **validated and restricted**.
The application should ensure that files are only loaded from the intended directory.
