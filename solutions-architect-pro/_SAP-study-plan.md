# Study Plan

<style>
  sup { vertical-align:super; 
    display: inline;
    font-size: 80%;
    color:#f55;
    font-weight:normal;    
  }
  time {
    color:#6bf;
    margin-left: 0.5em;
  }
  done {
    initial: "&#x2713;";
    color: green;
  }
</style>

# Breakdown

Domain | % of Exam
--- | ---
Domain 1: Design for Organizational Complexity | 12.5%
Domain 2: Design for New Solutions | 31%
Domain 3: Migration Planning | 15%
Domain 4: Cost Control | 12.5%
Domain 5: Continuous Improvement | 29%
TOTAL | 100

# Domains

## Domain 1: Design for Organizational Complexity <time>6 weeks</time>
1.1 Determine _cross-account authentication_ and _access strategy_ for complex organizations. - <time>1 week<time>

   - Analyze the organizational structure <sup>cross-account auth</sup>
   - Evaluate the current authentication infrastructure <sup>AD connector, AWS SSO</sup>
   - Analyze the AWS resources at an account level <sup>?</sup>
   - Determine an auditing strategy for authentication and access <sup>cloud trail</sup>

1.2 Determine how to design networks for complex organizations. <time>3 weeks</time>
  - Outline an IP addressing strategy for VPCs <sup>subnetting, overlapping IP's, VPC peering</sup> <time>1 week</time>
  - Determine DNS strategy <sup>Route53</sup><time>3 days</time>
  - Classify network traffic and security <sup>port numbers?, VPC, securing a network - NACL, security groups, WAF, Shield</sup><time>2 days</time>
  - Determine connectivity needs for hybrid environments <sup>Direct Connect, VPN</sup> <time>1 week</time>
  - Determine a way to audit network traffic <sup>VPC flow logs</sup> <time>2 days</time>

1.3 Determine how to design a multi-account AWS environment for complex organizations. - <time>2 weeks</time>
  - Determine how to use AWS Organizations <time>1 day</time>
  - Implement the most appropriate account structure for proper cost allocation, agility, and security <sup>Organizations, cost explorer, SCP, stack sets</sup> <time>3 days</time>
  - Recommend a central audit and event notification strategy <sup>cloud trail, event bridge</sup><time>3 days</time>
  - Decide on an access strategy <sup>AD connector, SimpleAD, AWS Directory service for AD</sup><time>4 days</time>
 
## Domain 2: Design for New Solutions
2.1 Determine security requirements and controls when designing and implementing a solution.
  - Implement infrastructure as code <sup>cloudformation advanced - retain/instance/etc</sup><time>3 days</time>
  - Determine prevention controls for large-scale web applications<sup>cloudformation
  - Determine roles and responsibilities of applications <sup>IAM roles</sup>
  - Determine a secure method to manage credentials for the solutions/applications <sup>Systems Manager Parameter Store, Secrets Manager</sup>
  - Enable detection controls and security services for large-scale applications <sup>WAF, Inspector, Macie</sup>
  - Enforce host and network security boundaries <sup>Security groups, NACLs</sup>
  - Enable encryption in transit and at rest<sup>ACM - TLS cert in transit, KMS - CMK at rest</sup>

2.2 Determine a solution design and implementation strategy to meet reliability requirements.
  - Design a highly available application environment <sup>multiple AZ's</sup>
  - Determine advanced techniques to detect for failure and service recoverability <sup>lambda hooks?</sup>
  - Determine processes and components to monitor and recover from regional service disruptions with regional failover <sup>multi-region architecture - Transit Gateway, Direct Connect Gateway, Route53 failover routing policy</sup>

2.3 Determine a solution design to ensure business continuity.
  - Architect an automated, cost-effective back-up solution that supports business continuity across multiple AWS Regions <sup>S3 cross-region replication, DMS</sup>
  - Determine an architecture that provides application and infrastructure availability in the event of a service disruption <sup>EC2 autoscaling across multiple AZ's, Route53 failover policy, Aurora multi-master, Aurora global tables</sup>

2.4 Determine a solution design to meet performance objectives.
  - Design internet-scale application architectures <sup>Kinesis</sup>❗
  - Design an architecture for performance according to business objectives <sup>RDS read-replica</sup>
  - Apply design patterns to meet business objectives with caches, buffering, and replicas <sup>Elasticache (Redis, Memcached), SQS, Aurora read-replicas</sup>❗

2.5 Determine a deployment strategy to meet business requirements when designing and implementing a solution.
  - Determine resource provisioning strategy to meet business objectives <sup>Cloudformation, SAM</sup>
  - Determine a migration process to change the version of a service <sup>blue/green deployment</sup>❗
  - Determine services to meet deployment strategy <sup>CodeDeploy, CodePipeline, SAM, Cloudformation, Elastic Beanstalk❗</sup>❗
  - Determine patch management strategy <sup>Systems Manager</sup>❗
 
