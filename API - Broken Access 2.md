
---------
This API allows for notes to be created, once signed in the server gives you two identifiers. A `cookie`, and a JSON value of `secret` with some string attached.

I'm thinking that the session identifiers have been generated insecurely.

After further reconnaissance we can read when other users have created their accounts, their name and id

potentially we could craft a new identifier for the user, and authenticate with our already established cookie.