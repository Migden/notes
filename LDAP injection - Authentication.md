
----

This called involved a Sign in page that used LDAP to validate password with a domain.

The first vulnerability was a verbose error message that when we injected the `)`, it return the full LDAP query in the error message

![[Pasted image 20250508035848.png]]

Since this is a conjunctive query, the results of both the queries need to be successful. We used a batched query that the original `AND` query would resolve into

```
username=*)(!(&(1=0
pasword=))
```

This payload created another query inside that when returned false would allow to original `conjunctive` query to be successful. We had to include the `(1=0` query as the username field appended a `)` to the end of our message and it would mess with the payload

