If the application does not properly validate this parameter, it may be possible to access files outside the intended directory.

Test

I attempted to move outside the images directory by using directory traversal sequences:

../

The sequence ../ moves one directory up in the filesystem.

By chaining multiple ../, an attacker may reach sensitive system directories.

Payload
/image?filename=../../../etc/passwd
Explanation

The payload uses multiple ../ sequences to move out of the image directory and access the system file:

/etc/passwd

This file exists on most Linux systems and contains user account information.

Result

The server returned the contents of the /etc/passwd file, confirming that directory traversal was possible.

This solved the lab.

Impact

If directory traversal vulnerabilities exist, attackers may be able to access sensitive files on the server.

This could allow attackers to:

read system configuration files

access application source code

obtain sensitive credentials

gather information about system users

Key Learning

User input used in file paths must be strictly validated.

Applications should restrict file access to specific directories and prevent traversal sequences like:

../

Using proper input validation and secure file handling prevents directory traversal attacks.
