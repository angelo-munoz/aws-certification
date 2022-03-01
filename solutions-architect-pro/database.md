# Database

## Aurora
- Supports cross-region read-replica *
**Aurora Global Database**

- Built-in cross-region replication

## Database Migration Service


## Data Warehouse Solutions
### Redshift Spectrum
- Service to query analytics data directly from S3

## Elastic Map Reduce (EMR)
> Amazon EMR provides a managed Hadoop framework that makes it easy, fast, and cost-effective to process vast amounts of data using EC2 instances. When using Amazon EMR, you don’t need to worry about installing, upgrading, and maintaining Spark software (or any other tool from the Hadoop framework). You also don’t need to worry about installing and maintaining underlying hardware or operating systems. Instead, you can focus on your business applications and use Amazon EMR to remove the undifferentiated heavy lifting. - AWS Docs

- Cluster. central component. Collection of EC2  instances. 
- Node. instance in a cluster. Each node has a role within the cluster, referred to as the node type. 
The node types in Amazon EMR are as follows:
  - *Master node*: A node that manages the cluster by running software components to coordinate the distribution of data and tasks among other nodes for processing. The master node tracks the status of tasks and monitors the health of the cluster. Every cluster has a master node, and it's possible to create a single-node cluster with only the master node.
  - *Core node*: A node with software components that run tasks and store data in the Hadoop Distributed File System (HDFS) on your cluster. Multi-node clusters have at least one core node.
  - *Task node*: A node with software components that only runs tasks and does not store data in HDFS. Task nodes are optional.