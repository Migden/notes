
---------

This challenge was quite advanced and I learnt a Fuck ton from this challenge

##### Key Learning Points
- Pay close attention to what you think the original query may be and think in terms of real-scenarios
- Blind Injection utilizes the `*` character to return a true character
- Python Scripting and Invalid characters from a python script including `#?&`
- In Python you can add an else statement for a `for` conditional to trigger is flow was redirected

First of all the website had a directory and login function, after entering some characters i realized that the login parameters where properly sanitized and while i didn't try bypasses, I assumed it was out of the scope of the challenge

The directory page gave the user an option to search for users on a domain.

I originally thought the query looked something like this.

`((email=<>))`

And I successfully did something on the server by injecting `admin)(password=test`. This did not return an error, i tried to trigger the response by injecting `admin)(1=1` but it didn't work. In hindsight this was a red flag as it tells that they where appending more then a `)` to our query, and later i found out it was appending `*<input>*`.

###### I should have assumed this due to the context of a search feature. It also explained why entering a `*` did not return all the users.

Now that i had found a parameter to brute force a made a script.

Originally this script tried to send every combination of characters under the sun, i think i was very tired or being stupid to think this.

I got confused then looked the solution up and found they used the appended `*` to return true if a character was at the start of the admin password.

I new this was how you did blind-injection but i failed to think properly. (Next time i need to give myself more time the think over speed)

Then i had issues with the script but it was due to my own faults (being bad logic, and not escaping bad characters). These errors stuffed with the script and made me more confused.

###### Next time i need to focus on the simple method before attempting to majorly change my script.

The script that returns the flag is as follows

```python
import string
import requests
import urllib.parse


URL = "http://challenge01.root-me.org/web-serveur/ch26/?action=dir&search=" 

password = ""
while True:
    for i in string.printable:
        response = requests.get(urllib.parse.quote(URL + "admin*)(password="+ (password+i)))
        if "admin" in response.text:
            password += i
            print(f"Password Starts With: {password}")
            break

print(f"Password = {password}")
```

