
2025-05-08 06:19

##### Learning Covered:
- What is XML Path Language
- How can we exploit a vulnerability in XPATH
--------------------------
Tags:

### Injecting into XPath
--------------------------------
The XML Path Language (XPath) is an interpreted language used to navigate around XML documents and to retrieve data from within them.

Where web applications store data within XML documents, they may use XPATH to access the data in response to user input

Consider an XML data store:

```xml
<addressBook>
	<address>
		<firstname>william</firstname>
		<password>secret123</password>
	</address>
</addressBook>
```

To retrieve the `firstname` information utilising XPath would look like this:
`//address/firstname/text{}`

A query to return all that match is:
`//address[surname/text{}='william']`

### Subverting Application Logic
-----
Consider an application that retrieves a users details. Consider the XPath query looks like this:
`//address[firstname/text{}='william' and password/text{}='secret123']`.

If user input is not sanitized an attacker may be able to inject a `'or 'a'='a`. That would result in not needing correct authentication

### Informed XPath Injection
--------
XPath injection vulnerabilities can not just be used for authentication. Using comparisons we can get a Boolean response on results. We can use this to dump passwords

We can use a XPath feature called `substrings`, which can be used to reference individual indexes in a data store:
`//address[firstname/text{}='wiilliam' and substring(password/text{},1,1='A'] and 'a'='a`

The last `'a'='a` comparison is not needed for the query but just to ensure that the quotes for the input are correctly closed

Say there is more queries that don't allow us to get a successful authentication we can effectively `comment` out the remaining query to the right.

The way XPath executes the queries is similar to Oder of operations in that it is done in differing steps. Since the `AND` statement is rendered first we could add another `OR` statement to return it as true. Consider this.

`//address[firstname/text{}='william' and password/text{}='secret']`.

If we want to bypass the password check we could include the following in the username section:

`' or 'a'='a' or ''='`

This will first make the username to `True`, then do an `OR` comparison on the results of the password comparison and `1=1`. Effectively nullifying the password authentication but not truly `Commenting it out` 
### References:




