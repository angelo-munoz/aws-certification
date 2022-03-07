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

## Snow family
|Type|Max Size|Use case
|---|---|---|
Snowball|80TB|Order several as needed. Up to 10 PB. Over that, use snowmobile
Snowmobile|100 PB|Large transfers


**Snowball Edge:**
- replaces Snowball
- 3 types - Storage-optimized, Compute-optimized, Compute-optimized w GPU
    - Storage-optimized: 
    - Compute-optimized:
    - Compute-optimized w GPU:
- can transfer using 3 methods: 
    - File interface: 
        - encrypts objects
    - S3 transfer tool
        - encrypts objects
    - AWS IoT Greengrass 
- Max storage: 60-80 TB
- File interface (NFS share) built-in
- Encrypts data by default (supports SSE-S3, SSE-KMS server side encryption). SSE-C (client owned encryption **not** supported)
- Transfer speeds: up to 100 Gbit/second
- Increase performance 🚀 by adding multiple transfers to the same Snowball

Snowball hardware:
- RJ45 (Cat6), SFP+ Copper (10Gb/s), SFP+ Optical

**Required ports for Snowball**: [Reference](https://docs.aws.amazon.com/snowball/latest/developer-guide/port-requirements.html)
|Port|Protocol|Comment|
|---|---|---|
22 (HTTP)|TCP|Device health check and for EC2 SSH
2049 (HTTP)|TCP|NFS endpoint
6078 (HTTP)|TCP|IAM HTTP endpoint
6089 (HTTPS)|TCP|IAM HTTPS endpoint
7078 (HTTP)|TCP|STS HTTP endpoint
7089 (HTTPS)|TCP|STS HTTPS endpoint
8080 (HTTP)|TCP|S3 HTTP endpoint
8443 (HTTPS)|TCP|S3 HTTPS endpoint
8008 (HTTP)|TCP|EC2 HTTP endpoint
8243 (HTTPS)|TCP|EC2 HTTPS endpoint
9091 (HTTP)|TCP|Endpoint for device management

## The 5 R's of Migration
![](https://media.tutorialsdojo.com/sap_migration_paths.png)
1. **Rehost** ("lift and shift") – Migrate as is. Most popular

2. **Replatform** ("lift, tinker and shift") – few small cloud optimizations toward tangible benefit without changing the core architecture of the application

3. **Repurchase** ("drop and shop") – upgrade or buy different product

4. **Refactor / Re-architect** – strong business need to add features, scale, or performance that can't be done in the app's current state/environment

5. **Retire** – Sunset/turn off application

6. **Retain** – stay the same. Maybe just upgraded, or too risky, or not cost/technically feasible to migrate. 

