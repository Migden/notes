2025-05-15 03:14

##### Learning Covered:
- The basics of GraphQL
--------------------------
Tags:


### The Basics
--------------------------------
`GraphQL` is an open source data query an manipulation language for application programming interfaces. Unlike other API formats, `GraphQL` allows an API consumer to request specific data from the application sever without receiving unnecessary information. The format is much like an XML and XPATH query.

![[Pasted image 20250515031710.png]]

As you can see, you can request more information than a standard REST query, such as the `firstname` and `lastname` field, instead of requesting an entry `1`. This provides greater security, as there is less chance that data that shouldn't be returned is returned.

In larger applications GraphQL can have a noticeable effect on performance and bandwidth. Instead of having to return a whole class of information we could return just what is needed. I think of it as a step up in efficiency from web request > rest request > GraphQL request


### How Does Communication Work?
-------
A typical GraphQL implementation incorporates a few components.

When a client wants to communicate with a GraphQL server, to read a list of usernames and emails, that client will use a HTTP POST request to send the server a GraphQL query. This seems non-standard but it is because we are sending `JSON` in every request to the GraphQL server.

The server will then process the query using a `query parser` to read and validate the query is correct and properly formatted.

Then the server checks the query against the GraphQL `Schema`.

If the query is deemed valid, it will be sent to the `resolver functions`, which send the query to where it needs to go, such as a MySQL server

##### The Schema
The GraphQL `schema` represents the type of data the client can query for.

`Object` types are the most basic component of a GraphQL schema; They represent a piece of data you can fetch from the service.


```
type User { 
	username: String 
	email: String 
} 

type Location { 
	latitude: Int
	longitude: Int 
}

```

The `Object Type` "Location" as two fields `latitude, and longititude.`

GraphQL also allows for us to form links between objects, much like inheritance, we can represent our schema as a graph consisting of `nodes` and `edges`.

The `nodes` are objects. And the `edges` are the link between nodes.

For example, an `object` could have a field that references another object.

```
type User {
	username: String
	email: String
	location: Location
}

type Location {
	latitude: Int
	longtitude: Int
}
```


##### Queries
Once and APIs schema is defined, clients can fetch information from it by using queries written in the GraphQL query language.

All `queries` begin with a definition of the operations `root type`, which specifies different operations
- Query - Read-Only operations
- Mutation - Data Manipulation (deletion, addition)
- Subscription - Real-time communication between clients and server

However a developer must define the operations allowed by the user in the schema and specify the fields that clients can access

An Example Schema will help explain:

```
type User {
	username: String
	email: String
}

type Query {
	user: [User]
}

schema {
	query: Query
}
```

If this above example, we define that the `query` field points to the `Query` object, and the `Query` object has a field `user`, that points to the object `User`. And it also defines that this `User` object returns an array of information.

This effectively means that a `query` query only has an edge with the `User` object and other objects can't be accessed utilising the `query` query.

A user may submit a GraphQL query as such:
```
query {
	users {
		username
		email
	}
}
```

###### Just think of this request as and object accessing child-objects and the child-objects fields.

The structure and layout makes it much harder for developers to introduce vulnerabilities but will prevent readability in some cases. And could also introduce vulnerabilities.
### References:




