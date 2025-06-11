2025-03-07 03:59

-------------------
Security Headers are directives return by the web server that tell the browser to load the website using proper methods to ensure security, some headers that are used consist of:

- Content Security Policy (CSP)
- X-Frame-Options


### Content Security Policy (CSP)
------------
The CSP is a feature that helps to prevent pr minimize the risk of certain security threats. It is mainly used in the defense against [[XSS]] attacks and defending against click jacking.

It works by providing directives on where content from the page is loaded from, it typically has the format of the following:

```html
Content-Security-Policy: default-src 'self'; img-src 'self' example.com
```

The first directive "default-src" tells the browser to load only resources that are from the same origin with the document. The "img-src" tells the browser to load images that are same origin or served from "example.com"

If sanitization does fail, there are various forms the injected malicious code can take in the document, including:

- A [`<script>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script) tag that links to a malicious source:
    
    
    ```html
    <script src="https://evil.example.com/hacker.js"></script>
    ```
    
- A `<script>` tag that includes inline JavaScript:
    
    
    ```javascript
    <script>
      console.log("You've been hacked!");
    </script>
    ```
    
- An inline event handler:
    
    
    ```html
    <img onmouseover="console.log(`You've been hacked!`)" />
    ```
    
- A `javascript:` URL:
    
    
    ```html
    <iframe src="javascript:console.log(`You've been hacked!`)"></iframe>
    ```
    
- A string argument to an unsafe API like [`eval()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval):
    
    
    ```javascript
    eval("console.log(`You've been hacked!`)");
    ```
    

A CSP can provide protection against all of these. With a CSP, you can:

- define the permitted sources for JavaScript files and other resources, effectively blocking loads from `https://evil.example.com`
- disable inline script tags
- allow only script tags which have the correct nonce or hash set
- disable inline event handlers
- disable `javascript:` URLs
- disable dangerous APIs like `eval()`

In conclusion it provides another layer of defense when protecting your website against cyber threats


### X-Frame-Options
-------------
The `X-Frame-Options` header indicates weather a browser should be allowed to render another page in their site using methods such as `<Frame>`, `<iframe>`, `<embed>`. 

The header prevents it from being loaded, therefore preventing clickjacking from malicious content loaded into the webpage such as a scam advertisement