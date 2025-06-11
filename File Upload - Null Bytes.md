
----
This challenge involved a photo board that was taking in user uploaded images and rendering them.

We found that it was not checking `magic bytes` but only checking the extension.

If the application is checking the end of the file only and not running canonicalized checks, if we insert the null byte after the `.php` and before the `.jpg`. The server will allow as it has the extension `.jpg`, but it will be truncated to `.php` only
