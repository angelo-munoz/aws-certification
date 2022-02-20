# AWS Organizations

- Service control policy (SCP) types: approve/deny policies
  - approve: whitelist. you approve max services accounts can access. everything else not allowed
  - deny: blacklist. you deny services accounts can access. everything else approved. 
- SCP's don't apply to management (master) accounts
- SCP's apply to all member account users, including root accounts
- Orgs integrate with stack sets for cross-region automation
- Benefits: consolidated billing, centralized account mgmt, centralized security
- AWS Quotas integration
- Use trusted service principals to allow services to access your organization or perform work on its behalf
- To exclude reserved instances, in billing console, add the account to the excluded reserved instances sharing

### SCP exceptions: 
1. Only **accounts** created after Sept 15, 2017 can control these actions with SCP's. That is, accounts before this date cannot control these actions with SCP's: 
    - Enable or disable multi-factor authentication on the root user
    - Create, update, or delete x.509 keys for the root user
    - Change the root user's password
    - Create, update, or delete root access keys


### References
- [Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
- [Establishing your best practice AWS environment](https://aws.amazon.com/organizations/getting-started/best-practices/)
- [Best Practices for Organizational Units with AWS Organizations](https://aws.amazon.com/blogs/mt/best-practices-for-organizational-units-with-aws-organizations/)