## Domain 3: Migration Planning
3.1 Select existing workloads and processes for potential migration to the cloud.
  - Complete an application migration assessment <sup>Application discovery service</sup>❗
  - Classify applications according to the six Rs (re-host, re-platform, re-purchase, refactor, retire, and retain) <sup>Migration types - 6R's❗❗</sup>

3.2 Select migration tools and/or services for new and migrated solutions based on detailed AWS knowledge.
  - Select an appropriate database transfer mechanism <sup>DMS, native import/export, backup</sup>
  - Select an appropriate data transfer service <sup>Storage Gateway, S3 sync, calculate transfer time based on bandwidth</sup>❗
  - Select an appropriate data transfer target
  - Select an appropriate server migration mechanism <sup>Application migration service, VM Import</sup>❗
  - Apply the appropriate security methods to the migration tools <sup>IAM?</sup>❗

3.3 Determine a new cloud architecture for an existing solution.
  - Evaluate business applications and determine the target cloud architecture <sup>design</sup>
  - Break down the functionality of applications into services <sup>design</sup>
  - Determine target database platforms <sup>NoSQL, Relational - Aurora, etc</sup>

3.4 Determine a strategy for migrating existing on-premises workloads to the cloud.
  - Determine the desired prioritization strategy of the organization <sup>?</sup>❗
  - Analyze data volume and rate of change to determine a data transfer strategy <sup>calculate time to transfer based on bandwidth, snow family limits</sup>❗
  - Evaluate cutover strategies <sup>DMS continuous replication</sup>
  - Assess internal and external compliance requirements for a successful migration <sup>?</sup>❗
 
## Domain 4: Cost Control
4.1 Select a cost-effective pricing model for a solution.
  - Purchase resources based on usage requirements <sup>Reserved instances, EC2 savings plans, Compute savings plans</sup>❗
  - Identify when to use different storage tiers <sup>durability, availability, etc</sup>

4.2 Determine which controls to design and implement that will ensure cost optimization.
  - Determine an AWS-generated cost allocation tags strategy that allows mapping cost to business units <sup>cost explorer by tag - activate tag for billing first</sup>
  - Determine a mechanism to monitor when underutilized resources are present <sup>Compute Optimizer, Trusted Advisor</sup>❗❗
  - Determine a way to manage commonly deployed resources to achieve governance <sup>Config, Systems Manager documents, runbooks</sup>
  - Define a way to plan costs that do not exceed the budget amount <sup>AWS Budgets</sup>

4.3 Identify opportunities to reduce cost in an existing architecture.
  - Distinguish opportunities to use AWS Managed Services  <sup>Review requirements</sup>
  - Determine which services are most cost-effective in meeting business objectives <sup>Know service prices!</sup>❗❗

## Domain 5: Continuous Improvement for Existing Solutions
5.1 Troubleshoot solutions architectures.
  - Assess an existing application architecture for deficiencies <sup>Well architected framework</sup>
  - Analyze application and infrastructure logs <sup>Cloudwatch agent</sup>
  - Test possible solutions in non-production environment <sup>Cloudformation, SAM</sup>

5.2 Determine a strategy to improve an existing solution for operational excellence.
  - Determine the most appropriate logging and monitoring strategy <sup>Cloudwatch, xray</sup>
  - Recommend the appropriate AWS offering(s) to enable configuration management automation <sup>Chef, Puppet, Systems Manager</sup>

5.3 Determine a strategy to improve the reliability of an existing solution.
  - Evaluate existing architecture to determine areas that are not sufficiently reliable <sup>Well architected framework</sup>
  - Remediate single points of failure <sup>Well architected framework</sup>
  - Enable data replication, self-healing, and elastic features and services <sup>Well archicted framework</sup>
  - Test the reliability of the new solution <sup>lambda functions, SAM, cloudformation</sup>

5.4 Determine a strategy to improve the performance of an existing solution.
  - Reconcile current performance metrics against performance targets <sup>Trusted Advisor❗, cloudwatch</sup>
  - Identify and examine performance bottlenecks <sup>CLoudwatch logs, single-points of failure - well architected framework</sup>
  - Recommend and test potential remediation solutions <sup>cloudformation</sup>

5.5 Determine a strategy to improve the security of an existing solution.
  - Evaluate AWS Secrets Manager strategy <sup>more expensive than param store but param store lacks key auto-rotation</sup>
  - Audit the environment for security vulnerabilities <sup>AWS Inspector</sup>
  - Enable manual and/or automated responses to the detection of vulnerabilities <sup>?</sup>❗

5.6 Determine how to improve the deployment of an existing solution.
  - Evaluate appropriate tooling to enable infrastructure as code <sup>cloudwatch, SAM, Beanstalk, Code Deploy, Code Pipeline❗</sup>
  - Evaluate current deployment processes for improvement opportunities <sup>cloudwatch, SAM</sup>
  - Test automated deployment and rollback strategies <sup>lambda hooks in pipeline</sup>

