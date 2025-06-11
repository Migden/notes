2025-04-17 05:10

##### Learning Covered:
- Learn the difference between file inclusion and directory traversal
- Gain an understanding of File inclusion vulnerabilities
- Understand how to leverage LFI to obtain code execution
- Explore PHP Wrapper usage
- Learn how to preform remote file inclusion (RFI) Attacks
--------------------------
Tags: [[PHP]], [[Wrappers]]


### Local File Inclusion
--------------------------------
Directory Traversal allows us to view the code, but a Local File inclusion allows us to include a file in the applications running code. This means that LFI executes the files.

A large goal of LFI is to obtain RCE. We can do this in several methods:

- Log Poisoning, SSH, WEB, SMTP
- Malicous File Upload

### PHP Wrappers
----
PHP offers a variety of protocol wrappers to enhance the languages capabilities. For example, PHP wrappers can be used to represent and access local or remote filesystems. We can use these wrappers to bypass filters or obtain code execution.

PHP Wrappers include but not limited too:
- php://
- data://
- file://
- http://
- ftp://
- zip://
- phar://

We can use the `php://filter` wrapper to display the contents of a file with encodings like base64. This allows us to review the contents of a file as well as executing the file.

`php://filter/resource=admin.php`
`php://filter/convert.base64-encode/resource=admin.php`

The `data://` wrapper allows for you to embed data directly within the URI.

`data://text/plain,<?php echo system('ls');?>`

##### Root-Me LFI - Wrappers

Using the `zip://` or `phar://` wrapper we can execute commands inside of the respective archive file.

The syntax is as following `zip://<directory of archive>#<file inside archive>.php`

Using a image upload feature and changing the extension we uploaded the file and accessed it utilizing LFI and PHP wrappers

##### Root-Me LFI - Double Encoding

Using the `php://filter/convert.base64-encode/resource=` we are able to return the contents of any PHP file.

However the server is checking for malicious input and block characters such as `:`, and `../`. However double URL encoding the payload bypasses this filter

### Remote File Inclusion
---
Remote File inclusion vulnerabilities are less common than LFIs since the target system must be configured in a certain way. For example the `allow_url_include` option needs to be enabled.

The remote file inclusion works by the server allowing remote URLs to be referenced in code. So just supplying a URL to a PHP file in a vulnerable input is mostly enough to gain code execution
### References:




