2025-05-31 06:40

##### Learning Covered:
- Understand the HSRP protocol
- Understand the EIGRP Protocol
--------------------------
Tags: 


### HSRP Overview
--------------------------------
HSRP or `Hot Standby Router Protocol` allows multiple routers to appear as one by assigning a `virutal IP (VIP)` and matching `Virtual MAC Addresses`

HSRP protocol elects one node in the list of routers in the HSRP to be active, while the rest of the routers wait for the failure of the elected node

###### HSRP communicates of UDP Port 1985


### HSRP Configuration
----
HSRP protocol configuration is done on the exposed interface.

Once you are in the interface conduct the following:
- Enter `standby version 2`
- Enter `standby <group number> <VIP>`
- Enter `standby priority <priority (Higher number better priority)>`
- Enter `standby preempt` On router regeneration it will assume previous role

### EIGRP Overview
----
EIGRP is a routing protocol that is used to increase network efficiency. It is similar in application to OSPF but utilizes a different algorithm to obtain its information

### EIGRP Configuration
----
The EIGRP protocol works by mapping the network by nodes describing what information they can reach, multiple different EIGRP instances can be run at the same time in groups.

Basic configuration goes as follows:
- `conf t`
- `router eigrp <group identifier>`
- `network <network address> <subnet mask>`
- Repeat above steps for all interfaces that are relevant
- Do on all router

### References:




