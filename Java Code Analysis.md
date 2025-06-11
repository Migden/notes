
---------

This is a challenge provided by PicoCTF at the medium difficultly.

This challenge involved a bookstore application that displayed books. This challenge gave us the source code.

From the source code we could see the website was using a JWT token to get information about the user to then conduct authorization based on the JWT values.

![[Pasted image 20250507062408.png]]

We checked to see if the JWT secret was hard coded, and yes it was! The server was utilising a poor JWT secret that was hard coded. Even if we didn't have access to the source code we would be able to crack the JWT token.

![[Pasted image 20250507062601.png]]

We then utilize the JWT Secret to modify JWT tokens and give ourselves the role of `Admin`. With this role i still was not able to access the flag as it came up as an unknown error. So i had to think. What i was thinking was that they where doing some type of semantic check on the JWT cookie (Comparing email with role) so it would not actually let me view the flag as i was not truly admin. 

However, we could access an admin dashboard and from there we upgraded a second account we made to have admin privileges. This seemed to have worked

```
picoCTF{w34k_jwt_n0t_g00d_7745dc02}
```