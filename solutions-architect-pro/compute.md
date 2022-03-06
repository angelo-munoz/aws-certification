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

## Compute Optimizer
- Analyzes current workload and makes recommendations to improve performance, lower cost, and for better resource fit
- free to use
- supports organizations