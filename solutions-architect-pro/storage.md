# Storage

## Block storage vs Object Storage vs File Storage

| Criteria | Block | Object | File 
|:---|:---:|:---:|:---:
Description| files split into blocks, stored across diff disks for efficiency |discrete objects, flexible and customizable |hierarchical, accessed via SMB/NFS. Users define the location
Includes Metadata | ❌| ✅ | ✅
Speed | ⚡|🐢| ?
Scalability | ❌| ✅ | ?
Use-cases | Databases, mission-critical application storage, virtualized systems. Speed, storage of transactional data, and data that doesn’t require metadata analysis. | Storing unstructured data, storing large data sets, and storing data with custom data preservation, deletion, and retention policies. | Office Content repository 

References:
- https://www.networkcomputing.com/data-centers/storage-comparison-object-vs-file-vs-block-storage


## Elastic File System (EFS)
- Network File System (NFS)-based block storage in the cloud
- More expensive💲than EBS ($0.30/GB EFS vs $0.10/GB for EBS) BUT cheaper for multiple volumes since only pay once w EFS regardless of connected volumes, but pay for each volume w EBS
- Highly available (survives single AZ failure)
- Does not audit access

## Elastic Block Storage (EBS)
- Specific to single AZ only. single AZ failure will take down EBS, even though EBS has 4 9's availability (99.99%)
- IOPS calculated at 3 iops/GB. ex: 100GB drive = 100 x 3 = 300 iops. Use `io1` or `io2` drives for performance intensive use-cases like databases. 
- max IOPS = 16,000 iops (or 5.34 TiB), meaning volumes larger than 5TB will not give more iops since it's already at 16000 iops.
- Multi-attach volumes. Can EBS be attached to multiple EC2 instances? Yes, with [multi-attach](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes-multi.html) with provisioned IOPS volumes: `io1` or `io2`. Block storage only, not [file system](https://aws.amazon.com/premiumsupport/knowledge-center/ebs-access-volumes-using-multi-attach/).


## EBS vs EFS vs S3
- See the excellent article: [EBS Pricing and Performance: A Comparison with Amazon EFS and Amazon S3](https://cloud.netapp.com/blog/ebs-efs-amazons3-best-cloud-storage-system)

## ext3, ext4 File System
- default file system used by linux 

## Simple Storage Service (S3)

Presigned Urls: 
|Session Type|Signed Url Valid for 
|---|---
IAM instance profile|Up to 6 hours.
AWS STS|Up to 36 hours when signed with permanent credentials, such as the credentials of the AWS account root user or an IAM user.
IAM user|Up to 7 days when using AWS Signature Version 4.

- get presigned urls from CLI using the `presign` command: 
```
aws s3 presign s3://am-2022-02-26/test.txt --expires-in 30
```
- can [upload to folders](https://docs.aws.amazon.com/AmazonS3/latest/userguide/PresignedUrlUploadObject.html) using presigned urls. Very interesting! 
- Intelligent tiering only applies to objects > 128K
- Storage tiers:

|Tier|Cost|Speed|Use cases
|---|---|---|---|
S3 Standard|💲💲|millisecond access|Most. default if not specified
S3 Intelligent Tiering|💲💲💲|millisecond access|auto-change classes based on access frequency. After 30 days transfer to diff tiers
S3 Infrequent Access|charged for minimum 30 days, and has access fee ❗|millisecond access|
S3 One-Zone IA|charged for minimum 30 days, and has access fee ❗|millisecond access|Use if you can re-create the data if the Availability Zone fails, and for object replicas when setting S3 Cross-Region Replication (CRR)
Glacier|💲|up to 6 hrs. instant retrieval available since 2021 reInvent|
Glacier Deep Archive|💲|up to 12 hrs|


## Amazon FSx for Lustre
- fast OS for HPC, machine learning, etc. 
- POSIX compliant so works OOTB w linux
- integrates w S3 to pull data on demand

## Storage Gateway
- 3 flavors: Volume Gateway, File Gateway, Tape Gateway
- Stored Volumes: 1 GiB to 16 TB

Volume Gateway:
- for disks
- 2 types: Volume Storage Gateway and Volume Cached Gateway
- Volume Storage
    - Full volume
    - Need local storage same size
- Cached Volume Mode
    - cache only frequently accessed
- How it works: 
    - VM in data center connects to iSCSI
    - provision disks
    - async data backup to S3 as block storage that can be restored for DR.
- DR: 
    - ❗take EBS snapshot then restore to EBS volume.

![](https://docs.aws.amazon.com/storagegateway/latest/userguide/images/aws-storage-gateway-stored-diagram.png) 

## Data Lifecyle Manager
- Amazon Data Lifecycle Manager (DLM) for EBS Snapshots provides a simple, automated way to back up data stored on Amazon EBS volumes. 
- define backup and retention schedules for EBS snapshots by creating lifecycle policies based on tags. 

## Transfer acceleration
- uses the `s3-accelerate.amazonaws.com` endpoints to transfer files to S3 via Amazon's backbone network
