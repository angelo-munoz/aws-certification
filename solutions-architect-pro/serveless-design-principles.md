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

  
