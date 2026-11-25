# **AWS CLI (Command Line Interface)**


# **Jira Ticket: AWS CLI Installation and Configuration**

**Problem statement**

An e-commerce company wants its DevOps team to manage AWS resources using command-line tools instead of performing every operation manually through the AWS Console.

The Junior DevOps Engineer must install AWS CLI, configure authentication and verify connectivity with AWS.

**Tasks:**

- Install AWS CLI Version 2.
- Verify installation using `aws --version`.
- Configure AWS credentials.
- Verify AWS identity using `aws sts get-caller-identity`.
- List all S3 buckets.
- List EC2 instances in the Mumbai region.
- Create an S3 bucket using AWS CLI.

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/a3fa5473-b256-4bae-a5eb-b2648febb66e" />

## **1. What is AWS CLI?**

**AWS CLI stands for Amazon Web Services Command Line Interface.**

AWS CLI is a tool that allows us to interact with and manage AWS services using commands instead of logging into the AWS Management Console (web browser).

In simple words:

AWS CLI allows a DevOps engineer to manage AWS resources directly from a terminal or command prompt.

**Example:**

Normally, if you want to create an S3 bucket, you:

1. Login to AWS Console.
2. Open S3 service.
3. Click Create Bucket.
4. Enter the bucket name.
5. Click Create.

Using AWS CLI, you can create an S3 bucket with just one command:

```
aws s3 mb s3://my-first-demo-bucket
```

## **2. Why do we need AWS CLI?**

Imagine you are working as a DevOps Engineer in an e-commerce company.

Your company has:

- 50 EC2 instances.
- 20 S3 buckets.
- 10 RDS databases.
- Multiple AWS environments (DEV, QA, UAT, PROD).

Managing all these resources manually through the AWS Console takes time.

AWS CLI helps automate these operations.

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/517b9b92-ddeb-4866-ae5f-2931a4d78608" />


### **Real-time use cases**

| Requirement           | AWS CLI command                                              |
| --------------------- | ------------------------------------------------------------ |
| List all S3 buckets   | `aws s3 ls`                                                  |
| Create an S3 bucket   | `aws s3 mb s3://bucket-name`                                 |
| Upload a file to S3   | `aws s3 cp index.html s3://bucket-name/`                     |
| List EC2 instances    | `aws ec2 describe-instances`                                 |
| Start an EC2 instance | `aws ec2 start-instances --instance-ids i-1234567890abcdef0` |
| Stop an EC2 instance  | `aws ec2 stop-instances --instance-ids i-1234567890abcdef0`  |
| List IAM users        | `aws iam list-users`                                         |

## **3. AWS CLI vs AWS Management Console**

| AWS Console                         | AWS CLI                     |
| ----------------------------------- | --------------------------- |
| GUI-based                           | Command-based               |
| Uses a web browser                  | Uses terminal               |
| Manual operations                   | Automation-friendly         |
| Suitable for beginners              | Useful for DevOps engineers |
| Time-consuming for repetitive tasks | Faster for repetitive tasks |

**Important:** AWS CLI is commonly used with Jenkins, Terraform, Shell Scripting and CI/CD pipelines to automate AWS operations.

## **4. How to install AWS CLI**

Recommended: AWS CLI Version 2

AWS provides AWS CLI Version 2 for Windows, Linux and macOS. We will use Version 2.&#x20;

https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32

AWS Command Line Interface+1



### **A. Install AWS CLI on Windows**

Since you are using Windows, follow these steps:

**Step 1: Download AWS CLI**

Open the official AWS download link:

