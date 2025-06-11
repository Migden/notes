2025-05-11 04:35

##### Learning Covered:

--------------------------
Tags: [[XSS]]

### What is the Document Object Model?
---
The Document Object Model is a tree like structure that represents the web page, when a response comes back from the webserver it is loaded into the `DOM` and is saved in client memory, the site JavaScript can dynamically make changes to the objects in the `DOM` tree.
### DOM-Based XSS Vulnerabilities
--------------------------------
Both reflected and stored XSS vulnerabilities involve a specific pattern of behavior, in which the application takes user controllable data and displays it back in an insecure way. 

The DOM Based XSS does not share these characteristics.

DOM Based XSS works as follows:
- Users requests a crafted URL supplied by the attacker and containing embedded JavaScript
- The servers response does not contain attackers script in any form
- Nonetheless the script is executed on the users browser

This is possible due to the `DOM` (Document Object Model). Client side JavaScript can access the browsers DOM and therefore can determine the URL used to load the current page.

The purpose of the `DOM` was to limit the amount of web requests going to a server and give the functionality to dynamically update the website without sending a request to the server. A script issues by an application may use information from the URL, and preform processing on this data and then update the page contents without sending out a request
### References:




