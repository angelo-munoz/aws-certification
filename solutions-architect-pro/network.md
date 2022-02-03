# Networking

## Transit VPC's
A network design allowing multiple networks/VPC's to connect and communicate over a shared network. Similar to hub and spoke model. 
![](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/images/image23.png)

**Design:**
- No single point of failure. 99.99 availability w 2 AZ's and redundant VPN links to each router 

**Advantages:** 
- Can be used for NAT for overlapping IP's
- Use network packet inspection. https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/transit-vpc-option.html

**Disadvantages**
- High maintenance cost (not managed) 

**Alternatives**
- [Transit gateway + Direct Connect](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect-aws-transit-gateway.html), [AWS Cloud hub](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-vpn-cloudhub.html)


## Ethernet bridging
Combining multiple ethernets to act a single subnet. https://openvpn.net/community-resources/ethernet-bridging/


## DHCP Option sets
VPC setting to change DHCP options for instances launched in that VPC. 
Options: 
- DNS
- NTP
- Domain name
- Net bios node servers
- Net bios node type

Reference: https://docs.aws.amazon.com/vpc/latest/userguide/VPC_DHCP_Options.html

## NTP
[Network Time Protocol (NTP)](https://en.wikipedia.org/wiki/Network_Time_Protocol) is used for time sync bw systems. 
- UDP port 123. 
- Amazon time sync service. Accessible at 169.254.169.123. https://aws.amazon.com/blogs/aws/keeping-time-with-amazon-time-sync-service/

## MPLS network
[Multiprotocol label switching](https://en.wikipedia.org/wiki/Multiprotocol_Label_Switching) is a routing protocol that uses packet labels to route traffic at layer 2.5 (not 2 or 3) instead of the layer 3 routing like OSPF, EIGRP. 

References: 
- Micro nugget youtube. [MPLS explained](https://www.youtube.com/watch?v=huKkCK8AJ7I&t=1s)

## Elastic Network Interface
- AWS Network card
- created/managed separate from instance
- **same AZ as instance**
- can have multiple ENI per instance (1 primary and multiple secondary)
- Each ENI can have multiple IP addresses

References: 
- [Elastic network interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html)