## Which key tools, technologies, and concepts might be covered on the exam?

The following is a non-exhaustive list of the tools and technologies that could appear on the exam. This list is subject to change and is provided to help you understand the general scope of services, features, or technologies on the exam. The general tools and technologies in this list appear in no particular order. 
AWS services are grouped according to their primary functions. While some of these technologies will likely be covered more than others on the exam, the order and placement of them in this list is no indication of relative weight or importance:

- Compute
- Cost management
- Database
- Disaster recovery
- High availability
- Management and governance
- Microservices and component decoupling
- Migration and data transfer
- Networking, connectivity, and content delivery
- Security
- Serverless design principles
- Storage

### AWS services and features
**Analytics:**

- [Amazon Athena](https://docs.aws.amazon.com/athena/latest/ug/what-is.html). Use S3 syntax to query S3 files
- [Amazon Elasticsearch Service](https://aws.amazon.com/opensearch-service/the-elk-stack/what-is-elasticsearch/). Search
- [Amazon EMR](https://aws.amazon.com/emr/). Big data
- [AWS Glue](https://aws.amazon.com/glue/). ETL tool. 
- [Amazon Kinesis](https://aws.amazon.com/kinesis/). Data streaming service
- [Amazon QuickSight](https://aws.amazon.com/quicksight/). Analytics and Business Intelligence tool

**AWS Billing and Cost Management:**
- AWS Budgets
- Cost Explorer

**Application integration:**
- Amazon MQ
- Amazon Simple Notification Service (Amazon SNS)
- Amazon Simple Queue Service (Amazon SQS)
- AWS Step Functions

**Business applications:**
- Amazon Alexa
- Amazon Alexa for Business
- Amazon Simple Email Service (Amazon SES)

**Blockchain:**
- Amazon Managed Blockchain

**Compute:**
- AWS Batch
- Amazon EC2
- AWS Elastic Beanstalk
- Amazon Elastic Container Service (Amazon ECS)
- Amazon Elastic Kubernetes Service (Amazon EKS)
- Elastic Load Balancing
- AWS Fargate
- AWS Lambda
- Amazon Lightsail
- AWS Outposts

**Containers:**
- Amazon Elastic Container Registry (Amazon ECR)

**Database:**
- Amazon Aurora
- Amazon DynamoDB
- Amazon ElastiCache
- Amazon Neptune
- Amazon RDS
- Amazon Redshift

**Developer tools:**
- AWS Cloud9
- AWS CodeBuild
- AWS CodeCommit
- AWS CodeDeploy
- AWS CodePipeline

**End user computing:**
- Amazon AppStream 2.0
- Amazon WorkSpaces

**Front-end web and mobile:**
- AWS AppSync❗

**Machine learning:**
- Amazon Comprehend
- Amazon Forecast
- Amazon Lex
- Amazon Rekognition
- Amazon SageMaker
- Amazon Transcribe
- Amazon Translate❗

**Management and governance:**
- AWS Auto Scaling❗
- AWS Backup 
- AWS CloudFormation 
- AWS CloudTrail 
- Amazon CloudWatch 
- AWS Compute Optimizer 
- AWS Config 
- AWS Control Tower 
- Amazon EventBridge 
- AWS License Manager ❗
- AWS Organizations 
- AWS Resource Access Manager 
- AWS Service Catalog 
- AWS Systems Manager 
- AWS Trusted Advisor 
- AWS Well-Architected Tool 

**Media services:** 
- Amazon Elastic Transcoder❗

**Migration and transfer:** 
- AWS Database Migration Service (AWS DMS) 
- AWS DataSync ❗
- AWS Migration Hub 
- AWS Server Migration Service (AWS SMS) 
- AWS Snowball - AWS Transfer Family

**Networking and content delivery:**
- Amazon API Gateway 
- Amazon CloudFront 
- AWS Direct Connect 
- AWS Global Accelerator 
- Amazon Route 53 
- AWS Transit Gateway 
- Amazon VPC

**Security, identity, and compliance:**
- AWS Artifact 
- AWS Certificate Manager (ACM) 
- Amazon Cognito 
- AWS Directory Service 
- Amazon GuardDuty ❗
- AWS Identity and Access Management (IAM) 
- Amazon Inspector ❗
- AWS Key Management Service (AWS KMS)
- Amazon Macie
- AWS Resource Access Manager
- AWS Secrets Manager
- AWS Security Hub❗
- AWS Shield
- AWS Single Sign-On❗
- AWS WAF

**Storage:**
- Amazon Elastic Block Store (Amazon EBS)
- Amazon Elastic File System (Amazon EFS)
- Amazon FSx
- Amazon S3
- Amazon S3 Glacier
- AWS Storage Gateway