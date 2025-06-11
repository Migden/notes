2025-04-18 04:33

##### Learning Covered:
- Understand File Upload Vulnerabilities
- Learn how to identify File Upload vulnerabilities
- Explore different vectors to exploit File upload vulnerabilities
--------------------------
Tags:


### File Upload Vulnerabilities
--------------------------------
Many web applications provide functionality to upload files. 

The first category consists of vulnerabilities that enable us to upload files that are executable by the web application. Allowing users to upload files that contain executable code is dangerous as a LFI exploit could lead to these files becoming executable.

The second category consist of vulnerabilities that require us to combine the file upload mechanism with another vulnerability such as directory traversal. We could overwrite important system files such as *authorized_keys* if we exploit that file upload to traverse directories.

The third category relies on user interaction. For example, when we discover an upload form for job applications. We can upload a CV in a `.docx` format with malicious macros inside.

### Using Executable Files
------
Depending on the web application used we can make guesses to locate upload mechanisms; such as profile avatars, text documents, images, etc.

When uploading a file it is common for the server to filter extensions for the file type to filter out potentially malicious files. This can be bypassed by a trial-and-error approach and many different scenarios could occur so it is important to remember what we can do to bypass filters.

We could change the file extension to lesser know `file types`. Or change to uppercase and lowercase letters. On potentially relying on canonicalization. Infinite possibilities can be used to bypass filters 

File Types that can be used to upload malicious code:
- php
- aspx
- py
- .etc
### Using Non-Executable Files
----
Allowing User Input to insecurely upload files even if they can't be executed is still a large risk. As if We utilize a directory traversal vulnerability we could overwrite important system files and crash the webserver or overwrite SSH keys.

Technically if the webserver states that a file already exists we could use this mechanism to brute-force existing files.


### References:

 


