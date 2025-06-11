2025-03-18 05:16

##### Learning Covered:

--------------------------
Tags: [[SMTP]], [[Active Information Gathering]]


### SMTP Enumeration
--------------------------------
We can also gather information about a host or network from vulnerable mail servers. The Simple Mail Transport Protocol (SMTP) supports several interesting commands such as VRFY and EXPN.

A VRFY request asks the server to verify an email address, while EXPN asks the server for the membership of a mailing list

These Keywords can be utilized to gain useful information during an penetration test.

```bash
kali@kali:~$ nc -nv 192.168.50.8 25
(UNKNOWN) [192.168.50.8] 25 (smtp) open
220 mail ESMTP Postfix (Ubuntu)
VRFY root
252 2.0.0 root
VRFY idontexist
550 5.1.1 <idontexist>: Recipient address rejected: User unknown in local recipient table
^C
```

We can see here that it will verify if a user exists on the mail server.

Similarly, we can obtain SMTP information bout our target from the Windows client

```powershell
Tests-NetConnection -port 25 192.168.50.8
```

Unfortunately the Test-NetConnection prevents us from fully interacting with the SMTP service. Nevertheless, if not installed we can install the Microsoft version of telnet:

```powershell
dism /online /Enable-Feature /FeatureName:TelnetClient
```
This will require admin privileges but if you have the binary you can file transfer from another machine if possible.

Then just use telnet as usual
### References:




