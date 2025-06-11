2025-03-17 02:21

##### Learning Covered:
- Determine what is NAT and PAT.
- Distinguish between NAT and PAT

--------------------------
Tags: [[NAT]] [[PAT]], [[IP]]


### Introduction to NAT and PAT
--------------------------------
##### It is IMPORTANT to note that NAT is a broad term and does not actually exist, only the different types of NAT such as Static, Dynamic and PAT

Without Network Address Translation (NAT) or Port Address Translation (PAT), we would not be able to utilize the internet

NAT or Network Address Translation is a broad term for technologies that allow private address to be converted in public addresses in order to combat the dimishing number of available public IP addresses.

NAT is split into 3 different categories':
- Static NAT
- Dynamic NAT
- Port Address Translation (PAT)

#### Static NAT
-------------
Static NAT is a NAT that is only used for a specific use case. In order to send a packet to a public address inside of a private address range, your NAT Technology (Router, Firewall, Server) has to convert the private address into a public. In Static NAT the private address is mapped to a singular public address, such as.  `192.168.1.15 -> 145.123.2.4`. Meaning that any packet with the source address will be replace with 145.123.2.4 and vice versa when coming back. 

This is problematic for most networks as it will require a large amount of Public IP address to allow all devices to access the Internet. That is where Dynamic NAT and PAT come into Play

#### Dynamic NAT
--------------------------
The main problem with Static NAT is that it only allows one IP to use the Public address. Dynamic NAT allows an infinite number of private address to use one public address by granting an public IP from a "Pool" when the packet crosses the router. The information of the IP mapping is stored in the router in the IP Translation Table and would look like this:

```
INSIDE | OUTSIDE
1.1.1.1  4.4.4.4
```

When the packet will come back, it looks up the destination address and replaces it with the relevant table entry. This allows the same public address to be utilized. But if not enough public addresses have been dedicated in the "pool" it can create congestion and some private address do not have current access to a public IP and must wait for it to become free.

#### Port Address Translation
--------------
PAT addresses and solve all of the issues with Static and Dynamic NAT. PAT records both the destination and source IP and PORT. When a packet is sent to the internet via the router, the router will record the private IP and PORT and map it to a singular public IP. But say 2 devices are using the same PORT, the router will use the next available port to continue the packet transaction . This means that multiple private IPs can use one public address at the same time by differentiating the different current address translations using PORTS.

Think of the following:

```
192.168.5.42:1337 -> 211.321.123.4:443
	PAT|
186.19.2.3:1337 -> 211.321.123.4:443
```

Here multiple session could be using the same public IP and could still work by separating them by PORT numbers. However any more sessions then there are PORT number will result in internet congestion and invalid requests