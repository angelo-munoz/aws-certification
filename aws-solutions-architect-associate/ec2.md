# EC2

## Simple boot strap script: bash
Use with the AWS linux AMI, in the `user data` section when launching your EC2 instance. Since this script will run as `root`, don't include the `sudo` comands. According to the AWS docs on [user data](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html): 
> Scripts entered as user data are run as the root user, so do not use the sudo command in the script. Remember that any files you create will be owned by root; if you need non-root users to have file access, you should modify the permissions accordingly in the script. Also, because the script is not run interactively, you cannot include commands that require user feedback (such as yum update without the -y flag).`

```bash
#!/bin/bash
#update OS
yum update -y

#install apache
yum install httpd -y

#start the web server
service httpd start

#set apache to start with reboot
chkconfig httpd on

#our first webpage! 
echo "<h1>hello!!</h1>" > /var/www/html/index.html

#make a backup of our webpage to s3 and remove it for demo purposes. 

#random bucket name: instanceId + datestamp
instanceId=`curl -X GET http://169.254.169.254/latest/meta-data/instance-id`
datestamp=`date '+%s'`
bucket=s3://angelo-test-$instanceId-$datestamp

#requires the ec2 instance role to have s3 perms
aws s3 mb $bucket
aws s3 cp /var/www/html/index.html $bucket/index.html

#remove item from bucket. Can't delete bucket unless it's empty
aws s3 rm $bucket/index.html
aws s3 rb $bucket
```

Your webpage will now display `hello!` 

### Troubleshooting
If you try to overwrite the file using the `echo` command like the example below and get a bash error, open the file with `nano` and manually edit and save. 
``` bash
echo "<h1>hello!!</h1>" > /var/www/html/index.html
```


## Autoscaling 
Use this bootstrap script on the EC2 instance user data to display a unique value for each instance web page. Makes it easy to see instance cycle in the load balancer as you hit refresh. 
```bash
#!/bin/bash
#update OS
yum update -y

#install apache
yum install httpd -y

#start the web server
service httpd start

#set apache to start with reboot
chkconfig httpd on

#make a backup of our webpage to s3 and remove it for demo purposes. 
#random bucket name: instanceId + datestamp
instanceId=`curl -X GET http://169.254.169.254/latest/meta-data/instance-id`
datestamp=`date '+%s'`
bucket=s3://angelo-test-$instanceId-$datestamp

#our first webpage! 
echo $instanceId > /var/www/html/index.html

```

To stress test the CPU: 
```bash
while true echo 1

#OR

sudo amazon-linux-extras install epel -y
sudo yum install stress -y
stress --cpu 4 #stress test the CPU (up to 4 cores)
```
