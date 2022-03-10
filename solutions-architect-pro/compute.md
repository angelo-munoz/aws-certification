# Compute

## Load Balancers

| Feature | Network LB | Application LB | Gateway LB | Classic LB|
| --- | --- | --- | --- | ---
OSI layer | 4 | 7 | | |
Routing | Basic (IP/port). Layer 4 | Advanced (Http headers, path, body, etc) - layer 7 | | |
Speed | millions request/sec | | | |
Use cases | High performance | Intelligent routing | | |

## Network Load balancer
- used for high perfomance (supports millions of requests/second)
- works at layer 4
- minimal routing capabilities (port number)
- improves security by improving availability (removes single point of failure)
- supports authentication with mutual TLS (2-way SSL).   See [Configuring Mutual TLS authentication for applications running on Amazon EKS](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/configure-mutual-tls-authentication-for-applications-running-on-amazon-eks.html). Example use cases: [Open Banking](https://docs.aws.amazon.com/wellarchitected/latest/financial-services-industry-lens/open-banking.html) ![](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/images/pattern-img/ae2761e3-7ed2-4c2a-ba54-a4ddce8a1e7e/images/cefc60f9-2f29-4052-b7ae-df4eb6395e1c.png)



## Kinesis
- 3 options: Kinesis Data Streams, Kinesis Firehose, Kinesis Analytics
    - Data streams: raw input, 10GB shard size
    - Firehose: easy ETL destined for S3
    - Analytics: view trends in near real-time

Quotas: 
- 10GB shard size
- 1 MB/s data processing limit. Ex: 450k data per second can scale to 2x that amount before exception thrown. 
> A single shard can ingest up to 1 MB of data per second (including partition keys) or 1,000 records per second for writes. Similarly, if you scale your stream to 5,000 shards, the stream can ingest up to 5 GB per second or 5 million records per second. If you need more ingest capacity, you can easily scale up the number of shards in the stream using the AWS Management Console or the UpdateShardCount API.
- 50 streams per account
- 500 shards per account in US-east-1 (Virginia), us-west-2 (Oregon), eu-west-1 (Ireland), 200 in other regions
- Can batch/group items for downstream lambda processing (good for release valve against high lambda throughput leading to downstream throttling)

## Kinesis Data Firehose
- ITL (ingest, transform, load) service for streaming data
- Can receive streaming traffic from Kinesis Data stream, Kinesis Agenda, AWS services, other AWS SDK/open source agents directly
- optional lambda transform before passing to downstream services (S3, Redshift, API Gateway, Splunk, other partners)
![](https://d1.awsstatic.com/pdp-how-it-works-assets/product-page-diagram_Amazon-KDF_HIW-V2-Updated-Diagram@2x.6e531854393eabf782f5a6d6d3b63f2e74de0db4.png)

## Compute Optimizer
- Analyzes current workload and makes recommendations to improve performance, lower cost, and for better resource fit
- free to use
- supports organizations

## Autoscaling
- Cannot span AZs across regions

## IoT Core
- [MQTT](https://mqtt.org/): pub/sub messaging protocol for IoT. Use MQTT clients on IoT devices with AWS IoT Core. 
- IoT core supports LoRaWan, MQTT, HTTPS transfer
- [Rules Engine](https://docs.aws.amazon.com/iot/latest/developerguide/iot-rules.html), sql-based language to filter messages to send to downstream services like S3, Lambda. 
- [send to Lambda](https://docs.aws.amazon.com/lambda/latest/dg/services-iot.html) (asynchronously) when need to forward to other AWS services

## IoT Analytics
- good but slow, seconds to minutes. If need near-real-time, use Kinesis Data Analytics (milliseconds processing time)

## Amazon Managed Blockchain
- Provisions, scales, and manages the complex blockchain network implementations
- auto-renew certs
- provisions new nodes
- Supports Hyperledger Fabric (private blockchain) and Ethereum blockchains (public blockchain)
- [Hyperledger Fabric](https://aws.amazon.com/blockchain/what-is-hyperledger-fabric/): use for access control and permissioned blockchain networks. Very useful! 
- [Ethereum](https://aws.amazon.com/blockchain/what-is-ethereum/): public blockchain network. Can join another ethereum network
- Many use-cases. Food, goods, jewelry supply chain management, insurance contracts, etc.

## AWS Outposts
- AWS Compute servers running on-prem
- Outposts Servers (1U/2U servers) and Outposts Racks (4U servers and racks)

## Amazon Lightsail
- quickly launch small web-apps, websites preconfigured w network, storage, etc
- concept:  `Virtual Private Server`
- use cases: test web apps, poc's, small business apps, etc.
- low cost

References: 
- https://aws.amazon.com/lightsail/