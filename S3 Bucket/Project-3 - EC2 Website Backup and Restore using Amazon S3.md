# Project-3 - EC2 Website Backup and Restore using Amazon S3

<img width="1489" height="371" alt="image" src="https://github.com/user-attachments/assets/e0b2a42d-1bd3-4bfd-952a-2f38600bd1f8" />


## Problem Statement

A company hosts its website on an **EC2 Linux server**. If the EC2 instance fails, or the website files are accidentally deleted, the company may lose its website content.

We need to create a **compressed backup** of the website and store it **securely in Amazon S3**, so that the website can be restored whenever required.

## Project Name

**WebBackup-S3: EC2 Website Backup and Restore using Amazon S3**

## Project Flow

```
EC2 website files (/var/www/html) → tar.gz compressed backup → AWS CLI upload (IAM Role) → Amazon S3 bucket → Restore when required
```

1. Create an S3 bucket to store the backups.
2. Create an IAM role with S3 permissions and attach it to the EC2 instance.
3. Connect to the EC2 instance and confirm the website files in `/var/www/html`.
4. Create a compressed backup using `tar`.
5. Upload the backup file to the S3 bucket using `aws s3 cp`.
6. Verify the backup in S3 using `aws s3 ls`.
7. Restore the website from the S3 backup when needed.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Architecture](#2-architecture)
3. [Prerequisites](#3-prerequisites)
4. [Step 1: Create an S3 Bucket](#4-step-1-create-an-s3-bucket)
5. [Step 2: Create an IAM Role and Attach it to EC2](#5-step-2-create-an-iam-role-and-attach-it-to-ec2)
6. [Step 3: Connect to EC2 and Check the Website Files](#6-step-3-connect-to-ec2-and-check-the-website-files)
7. [Step 4: Create a Compressed Backup](#7-step-4-create-a-compressed-backup)
8. [Step 5: Upload the Backup to Amazon S3](#8-step-5-upload-the-backup-to-amazon-s3)
9. [Step 6: Verify the Backup in S3](#9-step-6-verify-the-backup-in-s3)
10. [Step 7: Restore the Website from the Backup](#10-step-7-restore-the-website-from-the-backup)
11. [Step 8: Automate the Backup with Cron (Optional)](#11-step-8-automate-the-backup-with-cron-optional)
12. [Troubleshooting](#12-troubleshooting)
13. [Key Learning Outcomes](#13-key-learning-outcomes)

---

## 1. Project Overview

Data stored only on an EC2 instance is at risk. The instance can fail, be terminated, or someone can delete the website files by mistake.

This project protects the website content by:

- Compressing the website files (`/var/www/html`) into a single `.tar.gz` archive.
- Uploading the archive to an **Amazon S3** bucket, which is durable, secure and independent of the EC2 instance.
- Using an **IAM role** attached to EC2, so no access keys are stored on the server.
- Restoring the files from S3 whenever they are lost or a new server must be set up.

**Tools used:** Amazon EC2 (Linux), Apache web server, `tar`, AWS CLI, Amazon S3, AWS IAM.

---

## 2. Architecture

<img width="2600" height="1480" alt="architecture" src="https://github.com/user-attachments/assets/c5cb8c0d-454d-4b44-8086-ea4ba6fc0064" />


| Component | Purpose |
|-----------|---------|
| EC2 (Linux) + Apache | Hosts the website files in `/var/www/html` |
| `tar` | Creates the compressed backup `website-backup.tar.gz` |
| AWS CLI | Uploads and lists backup files in S3 |
| IAM Role | Gives EC2 permission to access S3 without storing access keys |
| Amazon S3 bucket | Stores the backup files securely and durably |

---

## 3. Prerequisites

- An active **AWS account**
- A running **EC2 Linux instance** hosting a website (Apache) with files in `/var/www/html`
- **AWS CLI** installed on the EC2 instance
- SSH access to the instance (key pair and a Security Group allowing SSH)
- Permission to create S3 buckets and IAM roles
- Basic knowledge of Linux commands

---

## 4. Step 1: Create an S3 Bucket

1. Open **AWS Console → S3 → Create bucket**.
2. Enter a globally unique bucket name. In this demo the bucket is:
   ```
   backupwebdata-01
   ```
3. Select your AWS Region and keep **Block all public access** enabled (backups should stay private).
4. Click **Create bucket**.

> In the demo, the bucket is already created. Use your own bucket name wherever `backupwebdata-01` appears below.

---

## 5. Step 2: Create an IAM Role and Attach it to EC2

1. Open **AWS Console → IAM → Roles → Create role**.
2. **Trusted entity:** AWS service → **Use case:** EC2.
3. Attach S3 permissions:
   - **Demo:** `AmazonS3FullAccess`, as used in the training session.
   - **Recommended (least privilege):** a custom policy limited to the backup bucket:
     ```json
     {
       "Version": "2012-10-17",
       "Statement": [
         {
           "Effect": "Allow",
           "Action": ["s3:PutObject", "s3:GetObject", "s3:ListBucket"],
           "Resource": [
             "arn:aws:s3:::backupwebdata-01",
             "arn:aws:s3:::backupwebdata-01/*"
           ]
         }
       ]
     }
     ```
4. Name the role, for example `EC2-S3-Backup-Role`, and click **Create role**.
5. Attach it to the instance: **EC2 → select instance → Actions → Security → Modify IAM role** → choose the role → **Update IAM role**.

> You can attach an existing role or create a new one and attach it to the EC2 instance.

---

## 6. Step 3: Connect to EC2 and Check the Website Files

1. Connect to the instance:
   ```bash
   ssh -i your-key.pem ubuntu@EC2-PUBLIC-IP
   ```
   *(Use `ec2-user` instead of `ubuntu` on Amazon Linux.)*
2. Check the website files that will be backed up:
   ```bash
   ls -l /var/www/html
   ```
3. Confirm the IAM role is working:
   ```bash
   aws s3 ls
   ```

---

## 7. Step 4: Create a Compressed Backup

Create a compressed archive of the website files:

```bash
tar -czf website-backup.tar.gz /var/www/html
```

| Option | Meaning |
|--------|---------|
| `c` | Create an archive |
| `z` | Compress with gzip |
| `f` | Name of the archive file |

Check the backup file:

```bash
ls -lh website-backup.tar.gz
```
<img width="1388" height="219" alt="image" src="https://github.com/user-attachments/assets/94b72fef-ded9-4e8f-a709-257ad1dc4934" />

---

## 8. Step 5: Upload the Backup to Amazon S3

Upload the backup file to the S3 bucket:

```bash
aws s3 cp website-backup.tar.gz s3://backupwebdata-01/backups/
```

<img width="1403" height="173" alt="image" src="https://github.com/user-attachments/assets/aeb6e48f-48d4-4f2b-b67d-ebefd12f7edd" />

> Replace `backupwebdata-01` with your bucket name. The `backups/` part is a folder (prefix) that keeps backups organised. Without it, the file is uploaded to the bucket root.

---

## 9. Step 6: Verify the Backup in S3

1. List the files from the command line:
   ```bash
   aws s3 ls s3://backupwebdata-01/backups/
   ```
2. Or open **AWS Console → S3 → backupwebdata-01 → backups/** and confirm that `website-backup.tar.gz` is listed.
   
<img width="1455" height="431" alt="image" src="https://github.com/user-attachments/assets/97737a7f-a270-410b-9128-8bf8c60f629f" />

---

## 10. Step 7: Restore the Website from the Backup

If the website files are deleted or you move to a new server:

1. Download the backup from S3:
   ```bash
   aws s3 cp s3://backupwebdata-01/backups/website-backup.tar.gz .
   ```
2. Extract it. The archive stores the path as `var/www/html/...`, so extract from `/`:
   ```bash
   sudo tar -xzf website-backup.tar.gz -C /
   ```
3. Restart Apache and open `http://EC2-PUBLIC-IP` to confirm the website is back:
   ```bash
   sudo systemctl restart apache2
   ```
   *(Use `httpd` instead of `apache2` on Amazon Linux.)*

---

## 11. Step 8: Automate the Backup with Cron (Optional)

Run the backup automatically every day at 2 AM, with the date in the file name so old backups are not overwritten.

1. Create a script `/home/ubuntu/backup.sh`:
   ```bash
   #!/bin/bash
   DATE=$(date +%F)
   tar -czf /tmp/website-backup-$DATE.tar.gz /var/www/html
   aws s3 cp /tmp/website-backup-$DATE.tar.gz s3://backupwebdata-01/backups/
   rm /tmp/website-backup-$DATE.tar.gz
   ```
2. Make it executable:
   ```bash
   chmod +x /home/ubuntu/backup.sh
   ```
3. Open the cron editor with `crontab -e` and add:
   ```
   0 2 * * * /home/ubuntu/backup.sh
   ```

---

## 12. Troubleshooting

| Problem | Possible Cause | Fix |
|---------|---------------|-----|
| `Unable to locate credentials` | IAM role not attached to the EC2 instance | Attach the role: EC2 → Actions → Security → Modify IAM role |
| `AccessDenied` on `aws s3 cp` | The role's policy does not allow S3 access to this bucket | Check the policy and the bucket ARN; attach the correct permissions |
| `NoSuchBucket` | Wrong bucket name or Region | Run `aws s3 ls` and copy the exact bucket name |
| `aws: command not found` | AWS CLI is not installed | Install AWS CLI (`sudo apt install awscli`, or AWS CLI v2 from the AWS documentation) |
| `tar: Removing leading '/' from member names` | Normal warning; `tar` stores relative paths | No action needed. Use `-C /` when restoring |
| `Permission denied` while creating or reading files | Insufficient permissions on the folder or file | Use `sudo`, or create the backup in a folder you own such as `/tmp` or your home folder |
| Backup file not found in S3 | Uploaded to the bucket root, or a different prefix | Run `aws s3 ls s3://backupwebdata-01/ --recursive` to find it |
| Restored website does not load | Apache not restarted, or wrong file ownership | Restart Apache; check ownership with `ls -l /var/www/html` |
| Disk full while creating the backup | Not enough space on EC2 | Check with `df -h`; create the archive in a path with free space and delete it after upload |

---

## 13. Key Learning Outcomes

- Understood why application and website data must be backed up outside the EC2 instance.
- Learned how to create a compressed backup using `tar -czf`.
- Learned how to upload and list backups in S3 using `aws s3 cp` and `aws s3 ls`.
- Learned how to use an **IAM role** so that EC2 can access S3 without storing access keys.
- Understood the difference between demo permissions (full access) and **least-privilege** policies.
- Learned how to **restore** a website from an S3 backup.
- Learned how to automate backups with a shell script and cron.
