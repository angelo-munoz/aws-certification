# Cost Management

## Compute Optimizer
- See [Compute Optimizer](./compute.md#compute-optimizer) in Compute

## Reducing cost
- purchase RI's. up to 72% over ondemand instances
- use spot instances. up to 90% over ondemand instances
- use savings plans

References:
- [AWS Cost Optimization Best Practices](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-rightsizing.html)
- [Optimizing your cost with Rightsizing Recommendations](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-rightsizing.html)

## AWS Budgets
- set budgets based on cost, savings, 
- set alerts with triggers to Cloudwatch Events, or automated event hooks to apply SCP, IAM policy

## Savings Plans
- 3 types: Compute, EC2, Sagemaker

Compute:
- Applies across regions
- Applies across instance family, size, OS, tenancy
- includes EC2, lamdba, fargate

EC2:
- region-specific
- up to 64%
- applies across types, size
- only covers EC2

Sagemaker:
- ? 