
---------------

This challenge involved a website that had a sign in feature, from the challenge name I considered XPath injection. 

I was easily able to gain authentication as a `member` utilising a simple payload `'or 'a'='a`.

However this challenge required logging in as an `admin`. I tried the payload `'or 'a'='a` on the password and the username of the admin `john`. But it did not work (Don't Known Why).

I did more research into the XPath injection and found out a way to effectively `comment` out the rest of the query. This was of no help, but in reading up on it I found out that the payload was automatically making the user sign in as the first in the table. Reading on the `"comment"` feature i discovered that if i false or comparison with the username it would not default to `steve` but to the original username in the query.

