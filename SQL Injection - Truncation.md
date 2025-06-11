
-------
This challenge involved a website that had a register then admin login section.

The vulnerability this application held was not sufficiently implementing  authorization controls on administration accounts. Any account that had the name `admin` was given admin rights.

Utilizing `SQL Truncation`, we could inject a string `admin++++++++++test`, this would count as a new user and not a duplicate, but would be registered as `admin` due to it being truncated.

Then we could login as admin using our new password we registered with