2025-03-08 03:58

##### Learning Covered:
- Conduct enumeration on the DNS service
--------------------------
Tags: [[DNS]], [[Active Information Gathering]]


### DNS
--------------------------------
The Domain Name System is a distributed database responsible for translating user-friendly domain names into IP addresses. This is facilitated by a hierarchical structure that is divided into zones, starting with the top level zone

Each Domain can used different types of DNS records. Some of the most common include:
- NS - Nameserver records contain name of the authoritative servers hosting the DNS records for a domain
- A - Contains the IPv4 address of the Hostname
- AAAA - Contains IPv6 address of the Hostname
- MX - Contains the names of the servers responsible for handling email for the domain
- PTR - Pointer records are used in a reverse lookup to transfer the records for an IP address
- CNAME - Canonical name records are used to create aliases for other host records
- TXT - Text records can hold any random data for any purpose

Due to the large amount of information in DNS it is a great starting point for active information gathering


### DNS Enumeration
----------
Some commands that can be used to enumerate DNS include:
- `host www.megacorpone.com`
- `host -t mx megacorpone.com`
- `host -t txt megacorpone.com`
- `host idontexist.megacorpone.com` - returns if it is a valid subdomain

We can automate subdomain discovery utilizing tools such as Dirbuster, or DNSenum

A windows alternative LOLbins is the `nslookup command`:
	`nslookup -type=TXT info.megacorptwo.com 192.168.50.151`

`IMPORTANT`, the DNS records will be taken from the default DNS server, other DNS servers can have different records you can query specific DNS server by asking for results from a specific host

### References:




