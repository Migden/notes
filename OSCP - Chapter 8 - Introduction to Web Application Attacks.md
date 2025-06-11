2025-04-12 05:33

##### Learning Covered:
- Web Application Assessment Methodology
- Web Application Enumeration
- Cross-Site Scripting

--------------------------
Tags: [[OWASP]], [[NMAP]], [[Proxy]], [[Gobuster]], [[API]], [[Headers]], [[XSS]]


## Web Application Assessment Methodology
--------------------------------
##### Learning Objectives
- Understand web application security testing requirements
- Learn different types and methodologies of web application testing
- Learn about the OWASP Top 10 and most common web vulnerabilities

As a penetration tester, we can asses a web application using three different methods. These include:
- White Box
- Grey Box
- Black Box

### Web application Assessment Tools
---
#### 2.1 Fingerprinting Web Servers with NMAP

NMAP is a go-to tool for initial active enumeration. We can rely on the NMAP Service Scan to grab the web server banner. 
```
nmap -p 80,433 -sV test.com 
```

To take our enumeration to the next level we can use service specific Nmap NSE scripts like, *http-enum*, which preforms an initial fingerprinting on the web server.

```
nmap -p 80,433 --script=http-enum test.com
```

#### 2.3 Directory Brute Force with Gobuster

Once we have discovered an application running on a web server, our next step is to map all its publicly accessible files and directories. To do this we would need to preform multiple queries against the target to discover any hidden paths.

```
gobuster
```

### 8.3 Web Application Enumeration
-------
It is important to identify the components that make up a web application before blindly trying to exploit it. Before launching any attacks we should attempt to discover the technology stack in use. Such as operating system, server software, database software, and frontend/backend programming.

#### Inspecting HTTP Response Headers and Sitemaps

We can also search the server responses for additional information. There are two types of tools we can use to accomplish this. One is a Proxy, like BurpSuite, and the other is the browser's own *Network* tool.

Headers are directives given by or too the web server. However not all of them are generated soly by the web server. For instance Web-Proxies actively insert the *X-Forwarded-For* header to signal the web-server about the original clients IP address.

*Sitemaps* are another important element we should take into consideration when enumerating web applications. Web applications can include sitemaps to help search engine bots crawl and index their sites. These sitemaps will also include directives of URLs not to crawl. This information is typically stored in the `robots.txt`, or `sitemap.xml` files

#### Enumerating and Abusing APIs

In many cases our penetration test target is an internally built, closed-source web application that is shipped with a number of APIs. These APIs are responsible for interacting with the back-end logic and providing a solid backbone of functions to the web application.

We can use Gobuster features to brute force the API endpoint.

API paths are often followed by a version number resulting in a pattern such as:

```
/api_name/v1
```

The API name is often quite descriptive about the feature or data it uses. With this information, we can try to brute force an API path using a wordlist.  To do this efficiently we can use fuzzers, or utilize the Gobuster pattern feature

```bash
vim pattern
{GOBUSTER}/v1
{GOBUSTER}/v2

gobuster dir -u http://test.com -w /usr/share/wordlists/dirb/big.txt -p pattern
```

A typical API will return some features such as:
- users/v1
- notes/v1

It is important to fully map out an API as they normally have features included in the REST API paths such as `/user/v1/login`.

It is important to pay attention to any documentation and response codes or irregular response from the server to determine avenues of enumeration and attack.

### Stored and Reflected XSS
----------
[[Stored and Reflected XSS]]
##### Malicous WordPress Plugins

### References:




