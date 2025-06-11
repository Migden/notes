2025-05-14 03:06

##### Learning Covered:
 - How to conduct Blind Boolean based SQLi
--------------------------
Tags:


### Boolean based injection
--------------------------------
The premise of Blind SQLi is to use features of SQL that do not rely on returning results to determine if information is true.

We can quickly compare if information is True by conducting a boolean comparison between the information requested and `1=1`. 

Such as `password' AND IF (1=1,sleep(3),'false'); -- `. This will compare `1=1` and the success of querying for the password. If the password is correct the application will sleep for 3 seconds, disregarding the need for the visual indication of success.

However we can do much more than just test the original query. We could check to see what passwords are in the database, and if the start of the result is `'a'` then 3 second delay, a continue for every character until dumped

### References:




