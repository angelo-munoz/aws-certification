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

## Systems Manager: Session Manager
- connect to EC2 instances in cloud with session manager (needs instance profiles - roles)
    - role needs `AmazonSSMManagedInstanceCore` policy
    - prerequisites: 
        - https outbound to ssm, ec2
    - add security group to ENI's
    - add [VPC endpoint to SSM](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-systems-manager-vpc-endpoints/)
- connect to onprem VM's using `hybrid activation`
    - IAM service role associated with the hybrid activation used to register your on-permises servers
    > ❗You can't change the IAM service role associated with a hybrid activation. If you find that the service role does not contain the required permissions, you must deregister the managed instance and register it with a new hybrid activation that uses a service role with the required permissions
- Get security credentials (`access key`, `secret access key`, `sessionKey`) from instance `meta-data` using the CLI command: 
```sh
# get from instance profile
TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` \
&& curl -H "X-aws-ec2-metadata-token: $TOKEN" -v http://169.254.169.254/latest/meta-data/iam/security-credentials/

# get from instance role name
TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` \
&& curl -H "X-aws-ec2-metadata-token: $TOKEN" -v http://169.254.169.254/latest/meta-data/iam/security-credentials/<instance-role-name>
```


## AWS Config
- Set rules to monitor. Config will alert w option to auto-remediate with systems manager documents integration. 
- Use [AWS Managed rules](https://docs.aws.amazon.com/config/latest/developerguide/managed-rules-by-aws-config.html), or [custom rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules.html) (requires lambda function)
- monitor and record state (previous versions) in your environment
- supports Multi-account, **multi-region** (global) data aggregation


## Event Bridge
- serverless event bus
- make rules, define source, handler and targets (functions, sns topics)

## Elastic Beanstalk
- simple application deployment service
- create environments
- deployment models:

|Model | Approach | Speed | Impact
|---|---|---|---|
All at once | Overwrite each instance w new version | ⚡ | small downtime
Rolling | deployed one batch of instances at a time | 🐢 | no downtime
Rolling with additional batch | maintain the same bandwidth throughout the deployment. With this method, Elastic Beanstalk launches an extra batch of instances, then performs a rolling deployment. | 🐢🐢 | no downtime
Immutable | blue/green. quick and safe rollback for failures | ⚡| no downtime
Traffic splitting| canary. test portion of incoming traffic while keeping the rest of the traffic served by the old application version. | ⚡| possible small impact if new version is bad