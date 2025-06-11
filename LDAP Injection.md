2025-05-08 02:47

##### Learning Covered:
 - Understand LDAP protocol
 - Exploit an application via LDAP injection
--------------------------
Tags: [[LDAP]]

### Injecting into LDAP
--------------------------------
The Lightweight Directory Access Protocol (LDAP) is used to access directory services over a network. A directory is a hierarchically organized data store that may contain any kind of information but is commonly used to store personal data such as names, telephone numbers, email addresses, and job functions.

`LDAP` is commonly used within Windows and Active Directory environments.

You can use `LDAP` to query for directory information.

Some basic query's look like:

Simple Match Conditions:
```
(username=aiden)
```

Disjunctive Queries: (Like and OR query if 1 data matches, it is returned)
```
(|(cn=searchterm)(sn=searchterm)(ou=searchterm))
```

Conjunctive Queries: (Like the AND query only if both terms match is a result returned)
```
(&(username=aiden)(password=secret))
```

### Exploiting LDAP injection
---------

It is possible to exploit LDAP injection similar to SQL injection in the principals of changing the original structure of the command.

##### Disjunctive Queries

A disjunctive query on calls for 1 term in the query to be true to return results. Say the application is putting unsanitized data into the LDAP query. We could submit a input like:

```
aiden)(department=*
```


##### Conjunctive Queries

Some LDAP implementations allow multiple search filters to be batched, and these are applied disjunctively.
So an input like this may work for LDAP injection:

```
*)(&(giveName=daf
```

##### Injecting NULL bytes

A NULL byte injected into a LDAP query will terminate any commands to the right, much like a comment in SQL.
### References:
https://www.brightsec.com/blog/ldap-injection/



