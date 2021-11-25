# Description
Repository for CloudFormation template deploying EC2 and s3 bucket. The s3 bucket stores EC2 syslog logs in `/logs` directory. After successful upload, SNS sends an email to an administrator. 

### Connection
You can connect to the EC2 instance using SSM (Session Manager). I have decided to use it instead of SSH keys since it requires less setup. Thanks to it, the user can log in to the instance right after the stack creation.  

### Logs rotating 
Logrotate postrotate script uploads log files to s3 bucket every hour. The following action triggers SNS Topic which sends an email notification to the administrator. Only one new message should appear in a mailbox because all logs are uploaded in a single archive.

# Future improvements
- SNS is sending a raw email message. Instead of sending direct mail, SNS could trigger a Lambda function that would send a better-formatted message. 
- The communication between EC2 and s3 buckets goes thru the public internet. Adding VPC Endpoint with Routing tables should improve connection privacy. 

