
----------
This challenge was tough, it involved a simple web application with a sign in functionality hinting that it was utilising some kind of database.

Upon further examination, we found a parameter called `order`, injecting into this parameter produced an error and told me that SQL injection was possible. However this parameter did not return any values of the original query stating `no authorization`, however i thought that Error based injection may be a good idea due to the fact that error messages where produced but a successful query was not.

To start of i found the the parameter i was injecting was at `SELECT * FROM page ORDER BY <>;`. After some research on this functionality, it was revealed that you could order by different columns in the table so i could add an additional instruction

`, CAST((SELECT version)AS numeric)`

BY casting the `version` to integer an error occurred displaying the version. Now all we had to do was dump the schema and get the tables and columns of the sign-in database.

`CAST((SELECT table_name FROM information_schema.tables) AS numeric)`

`(CAST(( SELECT column_name FROM information_schema.columns WHERE table_name=chr(109)||chr(51)||chr(109)||chr(98)||chr(114)||chr(51)||chr(53)||chr(116)||chr(52)||chr(98)||chr(108)||chr(51) LIMIT 1 OFFSET 1)AS numeric)`

I encountered an issue, only one column could be printed that where the `OFFSET` command comes in handy, i could print the column in the results at a certain offset to ensure that only 1 column is printed and a error does not occur.

Then all i had to do was dump the password:

`(CAST((select p455w0rd_c0l FROM m3mbr35t4bl3 LIMIT 1 OFFSET 0)AS numeric))`

###### KEY LEARNING OBJECTIVES:
- Incorrect type-casting shows an error of the resolved object to cast
- You can replace strings with `chr()` and the ascii code
- You can use `LIMIT` and `OFFSET` to control what data you return