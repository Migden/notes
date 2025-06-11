2025-03-19 03:37

##### Learning Covered:

--------------------------
Tags: [[SNMP]], [[Active Information Gathering]]


### SNMP
--------------------------------
The Protocol Simple Network Management Protocol (SNMP) is not well understood by many network administrators. This often results in misconfigurations and information leaks.

SNMP is based on UDP, and is therefore susceptible to IP spoofing and replay attacks. Additionally the SNMP protocol version 1,2,2C offer no traffic encryption, meaning that SNMP information and credentials can be easily intercepted over a local network.

### SNMP MIB
-----------
The SNMP Management Information Base (MIB) is a file that states what information is being provided by the SNMP service and how to interpret the information, much like an API. A MIB will be given by manufactures when a product is purchased. The https://www.ibm.com/support/knowledgecenter/ssw_aix_71/commprogramming/mib.html contains a wealth of information about the MIB tree.

For example, the following MIB codes on the left will give use the information on the right.

```
|||
|---|---|
|1.3.6.1.2.1.25.1.6.0|System Processes|
|1.3.6.1.2.1.25.4.2.1.2|Running Programs|
|1.3.6.1.2.1.25.4.2.1.4|Processes Path|
|1.3.6.1.2.1.25.2.3.1.4|Storage Units|
|1.3.6.1.2.1.25.6.3.1.2|Software Name|
|1.3.6.1.4.1.77.1.2.25|User Accounts|
|1.3.6.1.2.1.6.13.1.3|TCP Local Ports|

```

### SNMP Enumeration
--------------
We can attempt to enumerate SNMP services by requesting a MIB for interesting data. However in order to get information we need to request the information utilizing the community string (password) which in most cases is `public`.

We can utilize a great tool called SNMPWALK to conduct our enumeration:

```bash
snmpwalk -c public -v1 -t 10 192.168.50.151
```


- Windows Users - 1.3.6.1.4.1.77.1.2.25
- running processes - 1.3.6.1.2.1.25.4.2.1.2
- Software installed - 1.3.6.1.2.1.25.6.3.1.2
- TCP ports - 1.3.6.1.2.1.6.13.1.3
### References:




