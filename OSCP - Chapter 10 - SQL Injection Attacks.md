2025-05-12 07:37

##### Learning Covered:
- SQL Theory and Database Types
- Manual SQL Exploitation
- SQL Attack Automation
--------------------------
Tags:


### DB Types and Characteristics
--------------------------------
When testing a web application, we sometimes lack prior knowledge of the underlying database system, so we should be prepared to interact with different SQL database variants.

In this unit we will focus on 2 different Databases:
- MySQL
- MSSQL

##### MySQL
MySQL is one of the most deployed database variants, along with MariaDB.

We can `connect` to a MySQL instance with the following command:
`mysql -u root -p'root' -h 192.168.0.1 -p 3306`

Show `Version`:
`select version();`

Show current `database user`:
`select system_user();`

Show `Databases`:
`show databases;`


##### MSSQL
MSSQL is a native windows application that integrates into the windows environment. Due to this fact we can't directly connect via a traditional means on a Linux host, instead we use a program called `impacket-mssqclient`

We can connect to an instance using this command:
`impacket--mssqlclient Administrator:Lab123@192.168.1.1 -windows-auth`

Show `Version`:
`select @@version;`

Show `databases`:
`SELECT anem FROM sys.databases;`

Show `tables`:
`SELECT * FROM offsec.information_schema.tables;`

List `table contents`:
`SELECT * from offsec.dbo.users;`

### Identifying SQLI via Error-based Payloads
----
 [[SQL - Error Based]]

### UNION-Based Payloads
----
[[SQL - UNION Based]]
### References:




