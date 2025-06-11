2025-05-14 02:43

##### Learning Covered:
 - What are HTTP Verbs
 - What is HTTP Verb Tampering
--------------------------
Tags: 


### HTTP Verbs
--------------------------------
`HTTP Verbs` or commonly know as `HTTP Methods`, each web request has a method that specifies to the web application what they plan to do.

The list of `HTTP Verbs` is:
- GET
- HEAD
- POST
- PUT
- PATCH
- CONNECT
- OPTIONS
- TRACE
- DELETE

All of which describe different functions such as submitting a form or just reloading a web page. By default some of these methods could pose a security risk such as `DELETE`, or `PATCH`. And may `HTTP Verbs` are disabled by default

### HTTP Verb Tampering
-------
The basis of `Verb Tampering` is to change the `HTTP Method` to bypass Authentication and Authorization features.

An example would be only Admins can submit a `GET`, or `POST` request. But if other methods are still enabled by default, a non-Admin may use the `HEAD` method to access the un-authorized areas.

### References:




