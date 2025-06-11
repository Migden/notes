

[[Network Security]]

-----

### Configuring VPN connection over internet
-----
To create a VPN tunnel, several steps need to be carried out, this includes:
- Configure Access Control List
- Configure ISAKMP
- Configure transform-set IPsec
- Tie all information together using a crypto map
- Assign the crypto-map to an interface

A VPN tunnel can bypass restrictions such as IP destination filtering, since the packets have two IP addresses, one to a router and then an encrypted packet to the destined device a firewall will just forward to the router and then the router to the destination
##### Configure ACL
-------
To configure the ACL we need to specify the network addresses of the host and destination network as well as the relevant subnets.

`access-list 100 permit ip <local address> <local subnet mask> <desitnation address> <destination sbunet>`

This setup needs to be done in reverse on the destination network to enable traffic to be successfully sent over the tunnel

##### Configure ISAKMP
-----
ISAKMP is a protocol used to establish secure communication over the internet. You have to configure ISAKMP.

`crypto isakmp policy 10`
`encryption aes 256`
`authentication pre-share`
`group 5`

Then we need to set the secret key for the communication encryption and the `peer` router that is used to transmit these VPN packets
`cryptyo isakmp key <password> address <peer router interface address>`

##### Configure IPsec Transform-set
---
The transform-set is just the configuration for the IPsec protocol, in this setup we just define the algorithms used in the VPN tunnel.

`crypto ipsec transform-set <name> <encryption algorithms>`

##### Crypto Map
-----
A crypto map is just all the information curated above tied into a package of configuration.

`crypto map <name> <number> ipsec-isakmp`
`set peer <peer router address>`
`set pfd group5`
`set security-association lifetime seconds 86400`
`set transform-set <transform-set profile name>`
`match address <access list number>`

##### Assign Map to Interface
----
`crypto map <map name>`

##### Good Articles:
---
https://community.cisco.com/t5/security-knowledge-base/crypto-map-based-ipsec-vpn-fundamentals-negotiation-and/ta-p/3153502
https://www.youtube.com/watch?v=Z7LwU6H5IGE