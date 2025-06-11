
-------
This challenge involved a website that contained a search function to retrieve information. We found a SQL injection vulnerability by inserting the character `'` and where given an error.

I assumed that it was doing somthing similar to this:

```SQL
SELECT * FROM web_pages WHERE name="test"
```

In this case we would be able to end the query and start a UNION clause to dump information from `sqlite_master`

We got the number of rows returned via `' ORDER BY 1;-- `

Found out it was returning 2 rows.

Then dumped the names of tables using the payload: `' UNION SELECT table_name, NULL FROM sqlite_master;-- `

Then guessed the column names and got the passwords for the application: `' UNION SELECT username, password FROM users;-- `

