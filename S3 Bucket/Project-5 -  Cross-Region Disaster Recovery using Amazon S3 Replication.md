# Project-5 -  Cross-Region Disaster Recovery using Amazon S3 Replication

<img width="1120" height="503" alt="image" src="https://github.com/user-attachments/assets/1b4deef9-75d4-4d68-8585-95768271154f" />


## Problem Statement

A company stores its **application backups and important files** in an Amazon S3 bucket in **us-east-1 (N. Virginia)**.

Although S3 is highly durable, all the data sits in a single AWS Region. If that Region has a major outage or disaster, the company could lose access to its backups exactly when it needs them most.

We need to **automatically replicate the files to another S3 bucket in a different Region (us-west-2, Oregon)**, so that a second copy of the data is always available if a regional failure occurs.

## Project Name

**GeoSafe-S3: Cross-Region Disaster Recovery using Amazon S3 Replication**

## Project Flow

```
Upload file to source bucket (us-east-1) → Replication rule + IAM role → Automatic copy to destination bucket (us-west-2) → Verify the replicated file
```

1. Create a source S3 bucket in `us-east-1` and enable **Versioning**.
2. Create a destination S3 bucket in `us-west-2` and enable **Versioning**.
3. Create a **replication rule** on the source bucket (apply to all objects).
4. Create or select an **IAM role** that S3 uses to replicate the objects.
5. Upload a test file to the source bucket.
6. Open the destination bucket and verify that the file has been replicated.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Architecture](#2-architecture)
3. [Prerequisites](#3-prerequisites)
4. [Step 1: Create the Source Bucket (us-east-1)](#4-step-1-create-the-source-bucket-us-east-1)
5. [Step 2: Enable Versioning on the Source Bucket](#5-step-2-enable-versioning-on-the-source-bucket)
6. [Step 3: Create the Destination Bucket (us-west-2) and Enable Versioning](#6-step-3-create-the-destination-bucket-us-west-2-and-enable-versioning)
7. [Step 4: Create the Replication Rule](#7-step-4-create-the-replication-rule)
8. [Step 5: Choose Scope and Destination](#8-step-5-choose-scope-and-destination)
9. [Step 6: Select the IAM Role and Save the Rule](#9-step-6-select-the-iam-role-and-save-the-rule)
10. [Step 7: Upload a Test File to the Source Bucket](#10-step-7-upload-a-test-file-to-the-source-bucket)
11. [Step 8: Verify the File in the Destination Bucket](#11-step-8-verify-the-file-in-the-destination-bucket)
12. [Troubleshooting](#12-troubleshooting)
13. [Key Learning Outcomes](#13-key-learning-outcomes)

---

## 1. Project Overview

**Cross-Region Replication (CRR)** automatically and asynchronously copies objects from an S3 bucket in one AWS Region to a bucket in a different Region.

**Why use it**

- **Disaster recovery:** a second copy of the data survives a regional failure.
- **Compliance:** some rules require data copies in geographically separate locations.
- **Lower latency:** keep data closer to users in another geography.

**Key points to remember**

- Both buckets must have **Versioning enabled**.
- The source and destination buckets must be in **different Regions**.
- S3 needs an **IAM role** with permission to read from the source and write to the destination.
- Replication applies to objects uploaded **after** the rule is created. Existing objects are not copied unless you choose to replicate them (S3 Batch Replication).
- Replication is **asynchronous**. A file usually appears in the destination within minutes, but it is not instant.

**Tools used:** Amazon S3, AWS IAM, AWS Management Console (and optionally AWS CLI).

---

## 2. Architecture

<img width="2600" height="1480" alt="architecture (2)" src="https://github.com/user-attachments/assets/3a762714-a967-40f4-a0fc-c41774184068" />


| Component | Purpose |
|-----------|---------|
| Source bucket (`us-east-1`) | Stores the original backups and files. Versioning is on |
| Destination bucket (`us-west-2`) | Holds the replicated copy. Versioning is on |
| Replication rule (`Backup-Replication`) | Tells S3 which objects to copy and where |
| IAM role | Gives S3 permission to read from the source and write to the destination |
| DevOps engineer | Uploads files and verifies the replica |

---

## 3. Prerequisites

- An active **AWS account**
- Permission to create S3 buckets and IAM roles
- A test file to upload, such as an image, a text file or the website backup `website-backup.tar.gz` created in the Application Backup project
- Two unique bucket names, for example:
  - Source: `my-source-bucket-us-east-1`
  - Destination: `my-destination-bucket-us-west-2`
- *(Optional)* AWS CLI configured, if you want to verify from the command line

---

## 4. Step 1: Create the Source Bucket (us-east-1)

1. Open **AWS Console → S3 → Create bucket**.
2. Enter a globally unique bucket name, for example `my-source-bucket-us-east-1`.
3. Select the Region **US East (N. Virginia) us-east-1**.

<img width="1254" height="216" alt="image" src="https://github.com/user-attachments/assets/c690785b-ef11-47cd-8601-dc2b8c05bed7" />

4. Keep **Block all public access** enabled.
5. Click **Create bucket**.

<img width="1266" height="466" alt="image" src="https://github.com/user-attachments/assets/126bca10-b667-47a1-bee7-110fb5c51dc8" />


---

## 5. Step 2: Enable Versioning on the Source Bucket

1. Open the source bucket.
2. Go to the **Properties** tab.
3. Under **Bucket Versioning**, click **Edit**.
4. Select **Enable** and click **Save changes**.

<img width="1500" height="225" alt="image" src="https://github.com/user-attachments/assets/b115063f-e8e5-4ecd-832a-493f1f03b7d1" />

<img width="1500" height="253" alt="image" src="https://github.com/user-attachments/assets/e5c8cb4a-d2cb-43b8-8d84-075cebd7c221" />


---

## 6. Step 3: Create the Destination Bucket (us-west-2) and Enable Versioning

1. Go back to **S3 → Create bucket**.
2. Enter a globally unique bucket name, for example `my-destination-bucket-us-west-2`.
3. Select the Region **US West (Oregon) us-west-2**.
4. Click **Create bucket**.
5. Open the destination bucket → **Properties → Bucket Versioning → Edit**.
6. Select **Enable** and click **Save changes**.

<img width="1424" height="333" alt="image" src="https://github.com/user-attachments/assets/88ea483c-27a7-481c-b681-ddef98b68f6a" />

<img width="1381" height="188" alt="image" src="https://github.com/user-attachments/assets/3230d9ad-b800-4908-a367-5c3bfd314710" />


> Versioning must be enabled on **both** buckets. The replication rule cannot be created without it.

---

## 7. Step 4: Create the Replication Rule

1. Open the **source bucket** in the S3 console.

<img width="1304" height="268" alt="image" src="https://github.com/user-attachments/assets/a6379f37-253e-4c83-8fde-6b0d90fbf910" />


2. Go to the **Management** tab.

<img width="1357" height="325" alt="image" src="https://github.com/user-attachments/assets/0907c5ed-6d40-4050-b9ad-4ffc1ea516b1" />


3. Scroll to **Replication rules** and click **Create replication rule**.
4. Enter a **Replication rule name**, such as:
   ```
   Backup-Replication
   ```
5. Keep the **Status** set to **Enabled**.

<img width="1266" height="352" alt="image" src="https://github.com/user-attachments/assets/76350dc7-d19b-45be-8674-9412db1bb465" />


---

## 8. Step 5: Choose Scope and Destination

1. Under **Choose a rule scope**, select **Apply to all objects in the bucket**.

<img width="1368" height="292" alt="image" src="https://github.com/user-attachments/assets/c3c98cf5-9749-49d1-819c-111b66848d23" />


2. Under **Destination**, select **Choose a bucket in this account**.

<img width="1444" height="337" alt="image" src="https://github.com/user-attachments/assets/08d0dc0e-b7cf-4ab8-bf98-200e632e20a2" />



3. Click **Browse S3** and select the destination bucket in `us-west-2` (`my-destination-bucket-us-west-2`).

---

## 9. Step 6: Select the IAM Role and Save the Rule

1. Under **IAM role**, choose **Create new role** (recommended for the demo), or select an existing replication role.

<img width="1417" height="231" alt="image" src="https://github.com/user-attachments/assets/ce60adfd-409e-49a5-b86c-e086309478b5" />


2. Leave the other options at their defaults.
3. Click **Save**.

<img width="1426" height="368" alt="image" src="https://github.com/user-attachments/assets/ad92a9d9-ea9a-4414-b14f-a5a95baf570f" />


4. If S3 asks **Replicate existing objects?**, choose **No, do not replicate existing objects** for this demo, then click **Submit**.
5. Confirm that the rule appears in the list with the status **Enabled**.

> The IAM role lets S3 read objects from the source bucket and write the copies into the destination bucket. A new role is created for you automatically when you choose **Create new role**.

---

## 10. Step 7: Upload a Test File to the Source Bucket

1. Open the **source bucket** → **Objects → Upload**.
2. Click **Add files** and select a test file, such as an image or a text file.
3. Click **Upload**.

**Or upload from the command line:**
```bash
aws s3 cp website-backup.tar.gz s3://my-source-bucket-us-east-1/backups/ --region us-east-1
```

<img width="1335" height="396" alt="image" src="https://github.com/user-attachments/assets/b4820b46-13ae-4014-a050-942735c9be66" />


---

## 11. Step 8: Verify the File in the Destination Bucket

1. Wait a minute or two, then open the **destination bucket** in `us-west-2`.
2. Click **Refresh** and confirm that the uploaded file is listed.

**Or verify from the command line:**
```bash
aws s3 ls s3://my-destination-bucket-us-west-2/ --recursive --region us-west-2
```

<img width="1421" height="543" alt="image" src="https://github.com/user-attachments/assets/868d5ffc-ea4e-4c76-8b05-dd03735f4341" />



**Check the replication status of the file:**
```bash
aws s3api head-object --bucket my-source-bucket-us-east-1 --key backups/website-backup.tar.gz --query ReplicationStatus --region us-east-1
```

| Where | Status | Meaning |
|-------|--------|---------|
| Source object | `PENDING` | Replication is in progress |
| Source object | `COMPLETED` | The copy has reached the destination |
| Source object | `FAILED` | Replication failed. Check the IAM role and rule |
| Destination object | `REPLICA` | This object is a replica |

---

## 12. Troubleshooting

| Problem | Possible Cause | Fix |
|---------|---------------|-----|
| Cannot create the replication rule, versioning error | Versioning is not enabled on one or both buckets | Enable Versioning on both the source and destination buckets |
| Destination bucket cannot be selected | Both buckets are in the same Region, or the destination is in another account | CRR needs two different Regions. For another account, choose that option and enter the account ID and bucket name |
| File not appearing in the destination | Replication is asynchronous, or the rule is disabled | Wait a few minutes, refresh, and confirm the rule status is **Enabled** |
| Files uploaded **before** the rule are missing in the destination | Replication works only for new objects by default | Re-upload the files, or use **S3 Batch Replication** to copy existing objects |
| Replication status is `FAILED` | The IAM role is missing permissions, or it was deleted | Re-create the rule with **Create new role**, or fix the role's permissions |
| `AccessDenied` when creating the rule | Your user lacks permission to create IAM roles or replication rules | Use an account with IAM and S3 admin permissions |
| Object encrypted with a KMS key is not replicated | The rule is not set up for KMS-encrypted objects | Enable replication of KMS-encrypted objects in the rule and grant the role access to the keys |
| Deleted file still exists in the destination | Delete markers are not replicated by default | Turn on **Delete marker replication** in the rule if you want deletes to be copied |
| Cannot find the file in the destination console | Looking in the wrong Region | Switch the console to **us-west-2** and open the destination bucket |

---

## 13. Key Learning Outcomes

- Understood why a single-Region copy is a risk and how **Cross-Region Replication** supports disaster recovery.
- Learned that **Versioning is mandatory** on both the source and destination buckets.
- Learned how to create a **replication rule** that applies to all objects in a bucket.
- Learned the role of the **IAM role** used by S3 to replicate data.
- Learned that replication is **asynchronous** and applies to new objects, and how **Batch Replication** handles existing ones.
- Learned how to verify replication from the console and with `aws s3 ls` and the object's replication status.
- Gained hands-on experience working with S3 buckets in two different AWS Regions.
