# Security

## AWS Shield Advanced
- includes **notifications** for incoming Layer 3 or Layer 4 attacks such as SYN floods and UDP reflection attacks. Shield standard doesn't include notification. 

## Lightweight Directory Access Protocol (LDAP)
See [IAM](./iam.md)

## AWS Key Management Service (KMS)
- customer managed or AWS managed
- AWS managed: generic on customer's behalf. 
- Customer managed: key material can be imported. More control options. 

References: 
- https://docs.aws.amazon.com/whitepapers/latest/kms-best-practices/aws-managed-and-customer-managed-cmks.html

## Firewall Manager
- centrally manage firewall or WAF rules across many accounts
- requires Organizations to share web ACL across member account WAF's. 