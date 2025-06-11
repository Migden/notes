2025-03-18 03:48

##### Learning Covered:
- Learn how to enumerate SMB for valuable information

--------------------------
Tags: [[SMB]] [[Active Information Gathering]], [[NetBIOS]]


### SMB Enumeration
--------------------------------
SMB has a very poor track records due to several critical security vulnerabilities to WinBlue and unauthenticated SMB Null sessions.

Keeping this in mind SMB has also been updated and improved in parallel with windows releases.

The [NetBIOS] service listens on TCP port 129, as well as several UDP ports. SMB and NetBIOS are two separate protocols. NetBIOS is a session layer protocol and service that allows computers on a local network to communicate with each other. In newer version NetBIOS is not required but is often required for backwards compatibility

You can scan SMB and NetBIOS utilizing tools such as NMAP, but for more specialized information a tool such as `nbtscan` can be used to find valid NetBIOS host names.

```bash 
kali@kali:~$ sudo nbtscan -r 192.168.50.0/24
Doing NBT name scan for addresses from 192.168.50.0/24

IP address       NetBIOS Name     Server    User             MAC address
------------------------------------------------------------------------------
192.168.50.124   SAMBA            <server>  SAMBA            00:00:00:00:00:00
192.168.50.134   SAMBAWEB         <server>  SAMBAWEB         00:00:00:00:00:00
...
```

This scan reveals two NetBIOS hostnames that could give us further insight into what the purpose of these two hosts are.

NMAP also provides useful NSE scripts that we can use to discover and enumerate SMB services.

``` bash
nmap -v -p 139,445 --script smb-os-discovery 192.168.50.152
```

For Windows Clients, we can use the command `net view`

```powershell
net view \\dc01 /all

```

`NetExec (Formerly CrackMapExec)`

```bash
netexec smb 192.168.154.20 -u "alfred" -p "" --shares
```


### References:
https://0xdf.gitlab.io/cheatsheets/smb-enum
https://www.youtube.com/watch?v=Qn-2XQ-0wLg


