# AWS SysOps Administrator Associate Certification
My practice scripts/study for the [sysops admin associate](https://aws.amazon.com/certification/certified-sysops-admin-associate/) exam. 


## VPC
**VPC S3 endpoints**

Endpoints. CLI Command: 
```sh
# gateway endpoints
aws s3 ls
# interface endpoints
# use the `--region` and `--endpoint-url` params
# todo: this command didn't work for me. troubleshoot 
aws s3 --region us-east-1 --endpoint-url vpce-1234.s3.us-east-1.vpce.amazonaws.com ls
```