
----
This challenge involved a NGINX server that was incorrectly configured to do the function `try_files` on any `URI` for the web root.

This paired with the fact that the base root was `/etc/nginx`. Allowed us to read the NGINX config to get the flag.

The `try_files` does not allow directory traversal but simply looks for files from the web root which was conveniently `/etc/nginx`