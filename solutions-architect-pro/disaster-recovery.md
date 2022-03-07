# Disaster Recovery

## Models
|Active/Passive|Models|RTO/RPO|Cost|Desciption
|---|---|---|---|---|
Active/Passive|Backup and restore|hours|$|slow but cheap
Active/Passive|Pilot light|10s of mins|$$|data live, skeleton infra up, can scale up. 
Active/Passive|Warm standby|mins|$$$|full app running but smaller instance, ability to scale up
Active/Active|Multi-site, active/active|real-time|$$$$|both active simultaneously

See [Disaster Recovery Options in the Cloud](https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/disaster-recovery-options-in-the-cloud.html)