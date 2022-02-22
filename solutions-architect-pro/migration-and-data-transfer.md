# Migrations

## Server Migration Service
- ** Deprecated and will sunset 3/22/22**. Replaced by [Application Migration Service](#application-migration-service)
- Migrate VM's from on-prem to cloud
- Supports up to 16TB drives
- Supports incremental sync
- Minimize downtime

References: 
- [Free AWS Cloud Migration Services](https://aws.amazon.com/free/migration/)
- https://aws.amazon.com/server-migration-service/?p=ft&c=mg&z=3

## Application Migration Service (MGN)
- Replaces Server migration service (SMS)

References: 
- https://aws.amazon.com/server-migration-service/

## Ops works
-  configuration management, compliance and security, and continuous deployment
- Chef and Puppet options
- Works in stacks and layers
- Layers have EC2 instances, load balancers, DB's, and other resources types
- Configuration as Code
- Autoscaling capability
- Dashboard shows the status of your stacks across all AWS regions
- Groups for cost allocation, and permissions
- Supports linux, Windows in cloud
- Supports cloud AND on-prem servers (hybrid architecture)
- Codepipeline more modern? Opsworks legacy? 

Billing:
- based on number of nodes connected to puppet master (or chef server), running time, and EC2 puppet master (or chef server) run time

References:
- https://aws.amazon.com/opsworks/stacks/faqs/?nc=sn&loc=5
- https://docs.aws.amazon.com/opsworks/latest/userguide/other-services-cp.html