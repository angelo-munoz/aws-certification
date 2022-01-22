# AWS Organizations

- Service control policy (SCP) types: approve/deny policies
  - approve: whitelist. you approve max services accounts can access. everything else not allowed
  - deny: blacklist. you deny services accounts can access. everything else approved. 
- SCP's don't apply to management (master) accounts
- SCP's apply to all member account users, including root accounts
- Orgs integrate with stack sets for cross-region automation
- Benefits: consolidated billing, centralized account mgmt, centralized security
- AWS Quotas integration

## References
- [Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
- [Establishing your best practice AWS environment](https://aws.amazon.com/organizations/getting-started/best-practices/)
- [Best Practices for Organizational Units with AWS Organizations](https://aws.amazon.com/blogs/mt/best-practices-for-organizational-units-with-aws-organizations/)