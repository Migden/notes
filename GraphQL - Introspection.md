
------
This challenge involved a page that displayed information about rockets currently outside of earth from different countries.

I found that the server was using GraphQL via hardcoded JavaScript that sent data to a GraphQL endpoint.

Hence the challenge name, I started a script called `clairvoyance` to complete introspection on the GraphQL enpoint, and found a Type Object called `IAmNotHere`.

The command to list the different type objects is:

```JSON
query {
	__schema {
		name
	}
}
```

Once we noticed the object i started to list the fields of the object type:

```JSON
query {
	__type(name: \"IAmNotHere\") {
		fields {
			name
			description
		}
	}
}
```

This gave the name and description of all fields for `IAmNotHere`.

After attempting to retrieve these fields, it gave me an error `argument "very_long_id" of type "int" is required, but not provided`, this meant that a `id` parameter is to be passed for the object type `IAmNotHere`.

After fuzzing the parameter the id of `18` return the challenge flag.

This was the final payload:

```JSON
query {
	IAmNotHere(very_long_id: 18) {
		very_long_value
	}
}
```

