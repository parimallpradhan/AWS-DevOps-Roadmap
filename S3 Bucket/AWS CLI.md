# **AWS CLI (Command Line Interface)**


# **Jira Ticket: AWS CLI Installation and Configuration**

AWS

Beginner

DevOps Engineer

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

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

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

AWS Command Line Interface+1

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


