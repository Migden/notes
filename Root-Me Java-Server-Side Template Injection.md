
---------
After entering the string `${7*7}` we can confirm that a SSTI vulnerability is present.

After testing against the image above to detect the engine, we did not find it. I then resorted to searching online for potential java engines and how to exploit, i then came across this site: https://medium.com/@bdemir/a-pentesters-guide-to-server-side-template-injection-ssti-c5e3998eae68

I used the payload: `<#assign command="freemarker.template.utility.Execute"?new()> ${ command("cat /etc/passwd") }` to successfully read `/etc/passwd`