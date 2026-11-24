# Project-4 - Apache Log Archiving from EC2 to Amazon S3

<img width="1500" height="642" alt="image" src="https://github.com/user-attachments/assets/38f57e5e-5a8a-48a0-8879-6e809bfe645b" />


## Problem Statement

A company hosts its website on an **EC2 Linux server** running **Apache2**. Apache continuously writes access and error logs on the server's local disk.

If these logs stay only on the EC2 instance:

- They are lost if the instance fails or is terminated.
- They fill up the server disk over time.
- Teams cannot easily access them for troubleshooting, auditing or analysis.

We need a simple and reliable way to **copy the Apache2 log files from EC2 to Amazon S3**, so they are stored safely, kept outside the server, and can be reviewed whenever required.

## Project Name

**LogVault-S3: Apache Log Archiving from EC2 to Amazon S3**

## Project Flow

```
Visitors use website → Apache2 writes logs (/var/log/apache2) → aws s3 cp --recursive (IAM Role) → S3 bucket (apache-logs/) → aws s3 ls to verify
```

1. Create an S3 bucket to store the logs.
2. Create an IAM role with S3 permissions and attach it to the EC2 instance.
3. Connect to the EC2 instance and check the Apache2 log files.
4. Copy the log files to S3 using `aws s3 cp --recursive`.
5. Verify that the files are in S3 using `aws s3 ls`.
6. Check the uploaded log files.
7. (Optional) Apply a lifecycle rule and automate the copy with cron.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Architecture](#2-architecture)
3. [Prerequisites](#3-prerequisites)
4. [Step 1: Create an S3 Bucket](#4-step-1-create-an-s3-bucket)
5. [Step 2: Create an IAM Role and Attach it to EC2](#5-step-2-create-an-iam-role-and-attach-it-to-ec2)
6. [Step 3: Connect to EC2 and Check the Apache2 Log Files](#6-step-3-connect-to-ec2-and-check-the-apache2-log-files)
7. [Step 4: Copy the Log Files to S3](#7-step-4-copy-the-log-files-to-s3)
8. [Step 5: Verify the Files in S3](#8-step-5-verify-the-files-in-s3)
9. [Step 6: Check the Uploaded Log Files](#9-step-6-check-the-uploaded-log-files)
10. [Step 7: Reduce Log Storage Cost with a Lifecycle Rule (Optional)](#10-step-7-reduce-log-storage-cost-with-a-lifecycle-rule-optional)
11. [Step 8: Automate the Log Copy with Cron (Optional)](#11-step-8-automate-the-log-copy-with-cron-optional)
12. [Troubleshooting](#12-troubleshooting)
13. [Key Learning Outcomes](#13-key-learning-outcomes)

---

## 1. Project Overview

Every request to a website is recorded by Apache2 in log files, usually in `/var/log/apache2/`:

| File | What it contains |
|------|------------------|
| `access.log` | Every request made to the website (client IP, page, status code, time) |
| `error.log` | Errors and warnings from the web server |

Logs are valuable for **troubleshooting, security investigation, auditing and traffic analysis**. Keeping them only on the server is risky, so this project copies them to **Amazon S3**, which is durable, low cost and independent of the EC2 instance.

**Tools used:** Amazon EC2 (Linux), Apache2, AWS CLI, Amazon S3, AWS IAM.

---

## 2. Architecture

<img width="2600" height="1480" alt="architecture (1)" src="https://github.com/user-attachments/assets/3d3b1191-0292-4842-be7d-327b99c5d00c" />


| Component | Purpose |
|-----------|---------|
| Website users and browser | Send requests to the website, which creates log entries |
| Apache2 on EC2 | Serves the website and writes logs to `/var/log/apache2/` |
| DevOps engineer | Connects over SSH and runs the copy and verify commands |
| AWS CLI | Copies and lists the log files in S3 |
| IAM Role | Gives EC2 permission to use S3 without storing access keys |
| Amazon S3 bucket | Stores the logs under the `apache-logs/` prefix |

---

## 3. Prerequisites

- An active **AWS account**
- A running **EC2 Linux instance** with **Apache2** installed and a website running
- **AWS CLI** installed on the EC2 instance
- SSH access to the instance (key pair, and a Security Group allowing SSH)
- Permission to create S3 buckets and IAM roles
- Basic knowledge of Linux commands

---

## 4. Step 1: Create an S3 Bucket

1. Open **AWS Console → S3 → Create bucket**.
2. Enter a globally unique bucket name, for example `your-bucket-name`.
3. Select your AWS Region.
4. Keep **Block all public access** enabled (logs can contain visitor IP addresses and should stay private).
5. Click **Create bucket**.

---

## 5. Step 2: Create an IAM Role and Attach it to EC2

1. Open **AWS Console → IAM → Roles → Create role**.
2. **Trusted entity:** AWS service → **Use case:** EC2.
3. Attach S3 permissions:
   - **Demo:** `AmazonS3FullAccess`.
   - **Recommended (least privilege):** a custom policy for this bucket only:
     ```json
     {
       "Version": "2012-10-17",
       "Statement": [
         {
           "Effect": "Allow",
           "Action": ["s3:PutObject", "s3:GetObject", "s3:ListBucket"],
           "Resource": [
             "arn:aws:s3:::your-bucket-name",
             "arn:aws:s3:::your-bucket-name/*"
           ]
         }
       ]
     }
     ```
4. Name the role, for example `EC2-S3-Logs-Role`, and click **Create role**.
5. Attach it to the instance: **EC2 → select instance → Actions → Security → Modify IAM role** → choose the role → **Update IAM role**.

---

## 6. Step 3: Connect to EC2 and Check the Apache2 Log Files

1. Connect to your EC2 instance:
   ```bash
   ssh -i your-key.pem ubuntu@EC2-PUBLIC-IP
   ```
2. Check the Apache2 log files:
   ```bash
   ls -lh /var/log/apache2/
   ```
   You should see files such as `access.log` and `error.log` (and rotated files like `access.log.1` or `access.log.2.gz`).
3. Confirm the IAM role works:
   ```bash
   aws s3 ls
   ```

---

## 7. Step 4: Copy the Log Files to S3

Copy the whole log folder to S3. Replace `your-bucket-name` with your actual bucket name:

```bash
aws s3 cp /var/log/apache2/ s3://your-bucket-name/apache-logs/ --recursive
```

| Part | Meaning |
|------|---------|
| `/var/log/apache2/` | Source folder with the Apache2 logs |
| `s3://your-bucket-name/apache-logs/` | Destination bucket and folder (prefix) |
| `--recursive` | Copy every file inside the folder |

> If you get `Permission denied` on some log files, run the command with `sudo`. The instance role credentials still work with `sudo`.

---

## 8. Step 5: Verify the Files in S3

List the uploaded files from the command line:

```bash
aws s3 ls s3://your-bucket-name/apache-logs/
```

You can also check in the console: **S3 → your bucket → apache-logs/**.

---

## 9. Step 6: Check the Uploaded Log Files

1. Open **AWS Console → S3 → your bucket → apache-logs/**.
2. Select a file such as `access.log` and click **Download** (or **Open**).
3. Confirm the content matches the server log, or compare from the command line:
   ```bash
   aws s3 cp s3://your-bucket-name/apache-logs/access.log /tmp/access.log
   tail -n 5 /tmp/access.log
   ```

---

## 10. Step 7: Reduce Log Storage Cost with a Lifecycle Rule (Optional)

Logs are accessed less and less as they get older. A lifecycle rule moves them to cheaper storage automatically, then deletes them.

1. Create `lifecycle.json`:
   ```json
   {
     "Rules": [
       {
         "ID": "apache-logs-lifecycle",
         "Filter": { "Prefix": "apache-logs/" },
         "Status": "Enabled",
         "Transitions": [
           { "Days": 30, "StorageClass": "STANDARD_IA" },
           { "Days": 90, "StorageClass": "GLACIER" }
         ],
         "Expiration": { "Days": 365 }
       }
     ]
   }
   ```
2. Apply it to the bucket:
   ```bash
   aws s3api put-bucket-lifecycle-configuration --bucket your-bucket-name --lifecycle-configuration file://lifecycle.json
   ```

This rule moves logs to Standard-IA after 30 days, to Glacier Flexible Retrieval after 90 days, and deletes them after 365 days. Adjust the days to match your retention needs.

> This step needs permission for `s3:PutLifecycleConfiguration`, which the least-privilege policy above does not include. Run it with your own admin permissions.

---

## 11. Step 8: Automate the Log Copy with Cron (Optional)

Use `aws s3 sync` so that only new or changed files are uploaded each time.

1. Open the cron editor:
   ```bash
   crontab -e
   ```
2. Add a daily job at 1 AM:
   ```
   0 1 * * * /usr/bin/aws s3 sync /var/log/apache2/ s3://your-bucket-name/apache-logs/
   ```

> If a log file needs `sudo` to read, add the job to root's crontab instead using `sudo crontab -e`.

---

## 12. Troubleshooting

| Problem | Possible Cause | Fix |
|---------|---------------|-----|
| `Unable to locate credentials` | IAM role not attached to the EC2 instance | Attach the role: EC2 → Actions → Security → Modify IAM role |
| `AccessDenied` on `aws s3 cp` | The role's policy does not allow access to this bucket | Check the policy and the bucket ARN |
| `NoSuchBucket` | Wrong bucket name or Region | Run `aws s3 ls` and copy the exact bucket name |
| `ls: cannot access '/var/log/apache2/'` | Apache2 is not installed, or this is Amazon Linux | Install Apache2 (`sudo apt install apache2`); on Amazon Linux logs are in `/var/log/httpd/` |
| `Permission denied` / `Failed to read file` | Log files are readable only by root or the `adm` group | Run the command with `sudo` |
| Folder uploaded but nothing listed | Missing trailing slash or wrong prefix | Run `aws s3 ls s3://your-bucket-name/ --recursive` to see all files |
| `access.log` in S3 is smaller than on the server | The log is still being written while copying | Copy again later, or copy the rotated files (`access.log.1`, `*.gz`) |
| Same files uploaded again and again | `cp` re-uploads everything every time | Use `aws s3 sync` to upload only new or changed files |
| Cron job does not run | Wrong path to `aws` or missing permissions | Use the full path (`which aws`) and check `/var/log/syslog` for cron errors |

---

## 13. Key Learning Outcomes

- Understood why server logs should be stored outside the EC2 instance.
- Learned where Apache2 stores its logs and how to inspect them with `ls -lh`.
- Learned how to copy a whole folder to S3 using `aws s3 cp --recursive`.
- Learned how to verify uploads using `aws s3 ls` and the S3 console.
- Learned how to use an **IAM role** so that EC2 can access S3 without storing access keys.
- Learned how an **S3 lifecycle rule** reduces cost by moving old logs to cheaper storage classes.
- Learned the difference between `aws s3 cp` and `aws s3 sync`, and how to automate with cron.
