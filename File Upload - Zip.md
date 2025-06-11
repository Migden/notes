
------
Tags: [[Symbolic Links]]

This challenge involved a site that would give an unzipped contents for download. When a zip file is passed it would unzip it in a safe way in that you couldn't execute it.

How ever i found an interesting article on `Zip Slips`, which in effectiveness is when you upload a zip with a file called `../../../../../../etc/passwd`. This would replace the file once unzip at the location.

Originally I thought that this would be the solution but couldn't create a file name including a path. But it did not work.

I had to search the answer as i was genuinely confused.

The solution included a zipped `symbolic file` that pointed to `index.php`. When the zip was unzipped the file was placed on the server, but it was actually a `symbolic link` to the website source code.

