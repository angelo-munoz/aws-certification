# Networking

### Transit VPC's
A network design allowing multiple networks/VPC's to connect and communicate over a shared network. Similar to hub and spoke model. 
![](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/images/image23.png)

**Design:**
- No single point of failure. 99.99 availability w 2 AZ's and redundant VPN links to each router 

**Advantages:** 
- Can be used for NAT for overlapping IP's
- Use network packet inspection. https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/transit-vpc-option.html

**Alternatives**
- [Transit gateway + Direct Connect](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect-aws-transit-gateway.html), [AWS Cloud hub](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-vpn-cloudhub.html)


### Ethernet bridging
Combining multiple ethernets to act a single subnet. https://openvpn.net/community-resources/ethernet-bridging/

### Amazon time sync service
Amazon time sync service. Accessible at 169.254.169.123. https://aws.amazon.com/blogs/aws/keeping-time-with-amazon-time-sync-service/