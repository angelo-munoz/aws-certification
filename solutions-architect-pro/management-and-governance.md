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
- Supports logging on multiple regions with the `multi-region trail` option. 
- Need to enable global for global services like `IAM`, `Cloudfront`, etc with `include-global-service-events` option