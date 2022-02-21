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

## Elastic Block Storage (EBS)
- Specific to single AZ only. single AZ failure will take down EBS, even though EBS has 4 9's availability (99.99%)
- IOPS calculated at 3 iops/GB. ex: 100GB drive = 100 x 3 = 300 iops. Use `io1` or `io2` drives for performance intensive use-cases like databases. 
- max IOPS = 16,000 iops
- Multi-attach volumes. Can EBS be attached to multiple EC2 instances? Yes, with [multi-attach](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes-multi.html) with provisioned IOPS volumes: `io1` or `io2`. Block storage only, not [file system](https://aws.amazon.com/premiumsupport/knowledge-center/ebs-access-volumes-using-multi-attach/).

## EBS vs EFS vs S3
- See the excellent article: [EBS Pricing and Performance: A Comparison with Amazon EFS and Amazon S3](https://cloud.netapp.com/blog/ebs-efs-amazons3-best-cloud-storage-system)

## ext3, ext4 File System
- default file system used by linux 


