## AWS SNS Mobile Push
- send push notifications to mobile devices

## AWS Lambda
- max concurrency: 1000 per region, per account
- [Provisioned Concurrency](https://docs.aws.amazon.com/lambda/latest/dg/provisioned-concurrency.html): 
  - lambdas stay hot (warmed) to meet traffic demand. remove cold starts
  - incurs cost since the compute stays on 
  - does not turn on immediately. 1-2 min delay. 
  - counts toward reserved concurrency?
  - applies to `alias` or `version`
- [Reserved concurrency](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html): 
  - per lambda function
  - reserve capacity for individual lambdas but provision capacity
  - Scaling upper limit. `Can scale up to that amount` 
  - throttle lambdas by setting reserved concurrency to `0`
- Unreserved concurrency: 
  - remaining after reserved and provisioned


References: 
  - https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html

  ## AWS AppSync
  - GraphQL api managed service
  - pulls from multiple data sources in single api call
  - real-time option via `subscriptions`
  ![](https://d1.awsstatic.com/AppSync/How-It-Works-product-page-diagram_AppSync%402x.c39ecb89b7b40ba682cf0f875ae13b6bdd8dca5b.png)

  
## SQS

Limits:
Item|min|max|Comment
---|---|---|---|
Message Size|0|256 KB|Use java client SDK lib to leverage storage in S3
Visibility Timeout|0 seconds|12 hours|default 30s 
Throughput (FIFO)||300 msgs/sec|High FIFO
Throughput (Standard)||3000 msgs/sec|Std
Message Content|||can include only `XML`, `JSON`, and `unformatted text`. The following Unicode characters are allowed: `#x9`, `#xA`, `#xD`, `#x20` to `#xD7FF`, `#xE000` to `#xFFFD`, `#x10000` to `#x10FFFF`
Retention|60s|14 days|default 4 days
Delay queue|0 secs|15 mins|
Long polling wait time|0|20 secs|
Message groups|0|none|for FIFO queues
Messages per queue (backlog)|0|none|The number of messages that an Amazon SQS queue can store is unlimited.
Messages per queue (in flight)|0|120,000|For most standard queues (depending on queue traffic and message backlog), there can be a maximum of approximately 120,000 inflight messages (received from a queue by a consumer, but not yet deleted from the queue). If you reach this quota while using short polling, Amazon SQS returns the `OverLimit` error message. If you use long polling, Amazon SQS returns no error messages. To avoid reaching the quota, you should **delete messages from the queue after they're processed.** You can also increase the number of queues you use to process your messages. To request a quota increase, submit a support request. For FIFO queues, there can be a maximum of 20,000 inflight messages (received from a queue by a consumer, but not yet deleted from the queue). If you reach this quota, Amazon SQS returns no error messages.
