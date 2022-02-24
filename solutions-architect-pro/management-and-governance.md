# Management and Governance

## Service Catalog
Managed service allowing users to deploy predefined workloads from a product catalog. 

- uses cloudformation templates
- integrates with ITSM systems (service now, Jira service desk, AWS Config)
- AppRegistry allows devs to deploy pre-built applications
- Manage license overrages with Cloudwatch > Step functions (not lambda) > dynamoDB > AWS License Manager

Cost
- Free tier (up to 1000 API calls)
- $0.0007 (14 calls for 1 cent) - us-east-1 & 2


References
- [AWS Service Catalog](https://aws.amazon.com/servicecatalog/?aws-service-catalog.sort-by=item.additionalFields.createdDate&aws-service-catalog.sort-order=desc)
- [Reference Architectures](https://github.com/aws-samples/aws-service-catalog-reference-architectures)

## Cloudtrail
- Audit trail of all changes made to infra and environment via API calls
- Supports logging on multiple regions with the `is-multi-region-trail` option. 
- Need to enable global for global services like `IAM`, `Cloudfront`, etc with `include-global-service-events` option

## Systems Manager: Patch manager

- Uses patch baseline (windows/linux/mac, when to apply, exceptions, patch source, auto-approve releases after configurable delay)
- auto-approving patches within days of their release
- whitelist/blacklist patches
- maintenance windows
- hybrid environments (cloud/on-prem)
- tag-based filtering (apply patches based on tags)

Patch groups: 
- groupings of instances to which to apply a patch baseline. Can create multiple, by environment for ex (Dev, QA, Prod)
- Requires a `tag` when creating. `key name is case-sensitive`. The tag is case-sensitive
- Add tag group in the Patch baseline section. Edit tag baseline patch group. 
- add `Patch Group` tag to instances. case sensitive! 

Maintenance Windows: 
- Set schedules for maintenance
- Supports maintenance tasks on other AWS resources like S3 buckets, SQS queues, KMS keys, etc. 
- has a schedule, a max duration, a set of registered targets


![](https://media.tutorialsdojo.com/sap_ssm_patch_group.png)

## AWS Config
- monitor and record state (previous versions) in your environment
- supports Multi-account, multi-region data aggregation

## Event Bridge
- serverless event bus
- make rules, define source, handler and targets (functions, sns topics)