[Download AWS CLI Version 2 for Windows (64-bit)](https://awscli.amazonaws.com/AWSCLIV2.msi?utm_source=chatgpt.com)

**Step 2: Install AWS CLI**

1. Double-click the downloaded `.msi` file.
2. Click Next.
3. Accept the license agreement.
4. Click Install.
5. Complete the installation.

**Step 3: Verify installation**

Open Command Prompt or PowerShell and execute:

```
aws --version
```

Expected output will look similar to:

```
aws-cli/2.x.x Python/3.x.x Windows/10 exe/AMD64
```

If you see the AWS CLI version, installation is successful.

### **B. Install AWS CLI on Ubuntu Linux**

Execute these commands one by one:

**Step 1: Download AWS CLI**

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

**Step 2: Install unzip**

```
sudo apt update
sudo apt install unzip -y
```

**Step 3: Extract the downloaded file**

```
unzip awscliv2.zip
```

**Step 4: Install AWS CLI**

```
sudo ./aws/install
```

**Step 5: Verify installation**

```
aws --version
```

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

## OR Install on Ubuntu

<img width="1855" height="152" alt="image" src="https://github.com/user-attachments/assets/d56aaf25-0803-4870-b302-deaa483afd81" />

```
sudo apt  install awscli -y

```


### **C. Install AWS CLI on macOS**

1. Download the installer: [AWS CLI for macOS](https://awscli.amazonaws.com/AWSCLIV2.pkg?utm_source=chatgpt.com).
2. Open the downloaded package.
3. Follow the installation instructions.
4. Open Terminal and execute:

```
aws --version
```

## **5. Configure AWS CLI**

Installing AWS CLI is not enough. We also need to configure AWS credentials so that CLI can communicate with our AWS account.

Think of it this way:

- AWS CLI = Your remote control.
- AWS credentials = Your identity.
- IAM permissions = What you are allowed to do.

### **Step 1: Create IAM credentials**

1. Login to AWS Management Console.
2. Open IAM.
3. Create an IAM user or use an approved IAM Identity Center login.
4. Set up programmatic access using the appropriate authentication method.
5. For an IAM user, obtain its Access Key ID and Secret Access Key.

**Important:** Never use root account access keys. Prefer short-lived credentials and least-privilege access.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

AWS Command Line Interface+1



### **Step 2: Execute AWS configure**

Open PowerShell or Terminal:

```
aws configure
```

It will ask four questions:

```
AWS Access Key ID: AKIAxxxxxxxxxxxx

AWS Secret Access Key: xxxxxxxxxxxxxxxx

Default region name: ap-south-1

Default output format: json
```

Explanation:

| Parameter         | Meaning                               |
| ----------------- | ------------------------------------- |
| Access Key ID     | Identifies your IAM access key        |
| Secret Access Key | Secret used to authenticate           |
| Region            | AWS region where you want to work     |
| Output format     | Format in which results are displayed |

For example, `ap-south-1` represents the Mumbai AWS region.

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

AWS Command Line Interface

## **6. Test AWS CLI connectivity**

After configuring AWS CLI, execute the following commands.

**Test 1: Check AWS account identity**

```
aws sts get-caller-identity
```

This displays the AWS account ID and the identity being used.

**Test 2: List S3 buckets**

```
aws s3 ls
```

This displays the S3 buckets available to your configured identity, subject to its permissions.

**Test 3: Check EC2 instances**

```
aws ec2 describe-instances --region ap-south-1
```

This displays EC2 instance information in the Mumbai region, if permitted.

Hands-on verification

If these commands work, your AWS CLI is installed and successfully communicating with AWS.

## **7. Where does AWS CLI store credentials?**

By default, AWS CLI stores configuration in two files:

| File                 | Purpose                         |
| -------------------- | ------------------------------- |
| `~/.aws/credentials` | Stores credentials              |
| `~/.aws/config`      | Stores region and output format |

On Windows:

```
C:\Users\YourUsername\.aws\
    credentials
    config
```

Never upload these files to GitHub or share their contents.





## **8. Frequently asked interview questions**

**Q1. What is AWS CLI?**

AWS CLI is a command-line tool used to interact with and manage AWS services using commands.

**Q2. Why do we use AWS CLI?**

To automate AWS operations, manage resources and integrate AWS services with CI/CD pipelines.

**Q3. What is the difference between AWS CLI and AWS Console?**

AWS Console is GUI-based, whereas AWS CLI is command-based.

**Q4. What is the command to verify AWS CLI installation?**

```
aws --version
```

**Q5. What is the command to configure AWS CLI?**

```
aws configure
```

**Q6. Can we use AWS CLI in Jenkins pipelines?**

Yes. We can execute AWS CLI commands inside Jenkins pipelines to automate tasks such as uploading artifacts to S3, managing EC2 instances and deploying applications.

## **Official AWS documentation**

- [Introduction to AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html?utm_source=chatgpt.com)
- [AWS CLI Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html?utm_source=chatgpt.com)
- [AWS CLI Configuration Guide](https://docs.aws.amazon.com/us_en/cli/latest/userguide/getting-started-quickstart.html?utm_source=chatgpt.com)


# **AWS CLI Commands Cheat Sheet – DevOps Engineer**

Below is a practical AWS CLI command reference covering EC2, S3, IAM, RDS, VPC, EBS, CloudWatch, Lambda and other important AWS services.

These commands are useful for:

- AWS beginners learning command-line operations.
- DevOps engineers managing AWS infrastructure.
- Automating AWS tasks using Shell Scripts and Jenkins pipelines.
- Interview preparation and hands-on practice.

**Before executing commands**, make sure AWS CLI is installed and configured.

```
aws --version
aws configure
aws sts get-caller-identity
```



# **1. EC2 – Elastic Compute Cloud**



EC2 is used to create and manage virtual servers in AWS.

| Requirement                     | AWS CLI command                                                                                                                                                   |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| List EC2 instances              | `aws ec2 describe-instances`                                                                                                                                      |
| List instances in Mumbai        | `aws ec2 describe-instances --region ap-south-1`                                                                                                                  |
| Launch EC2 instance             | `aws ec2 run-instances --image-id ami-xxxxxxxx --instance-type t2.micro --key-name my-key --security-group-ids sg-xxxxxxxx --subnet-id subnet-xxxxxxxx --count 1` |
| Start EC2 instance              | `aws ec2 start-instances --instance-ids i-1234567890abcdef0`                                                                                                      |
| Stop EC2 instance               | `aws ec2 stop-instances --instance-ids i-1234567890abcdef0`                                                                                                       |
| Reboot EC2 instance             | `aws ec2 reboot-instances --instance-ids i-1234567890abcdef0`                                                                                                     |
| Terminate EC2 instance          | `aws ec2 terminate-instances --instance-ids i-1234567890abcdef0`                                                                                                  |
| Get EC2 instance details        | `aws ec2 describe-instances --instance-ids i-1234567890abcdef0`                                                                                                   |
| List EC2 instance types         | `aws ec2 describe-instance-types`                                                                                                                                 |
| List AMIs owned by your account | `aws ec2 describe-images --owners self`                                                                                                                           |
| Create AMI                      | `aws ec2 create-image --instance-id i-1234567890abcdef0 --name ecommerce-server-ami`                                                                              |

**Real-time example:** The development team wants to stop a DEV EC2 instance after office hours to reduce infrastructure costs.

```
aws ec2 stop-instances --instance-ids i-1234567890abcdef0
```

# **2. S3 – Simple Storage Service**

[¿Qué es Amazon Simple Storage Service o Amazon S3?](https://images.openai.com/static-rsc-4/51eOWzJalw2yq_dBMfBxGEGX7-PbAjDQ4mjuwV0FTMjVHoW74eNKBP-AUcHYzVtBu2ArveGRaToy5HGNVghw16DkMlSRTHG6EXhTGKCaIAQcN2UP9TubvKMwGtChLeJENwUbBai-KAqOCj0vvruMcHHO83aWk7q_spx-TaESP1g?purpose=inline)

S3 is used to store images, videos, documents, application backups and static website files.

| Requirement               | AWS CLI command                                                                                     |
| ------------------------- | --------------------------------------------------------------------------------------------------- |
| List all buckets          | `aws s3 ls`                                                                                         |
| Create bucket (Mumbai)    | `aws s3 mb s3://my-demo-bucket --region ap-south-1`                                                 |
| List bucket contents      | `aws s3 ls s3://my-demo-bucket`                                                                     |
| Upload file               | `aws s3 cp index.html s3://my-demo-bucket/`                                                         |
| Upload folder             | `aws s3 cp ./website s3://my-demo-bucket/ --recursive`                                              |
| Download file             | `aws s3 cp s3://my-demo-bucket/index.html .`                                                        |
| Download complete bucket  | `aws s3 cp s3://my-demo-bucket ./backup --recursive`                                                |
| Copy object               | `aws s3 cp s3://my-demo-bucket/index.html s3://my-backup-bucket/`                                   |
| Sync local folder to S3   | `aws s3 sync ./website s3://my-demo-bucket/`                                                        |
| Sync S3 to local folder   | `aws s3 sync s3://my-demo-bucket/ ./website`                                                        |
| Delete an object          | `aws s3 rm s3://my-demo-bucket/index.html`                                                          |
| Delete all bucket objects | `aws s3 rm s3://my-demo-bucket --recursive`                                                         |
| Remove empty bucket       | `aws s3 rb s3://my-demo-bucket`                                                                     |
| Enable versioning         | `aws s3api put-bucket-versioning --bucket my-demo-bucket --versioning-configuration Status=Enabled` |
| Check versioning          | `aws s3api get-bucket-versioning --bucket my-demo-bucket`                                           |

**Real-time example:** The e-commerce development team wants to upload product images to S3.

```
aws s3 cp mobile.jpg s3://my-demo-bucket/product-images/
```

# **3. IAM – Identity and Access Management**



IAM manages users, groups, roles and permissions in AWS.

| Requirement                       | AWS CLI command                                                                                                   |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| List IAM users                    | `aws iam list-users`                                                                                              |
| Create IAM user                   | `aws iam create-user --user-name developer`                                                                       |
| Get user details                  | `aws iam get-user --user-name developer`                                                                          |
| Delete IAM user                   | `aws iam delete-user --user-name developer`                                                                       |
| Create IAM group                  | `aws iam create-group --group-name Developers`                                                                    |
| List IAM groups                   | `aws iam list-groups`                                                                                             |
| Add user to group                 | `aws iam add-user-to-group --user-name developer --group-name Developers`                                         |
| List group users                  | `aws iam get-group --group-name Developers`                                                                       |
| Create IAM role                   | `aws iam create-role --role-name EC2-S3-Role --assume-role-policy-document file://trust-policy.json`              |
| List IAM roles                    | `aws iam list-roles`                                                                                              |
| Attach AWS managed policy to user | `aws iam attach-user-policy --user-name developer --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess`    |
| Attach policy to group            | `aws iam attach-group-policy --group-name Developers --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess` |
| List user policies                | `aws iam list-attached-user-policies --user-name developer`                                                       |
| Detach policy from user           | `aws iam detach-user-policy --user-name developer --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess`    |

**Real-time example:** A developer needs read-only access to S3 buckets.

```
aws iam attach-user-policy \
--user-name developer \
--policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
```

# **4. RDS – Relational Database Service**



RDS is used to create and manage relational databases such as MySQL, PostgreSQL and MariaDB.

| Requirement           | AWS CLI command                                                                                                                                                                                |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| List RDS instances    | `aws rds describe-db-instances`                                                                                                                                                                |
| Create MySQL database | `aws rds create-db-instance --db-instance-identifier ecommerce-db --db-instance-class db.t3.micro --engine mysql --master-username admin --manage-master-user-password --allocated-storage 20` |
| Get DB details        | `aws rds describe-db-instances --db-instance-identifier ecommerce-db`                                                                                                                          |
| Start database        | `aws rds start-db-instance --db-instance-identifier ecommerce-db`                                                                                                                              |
| Stop database         | `aws rds stop-db-instance --db-instance-identifier ecommerce-db`                                                                                                                               |
| Reboot database       | `aws rds reboot-db-instance --db-instance-identifier ecommerce-db`                                                                                                                             |
| Delete database       | `aws rds delete-db-instance --db-instance-identifier ecommerce-db --skip-final-snapshot`                                                                                                       |
| List DB snapshots     | `aws rds describe-db-snapshots`                                                                                                                                                                |
| Create DB snapshot    | `aws rds create-db-snapshot --db-instance-identifier ecommerce-db --db-snapshot-identifier ecommerce-db-backup`                                                                                |

**Real-time example:** The DevOps engineer needs to take a backup before applying database changes.

```
aws rds create-db-snapshot \
--db-instance-identifier ecommerce-db \
--db-snapshot-identifier ecommerce-db-backup
```

# **5. EBS – Elastic Block Store**



EBS provides block storage volumes for EC2 instances.

| Requirement          | AWS CLI command                                                                             |
| -------------------- | ------------------------------------------------------------------------------------------- |
| List EBS volumes     | `aws ec2 describe-volumes`                                                                  |
| Create EBS volume    | `aws ec2 create-volume --availability-zone ap-south-1a --size 10 --volume-type gp3`         |
| Attach volume to EC2 | `aws ec2 attach-volume --volume-id vol-xxxxxxxx --instance-id i-xxxxxxxx --device /dev/sdf` |
| Detach volume        | `aws ec2 detach-volume --volume-id vol-xxxxxxxx`                                            |
| Delete volume        | `aws ec2 delete-volume --volume-id vol-xxxxxxxx`                                            |
| Create snapshot      | `aws ec2 create-snapshot --volume-id vol-xxxxxxxx --description "Ecommerce backup"`         |
| List snapshots       | `aws ec2 describe-snapshots --owner-ids self`                                               |
| Delete snapshot      | `aws ec2 delete-snapshot --snapshot-id snap-xxxxxxxx`                                       |

**Real-time example:** The e-commerce application server needs additional storage for application logs.

```
aws ec2 create-volume \
--availability-zone ap-south-1a \
--size 20 \
--volume-type gp3
```

# **6. VPC – Virtual Private Cloud**



VPC provides an isolated virtual network in AWS.

| Requirement             | AWS CLI command                                                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| List VPCs               | `aws ec2 describe-vpcs`                                                                                                  |
| Create VPC              | `aws ec2 create-vpc --cidr-block 10.0.0.0/16`                                                                            |
| Get VPC details         | `aws ec2 describe-vpcs --vpc-ids vpc-xxxxxxxx`                                                                           |
| Create subnet           | `aws ec2 create-subnet --vpc-id vpc-xxxxxxxx --cidr-block 10.0.1.0/24 --availability-zone ap-south-1a`                   |
| List subnets            | `aws ec2 describe-subnets`                                                                                               |
| Create Internet Gateway | `aws ec2 create-internet-gateway`                                                                                        |
| List Internet Gateways  | `aws ec2 describe-internet-gateways`                                                                                     |
| Attach Internet Gateway | `aws ec2 attach-internet-gateway --internet-gateway-id igw-xxxxxxxx --vpc-id vpc-xxxxxxxx`                               |
| Create route table      | `aws ec2 create-route-table --vpc-id vpc-xxxxxxxx`                                                                       |
| List route tables       | `aws ec2 describe-route-tables`                                                                                          |
| Create security group   | `aws ec2 create-security-group --group-name ecommerce-sg --description "Ecommerce security group" --vpc-id vpc-xxxxxxxx` |
| List security groups    | `aws ec2 describe-security-groups`                                                                                       |
| Allow HTTP traffic      | `aws ec2 authorize-security-group-ingress --group-id sg-xxxxxxxx --protocol tcp --port 80 --cidr 0.0.0.0/0`              |

**Real-time example:** The e-commerce website needs to allow customers to access the application over HTTP port 80.

```
aws ec2 authorize-security-group-ingress \
--group-id sg-xxxxxxxx \
--protocol tcp \
--port 80 \
--cidr 0.0.0.0/0
```

# **7. ELB – Elastic Load Balancing**



ELB distributes incoming application traffic across multiple EC2 instances.

| Requirement                      | AWS CLI command                                                                                                                                                 |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| List load balancers              | `aws elbv2 describe-load-balancers`                                                                                                                             |
| Create Application Load Balancer | `aws elbv2 create-load-balancer --name ecommerce-alb --subnets subnet-aaa subnet-bbb --security-groups sg-xxxxxxxx --scheme internet-facing --type application` |
| List target groups               | `aws elbv2 describe-target-groups`                                                                                                                              |
| Create target group              | `aws elbv2 create-target-group --name ecommerce-tg --protocol HTTP --port 80 --vpc-id vpc-xxxxxxxx`                                                             |
| Register EC2 target              | `aws elbv2 register-targets --target-group-arn TARGET_GROUP_ARN --targets Id=i-xxxxxxxx`                                                                        |
| Check target health              | `aws elbv2 describe-target-health --target-group-arn TARGET_GROUP_ARN`                                                                                          |
| List listeners                   | `aws elbv2 describe-listeners --load-balancer-arn ALB_ARN`                                                                                                      |

**Real-time example:** Register two EC2 instances with the e-commerce application's target group.

```
aws elbv2 register-targets \
--target-group-arn TARGET_GROUP_ARN \
--targets Id=i-11111111111111111 Id=i-22222222222222222
```

# **8. Auto Scaling**



Auto Scaling automatically increases or decreases EC2 instances based on demand and scaling policies.

| Requirement               | AWS CLI command                                                                                                                                                                                                                         |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| List Auto Scaling groups  | `aws autoscaling describe-auto-scaling-groups`                                                                                                                                                                                          |
| Create Auto Scaling group | `aws autoscaling create-auto-scaling-group --auto-scaling-group-name ecommerce-asg --launch-template LaunchTemplateId=lt-xxxxxxxx,Version=1 --min-size 1 --max-size 3 --desired-capacity 2 --vpc-zone-identifier subnet-aaa,subnet-bbb` |
| Increase desired capacity | `aws autoscaling set-desired-capacity --auto-scaling-group-name ecommerce-asg --desired-capacity 3`                                                                                                                                     |
| Decrease desired capacity | `aws autoscaling set-desired-capacity --auto-scaling-group-name ecommerce-asg --desired-capacity 1`                                                                                                                                     |
| Suspend scaling processes | `aws autoscaling suspend-processes --auto-scaling-group-name ecommerce-asg`                                                                                                                                                             |
| Resume scaling processes  | `aws autoscaling resume-processes --auto-scaling-group-name ecommerce-asg`                                                                                                                                                              |
| Delete Auto Scaling group | `aws autoscaling delete-auto-scaling-group --auto-scaling-group-name ecommerce-asg --force-delete`                                                                                                                                      |

**Real-time example:** During a sale, customer traffic increases. The DevOps engineer increases the desired EC2 count from 2 to 3.

```
aws autoscaling set-desired-capacity \
--auto-scaling-group-name ecommerce-asg \
--desired-capacity 3
```

# **9. CloudWatch**


CloudWatch is used to monitor AWS resources, metrics, logs and alarms.

| Requirement             | AWS CLI command                                                                                                                                                                                                                           |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| List CloudWatch alarms  | `aws cloudwatch describe-alarms`                                                                                                                                                                                                          |
| Get EC2 CPU utilization | `aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name CPUUtilization --dimensions Name=InstanceId,Value=i-xxxxxxxx --start-time 2026-11-24T00:00:00Z --end-time 2026-11-25T00:00:00Z --period 300 --statistics Average` |
| Create log group        | `aws logs create-log-group --log-group-name /ecommerce/application`                                                                                                                                                                       |
| List log groups         | `aws logs describe-log-groups`                                                                                                                                                                                                            |
| List log streams        | `aws logs describe-log-streams --log-group-name /ecommerce/application`                                                                                                                                                                   |
| Get log events          | `aws logs get-log-events --log-group-name /ecommerce/application --log-stream-name application-stream`                                                                                                                                    |
| Delete log group        | `aws logs delete-log-group --log-group-name /ecommerce/application`                                                                                                                                                                       |

**Real-time example:** The DevOps team wants to monitor EC2 CPU utilization to troubleshoot high server usage.

```
aws cloudwatch get-metric-statistics \
--namespace AWS/EC2 \
--metric-name CPUUtilization \
--dimensions Name=InstanceId,Value=i-xxxxxxxx \
--start-time 2026-11-24T00:00:00Z \
--end-time 2026-11-25T00:00:00Z \
--period 300 \
--statistics Average
```

# **10. Lambda**



Lambda allows us to execute code without managing servers.

| Requirement            | AWS CLI command                                                                                                                                                                                                 |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| List Lambda functions  | `aws lambda list-functions`                                                                                                                                                                                     |
| Get function details   | `aws lambda get-function --function-name ecommerce-function`                                                                                                                                                    |
| Create Lambda function | `aws lambda create-function --function-name ecommerce-function --runtime python3.12 --role arn:aws:iam::123456789012:role/lambda-role --handler lambda_function.lambda_handler --zip-file fileb://function.zip` |
| Invoke Lambda          | `aws lambda invoke --function-name ecommerce-function response.json`                                                                                                                                            |
| Update Lambda code     | `aws lambda update-function-code --function-name ecommerce-function --zip-file fileb://function.zip`                                                                                                            |
| Delete Lambda          | `aws lambda delete-function --function-name ecommerce-function`                                                                                                                                                 |

**Real-time example:** Whenever a customer uploads a product image to S3, a Lambda function can automatically process the image.

# **11. Route 53**



Route 53 is used for DNS management and domain routing.

| Requirement             | AWS CLI command                                                                                                |
| ----------------------- | -------------------------------------------------------------------------------------------------------------- |
| List hosted zones       | `aws route53 list-hosted-zones`                                                                                |
| Get hosted zone details | `aws route53 get-hosted-zone --id Z123456789`                                                                  |
| List DNS records        | `aws route53 list-resource-record-sets --hosted-zone-id Z123456789`                                            |
| Create DNS record       | `aws route53 change-resource-record-sets --hosted-zone-id Z123456789 --change-batch file://dns-record.json`    |
| Delete DNS record       | `aws route53 change-resource-record-sets --hosted-zone-id Z123456789 --change-batch file://delete-record.json` |

**Real-time example:** The company wants to point `www.techpari.in` to its Application Load Balancer using an Alias record.

# **12. DynamoDB**


DynamoDB is a fully managed NoSQL database.

| Requirement    | AWS CLI command                                                                                                                                                                              |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| List tables    | `aws dynamodb list-tables`                                                                                                                                                                   |
| Describe table | `aws dynamodb describe-table --table-name Orders`                                                                                                                                            |
| Create table   | `aws dynamodb create-table --table-name Orders --attribute-definitions AttributeName=OrderId,AttributeType=S --key-schema AttributeName=OrderId,KeyType=HASH --billing-mode PAY_PER_REQUEST` |
| Insert item    | `aws dynamodb put-item --table-name Orders --item '{"OrderId":{"S":"101"},"CustomerName":{"S":"Rahul"}}'`                                                                                    |
| Get item       | `aws dynamodb get-item --table-name Orders --key '{"OrderId":{"S":"101"}}'`                                                                                                                  |
| Scan table     | `aws dynamodb scan --table-name Orders`                                                                                                                                                      |
| Delete item    | `aws dynamodb delete-item --table-name Orders --key '{"OrderId":{"S":"101"}}'`                                                                                                               |
| Delete table   | `aws dynamodb delete-table --table-name Orders`                                                                                                                                              |

**Real-time example:** The e-commerce application stores customer order details in a DynamoDB table.

# **13. SQS – Simple Queue Service**



SQS is used to exchange messages between distributed application components.

| Requirement     | AWS CLI command                                                                  |
| --------------- | -------------------------------------------------------------------------------- |
| List queues     | `aws sqs list-queues`                                                            |
| Create queue    | `aws sqs create-queue --queue-name ecommerce-orders`                             |
| Get queue URL   | `aws sqs get-queue-url --queue-name ecommerce-orders`                            |
| Send message    | `aws sqs send-message --queue-url QUEUE_URL --message-body "New Order Received"` |
| Receive message | `aws sqs receive-message --queue-url QUEUE_URL`                                  |
| Delete message  | `aws sqs delete-message --queue-url QUEUE_URL --receipt-handle RECEIPT_HANDLE`   |
| Delete queue    | `aws sqs delete-queue --queue-url QUEUE_URL`                                     |

**Real-time example:** When a customer places an order, the application sends an order-processing message to SQS.

# **14. SNS – Simple Notification Service**



SNS is used to send notifications through email, SMS and other supported endpoints.

| Requirement        | AWS CLI command                                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------------ |
| List SNS topics    | `aws sns list-topics`                                                                                  |
| Create topic       | `aws sns create-topic --name ecommerce-alerts`                                                         |
| Subscribe email    | `aws sns subscribe --topic-arn TOPIC_ARN --protocol email --notification-endpoint student@example.com` |
| Publish message    | `aws sns publish --topic-arn TOPIC_ARN --message "EC2 CPU utilization is high"`                        |
| List subscriptions | `aws sns list-subscriptions`                                                                           |
| Delete topic       | `aws sns delete-topic --topic-arn TOPIC_ARN`                                                           |

**Real-time example:** The DevOps team wants to receive an email notification when an application server experiences an issue.

# **15. CloudTrail**


CloudTrail records account activity and API events for auditing.

| Requirement        | AWS CLI command                                                                       |
| ------------------ | ------------------------------------------------------------------------------------- |
| List trails        | `aws cloudtrail describe-trails`                                                      |
| List recent events | `aws cloudtrail lookup-events`                                                        |
| Get trail status   | `aws cloudtrail get-trail-status --name my-trail`                                     |
| Create trail       | `aws cloudtrail create-trail --name ecommerce-trail --s3-bucket-name my-audit-bucket` |
| Start logging      | `aws cloudtrail start-logging --name ecommerce-trail`                                 |
| Stop logging       | `aws cloudtrail stop-logging --name ecommerce-trail`                                  |

**Real-time example:** The security team wants to identify who terminated an EC2 instance.

```
aws cloudtrail lookup-events \
--lookup-attributes AttributeKey=EventName,AttributeValue=TerminateInstances
```

# **16. ECR – Elastic Container Registry**



ECR is used to store Docker container images.

| Requirement       | AWS CLI command                                                                                                                                 |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| List repositories | `aws ecr describe-repositories`                                                                                                                 |
| Create repository | `aws ecr create-repository --repository-name ecommerce-app`                                                                                     |
| Login to ECR      | `aws ecr get-login-password --region ap-south-1 \\| docker login --username AWS --password-stdin 123456789012.dkr.ecr.ap-south-1.amazonaws.com` |
| List images       | `aws ecr list-images --repository-name ecommerce-app`                                                                                           |
| Describe images   | `aws ecr describe-images --repository-name ecommerce-app`                                                                                       |
| Delete image      | `aws ecr batch-delete-image --repository-name ecommerce-app --image-ids imageTag=v1`                                                            |
| Delete repository | `aws ecr delete-repository --repository-name ecommerce-app --force`                                                                             |

**Real-time example:** The DevOps engineer builds a Docker image using Jenkins and pushes it to AWS ECR.

```
docker build -t ecommerce-app:v1 .
```

```
docker tag ecommerce-app:v1 \
123456789012.dkr.ecr.ap-south-1.amazonaws.com/ecommerce-app:v1
```

```
docker push \
123456789012.dkr.ecr.ap-south-1.amazonaws.com/ecommerce-app:v1
```

# **17. Secrets Manager**



Secrets Manager stores sensitive information such as database passwords and API credentials.

| Requirement     | AWS CLI command                                                                                                  |
| --------------- | ---------------------------------------------------------------------------------------------------------------- |
| List secrets    | `aws secretsmanager list-secrets`                                                                                |
| Create secret   | `aws secretsmanager create-secret --name ecommerce/db-password --secret-string 'MyExamplePassword123!'`          |
| Retrieve secret | `aws secretsmanager get-secret-value --secret-id ecommerce/db-password`                                          |
| Update secret   | `aws secretsmanager put-secret-value --secret-id ecommerce/db-password --secret-string 'NewExamplePassword456!'` |
| Delete secret   | `aws secretsmanager delete-secret --secret-id ecommerce/db-password`                                             |

**Real-time example:** An application needs the database password without hardcoding it in the application source code.

# **18. Additional useful AWS CLI commands**

These commands are useful across almost all AWS services.

| Requirement                  | Command                                                                        |
| ---------------------------- | ------------------------------------------------------------------------------ |
| Check AWS identity           | `aws sts get-caller-identity`                                                  |
| List configured profiles     | `aws configure list-profiles`                                                  |
| Check current configuration  | `aws configure list`                                                           |
| Use a particular profile     | `aws s3 ls --profile dev`                                                      |
| Change default region        | `aws configure set region ap-south-1`                                          |
| Display output as table      | `aws ec2 describe-instances --output table`                                    |
| Display output as JSON       | `aws ec2 describe-instances --output json`                                     |
| Filter running EC2 instances | `aws ec2 describe-instances --filters Name=instance-state-name,Values=running` |
| Get AWS CLI help             | `aws help`                                                                     |
| Get EC2 command help         | `aws ec2 help`                                                                 |

## **19. Important AWS CLI options**

| Option      | Purpose                    | Example                                             |
| ----------- | -------------------------- | --------------------------------------------------- |
| `--region`  | Specify AWS region         | `--region ap-south-1`                               |
| `--profile` | Use a specific AWS profile | `--profile dev`                                     |
| `--output`  | Specify output format      | `--output table`                                    |
| `--query`   | Filter command output      | `--query 'Reservations[*].Instances[*].InstanceId'` |
| `--filters` | Filter AWS resources       | `--filters Name=instance-state-name,Values=running` |

## **20. Practice assignments for students**

Here are some practical assignments you can give your students after teaching AWS CLI.

**Assignment 1 – EC2 Management**

Beginner

- List all EC2 instances.
- Start an EC2 instance.
- Stop an EC2 instance.
- Display running instances only.

  **Assignment 2 – S3 Management**

Beginner

- Create an S3 bucket.
- Upload an HTML file.
- List bucket objects.
- Download the HTML file.
- Enable bucket versioning.

  **Assignment 3 – IAM Management**

Intermediate

- Create an IAM user.
- Create a Developers group.
- Add the user to the group.
- Attach S3 read-only permissions.

  **Assignment 4 – RDS Management**

Intermediate

- List RDS databases.
- Get database details.
- Create a database snapshot.
- Identify the database endpoint.

  **Assignment 5 – DevOps Automation**

Advanced

- Build a Docker image.
- Push the image to ECR.
- Deploy the application on EC2.
- Upload application artifacts to S3.
- Monitor EC2 using CloudWatch.

## **Note**

1. Replace sample IDs such as `i-xxxxxxxx`, `sg-xxxxxxxx` and `vpc-xxxxxxxx` with actual AWS resource IDs.
2. Commands that create, stop, terminate or delete resources can have cost or availability consequences. Verify before executing.
3. Never commit AWS access keys or secrets to GitHub.
4. Prefer IAM roles, IAM Identity Center and temporary credentials over long-lived access keys.
5. Some commands require additional configuration, permissions, resource dependencies or JSON input files.




