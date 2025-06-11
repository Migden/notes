2025-04-17 03:55

##### Learning Covered:
- Understand Absolute and Relative Paths
- Learn how to exploit directory traversal vulnerabilities
- Use encoding for special characters
--------------------------
Tags:  


### Absolute vs Relative Paths
--------------------------------
When working with Paths in any operating system it is important to be able to distinguish between *absolute* and *relative* Paths.

*Absolute* paths are paths that no matter where the current working directory is the command will always point to the same location. This is done by starting from the *root* of the file tree.

*Relative* paths are paths that are determined from the current directory such as `../../../etc/passwd`. Only from some working directories will this path reference the desired material.

### Identifying and Exploiting Directory Traversals
-------
For a web application to show a specific page it has to know where it is in the file system. Traditionally the base of the web application is located in the `/var/www/html` directory and the access the initial page the server would host `/var/www/html/index.html`.

It is important to test anything that is loading or selecting a file such as a different `.html` file for different languages. 

Windows servers are not as easy to leverage the directory traversal for system access. In Linux it is a matter of showing user private keys. But on windows there is no equivalent. We would have toe examine the web application for frameworks or information to determine if sensitive files may be included such as hard-coded credentials or admin pages. Once we gather information about web application technology we can research paths leading to sensitive information such as `C:\inetpug\logs\LogsFiles\W3SVC1` - for logs, or `C:\inetpub\www\root\web.config` - passwords and usernames.

##### IMPORTANT
- Windows utilizes `\` instead of `/`.

### Encoding Special Characters
---
A very simple Web Application Firewall or filters will prevent basic directory traversal by blocking malicious characters that could be used in a number of attacks. A way to bypass these filters is to encode them to avoid the filter turning a positive match (More advanced filters will just decode them).

Depending on what the filter is doing with the information will determine how we craft our payload to get the results we want.

Such  as:
- URL Encoding
- Filter removes bad characters payload = `....//....//....//`. Once removed it will become malicious
### References:




