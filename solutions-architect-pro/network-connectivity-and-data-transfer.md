# Networking

## Direct Connect
- Direct connection to AWS using the AWS backbone network
- Connection options: from 50 Mbps to 100 Gbps
- Encryption available using MACSec (built-in) OR IPsec VPN (separate)

## Direct Connect Gateway
- Connect VPC's across regions
- Several VPC's share the same direct connect
- See this megaport article for a comparison: [DGW vs VPG vs TGW](https://www.megaport.com/blog/aws-vgw-vs-dgw-vs-tgw/)
![](https://www.megaport.com/wp-content/uploads/2020/02/awstable1.png)

**References**:
- https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-gateways-intro.html

## Transit VPC's
A network design allowing multiple networks/VPC's to connect and communicate over a shared network. Similar to hub and spoke model. 
![](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/images/image23.png)

Design:
- No single point of failure. 99.99 availability w 2 AZ's and redundant VPN links to each router 

Advantages:
- Can be used for NAT for overlapping IP's
- Use network packet inspection. https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/transit-vpc-option.html

Disadvantages:
- High maintenance cost (not managed) 

Alternatives:
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

Reference: 
- https://docs.aws.amazon.com/vpc/latest/userguide/VPC_DHCP_Options.html

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

## DNS
Domain Name System. Route53
- Port 53

**Private hosted zones**
- Internal DNS for VPC's
- create custom internal domains
  > VPC's `enableDnsHostnames` and `enableDnsSupport` attributes must be set to `true`
- `Split-view DNS`. Use same domain for internal and external DNS
- Amazon-provided DNS server is at base of network plus 2. Ex: For the `10.0.0.0/16` network, the DNS will be at `10.0.0.2`. So interesting! did not know this before! 

**Cross-account VPC's using a private hosted zone**

- In VPC A (that owns the private hosted zone), create a VPC association authorization using CLI `create-vpc-association-authorization`
- In VPC B (with resources trying to use Route53), create a VPC association using CLI.
- (*optional*). Remove the association authorization for security?

References: 
- https://aws.amazon.com/premiumsupport/knowledge-center/route53-private-hosted-zone/
- https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/hosted-zone-private-associate-vpcs-different-accounts.html


## Route53 Resolver
DNS service for **hybrid** environments (onprem/cloud)
- `Inbound`: originates from onPrem to lookup VPC resources
- `Outbound`: 
  - originates from VPC to lookup onPrem resources
  - uses `conditional forwarding rules`: forwards request to onPrem DNS
- Recursive DNS: one DNS server queries other DNS server to find the right IP address. See [Recursive DNS](https://www.cloudflare.com/learning/dns/what-is-recursive-dns/)

![](https://d2908q01vomqb2.cloudfront.net/da4b9237bacccdf19c0760cab7aec4a8359010b0/2018/11/19/resolver-1-howitworks-3.png)

References: 
- https://aws.amazon.com/blogs/aws/new-amazon-route-53-resolver-for-hybrid-clouds/

## Shared VPC
- Efficient way to share network resources (subets) across multiple accounts, or an organization. 
- Decouple accounts and networks
- Use Resource access manager (RAM) to share subnets, etc
- Use when need to centrally manage network resources (by a single team for example)

Benefits: 
- Separation of duties: centrally controlled VPC structure, routing, IP address allocation.
- Application owners continue to own resources, accounts, and security groups.
- VPC sharing participants can reference security group IDs of each other.
- Efficiencies: higher density in subnets, efficient use of VPNs and AWS Direct Connect.
- Hard limits can be avoided, for example, 50 VIFs per AWS Direct Connect connection through simplified network architecture.
- Costs can be optimized through reuse of NAT gateways, VPC interface endpoints, and intra-Availability Zone traffic.

References: 
- https://docs.aws.amazon.com/vpc/latest/userguide/vpc-sharing.html
- https://aws.amazon.com/blogs/networking-and-content-delivery/vpc-sharing-a-new-approach-to-multiple-accounts-and-vpc-management/

## Private Link
- Creates private connection bw your VPC and another service using the AWS network (private connection - no need for internet)
- Faster, more reliable connections
- More secure. Don't have to traverse internet

## Interface Endpoints
- use private link under the hood
- creates 2 ENI's across 2 of your subnets, and security group applied to them
- routes traffic through those ENI's using NAT
- assumes overlapping IP's so uses NAT under the hood
- Specific to: AWS Service (EC2, S3, etc), Marketplace, PrivateLink Ready partner services, custom endpoint services (search by name)

## Cloudfront
- Content delivery
- Geo restriction
  - based on country. 
  - **use 3rd party if need more granular than country**
- Custom origins: load balancer, pass-through headers
