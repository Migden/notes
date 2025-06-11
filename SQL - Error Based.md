2025-05-12 07:46

##### Learning Covered:
 - Learn what Error Based SQLI is
--------------------------
Tags: [[SQL]]


### Identify SQLi via Error based payloads
--------------------------------
The principal of Error Based SQLi is that the SQLi has to be inband and displays the SQL error in some way for the attacker to see.

Error based SQLi works via implementing an incorrect syntax or command to purposely produce and error. This error message is typically very verbose and could be used to display information.

Purposely causing an error could result in the contents of a database being dumped if the payload is just right.

```sql
' or 1=1 in (select @@version) -- //
```

### References:




