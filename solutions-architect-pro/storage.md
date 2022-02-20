# Storage

## Block storage vs Object Storage vs File Storage

| Criteria | Block | Object | File 
|:---|:---:|:---:|:---:
Description| files split into blocks, stored across diff disks for efficiency |discrete objects, flexible and customizable |hierarchical, accessed via SMB/NFS. Users define the location
Includes Metadata | ❌| ✅ | ✅
Speed | ⚡|🐢| ?
Scalability | ❌| ✅ | ?
Use-cases | Databases, mission-critical application storage, virtualized systems. Speed, storage of transactional data, and data that doesn’t require metadata analysis. | Storing unstructured data, storing large data sets, and storing data with custom data preservation, deletion, and retention policies. | Office Content repository 


**References** 
- https://www.networkcomputing.com/data-centers/storage-comparison-object-vs-file-vs-block-storage


## Elastic File System (EFS)
- Network File System (NFS)-based block storage in the cloud
- More expensive💲than EBS ($0.30/GB EFS vs $0.10/GB for EBS) BUT cheaper for multiple volumes since only pay once w EFS regardless of connected volumes, but pay for each volume w EBS



