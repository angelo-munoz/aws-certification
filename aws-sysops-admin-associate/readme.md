# AWS SysOps Administrator Associate Certification
My practice scripts/study for the [sysops admin associate](https://aws.amazon.com/certification/certified-sysops-admin-associate/) exam. 


## Exercise 1.

Create a solution with EC2 and Aurora RDS. RDS and EC2 should be in a private subnet, as well as EC2. Use a bastion to SSH into the EC2 instance. Bastion is restricted to your own IP address. RDS accessed from app security group only, app security group accessed from bastion security group only.  

**EC2 commands**
```sh
# ssh to bastion: public IP. This IP has been dead for a while.. don't even try it 😂
ssh ec2-user@52.87.228.85 -i <path_to_key_pair_file>

# ssh to app: private IP. Testing w a small network. 
ssh ec2-user@192.168.5.253 -i <path_to_key_pair_file>

# connect to aurora instance: get DNS name from RDS console
mysql -u admin -h <path_to_aurora_instance> -p <database_name>
# enter mysql password: ___ 
# connection successful.. run mysql commands against aurora instance

#create sample db table
MySQL> create table Sample ( sample_id INT NOT NULL AUTO_INCREMENT, sample_title varchar(128) not null, sample_date date, primary key (sample_id) );
# >: Query OK, 0 rows affected (0.02 sec)

# insert sample records and retrieve
MySQL> insert Sample (sample_title) values('test title');
# >: Query OK, 1 row affected (0.00 sec)

# see my values
MySQL> select * from Sample;
# +-----------+--------------+-------------+
# | sample_id | sample_title | sample_date |
# +-----------+--------------+-------------+
# |         1 | test title   | NULL        |
# +-----------+--------------+-------------+
# 1 row in set (0.01 sec)
```

References: 
- https://www.tutorialspoint.com/mysql/mysql-insert-query.htm

Notes: 
- An Aurora MySQL replica runs in MySQL read-only mode so no changes to data or schema allowed: `ERROR 1290 (HY000): The MySQL server is running with the --read-only option so it cannot execute this statement`

## VPC
**VPC S3 endpoints**

Endpoints. CLI Command. 
```sh
# gateway endpoints
aws s3 ls
# interface endpoints
# use the `--region` and `--endpoint-url` params
# todo: this command didn't work for me. troubleshoot 
# ref: https://docs.aws.amazon.com/AmazonS3/latest/userguide/privatelink-interface-endpoints.html
aws s3 --region us-east-1 --endpoint-url vpce-1234.s3.us-east-1.vpce.amazonaws.com ls
```

## Budgets

Notes: 
- Budgets can send notifications, send SNS message, trigger EC2/RDS stop action. 

## Cloudwatch insights
Log aggregation and analytics. My Examples below. Also see [Sample Queries](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_QuerySyntax-examples.html) in the AWS docs.  
```sh
#show last 20 error entries: with text 'Access denied'. 
# filter is CASE SENSITIVE!
fields @timestamp, @message
| filter @message like /Access denied/
| sort @timestamp desc
| limit 20

#error rate per hour
# filter is CASE SENSITIVE!
# bin function slices timestamp data - use with aggregate functions
 filter @message like /Access denied/
| stats count(*) as error_count by bin(1h)
| sort error_count desc

# message rate per hour
| stats count(*) as rate by bin(1h)
| sort rate desc
```