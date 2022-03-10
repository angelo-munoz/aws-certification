# Database

## RDS
- supported RDBMS: 
- not supported: Oracle RAC, SAP Hana
- `Available` updates can be deferred indefinitely. `Required` updates are deferred until an AWS-defined max date. 

EBS Volume:
- General purpose SSD (gp2) may decrease in performance after: `read replica creation, Multi-AZ conversion, and DB snapshot restoration`
- Scaling storage: 
  - possible with `modify-instance`. Does not cause service degradation but can take up to few hours to complete. 
  - Can't request another storage change for 6 hrs
  - See [Working with Storage for RDS Instances](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.StorageTypes.html)
    - can't **reduce** the storage size, only increase
    - size increase required by at least 10%
    - During failover, the DNS CNAME is updated from primary to secondary, not the IP address. ❗ 
    - to force a failover, do a `reboot instance`


## Aurora
- Supports cross-region read-replica

**Aurora Global Database**
- Built-in cross-region replication

## Database Migration Service
- Migrate on-prem to cloud, cloud to cloud, cloud to onprem. But Not onprem to onprem
- Supports one-time and continuous replication
- Use in conjunction with the Schema Conversion Tool (SCT). Convert schema first w SCT, then DMS to fill data


## Data Warehouse Solutions
## Redshift Spectrum
- Service to query analytics data directly from S3

## Elastic Map Reduce (EMR)
> Amazon EMR provides a managed Hadoop framework that makes it easy, fast, and cost-effective to process vast amounts of data using EC2 instances. When using Amazon EMR, you don’t need to worry about installing, upgrading, and maintaining Spark software (or any other tool from the Hadoop framework). You also don’t need to worry about installing and maintaining underlying hardware or operating systems. Instead, you can focus on your business applications and use Amazon EMR to remove the undifferentiated heavy lifting. - AWS Docs

- Cluster. central component. Collection of EC2  instances. 
- Node. instance in a cluster. Each node has a role within the cluster, referred to as the node type. 
The node types in Amazon EMR are as follows:
  - *Master node*: A node that manages the cluster by running software components to coordinate the distribution of data and tasks among other nodes for processing. The master node tracks the status of tasks and monitors the health of the cluster. Every cluster has a master node, and it's possible to create a single-node cluster with only the master node.
  - *Core node*: A node with software components that run tasks and store data in the Hadoop Distributed File System (HDFS) on your cluster. Multi-node clusters have at least one core node.
  - *Task node*: A node with software components that only runs tasks and does not store data in HDFS. Task nodes are optional.

![](https://media.tutorialsdojo.com/sap_emr_node_types.png)

## Redshift
- cross-region backup. Use `snapshot copy grant` feature that allows the destination region to decrypt using that key. 

## DynamoDB
- primary key = partition key alone OR partition key + sort key
- global secondary index doesn't support strongly consistent reads. See [Read Consistency](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadConsistency.html)
- Use [Conditional Writes](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithItems.html#WorkingWithItems.ConditionalUpdate) to prevent race conditions or catch-22's where multiple writers need to both write to the table. Ex: only update `price` to 8 if `price` is currently 10. That way, before you update, you get the current item, and add it to the conditional statement. 