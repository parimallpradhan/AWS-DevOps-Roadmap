## **1. What is Amazon S3?**

Amazon S3 is an object storage service provided by AWS. We can store different types of data such as:

- Images and videos
- Documents and PDF files
- Application logs
- Database backups
- Static website files
- Application deployment packages



<img width="923" height="616" alt="image" src="https://github.com/user-attachments/assets/0719fb86-dab5-4f53-b183-3bcc391b0f99" />



## **Real-time example:**

Imagine an e-commerce application like Amazon.

When a customer uploads a product image, we can store that image in an S3 bucket.

For example:

- Customer uploads a mobile phone image.
- Application sends the image to S3.
- S3 stores the image as an object.
- Application retrieves the image whenever required.



<img width="926" height="342" alt="image" src="https://github.com/user-attachments/assets/10888a88-c24c-4dc1-8dc8-8262ad0c5c20" />


## **Important S3 terminology or components**

| Component  | Meaning                                | Example             |
| ---------- | -------------------------------------- | ------------------- |
| Bucket     | Container to store objects             | ecommerce-images    |
| Object     | Actual file                            | mobile.jpg          |
| Key        | Unique object identifier within bucket | products/mobile.jpg |
| Region     | AWS geographical location              | ap-south-1          |
| Version ID | Identifies a particular version        | Version 123abc      |

<img width="942" height="635" alt="image" src="https://github.com/user-attachments/assets/7f533c50-9f17-4e0f-95c5-6c84e81963e5" />


# **2. S3 Versioning**

## **What is S3 Versioning?**

S3 Versioning allows us to maintain multiple versions of the same object inside an S3 bucket.

Whenever we upload a new file with the same object key, S3 keeps the previous version instead of simply replacing it.

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/ffbbd4df-a02e-4436-8153-5f93b31f26f4" />


### **Problem statement**



The e-commerce development team stores product images in an S3 bucket named ecommerce-product-images.

Initially, the team uploads a mobile phone image.

Later, the developer replaces the mobile image with a new image. After that, another developer accidentally uploads a laptop image using the same object key.

The original mobile image is no longer the current version.

The company wants to maintain previous versions of product images so that accidentally overwritten images can be recovered.


Requirements:
- Enable S3 Versioning.
- Maintain multiple versions of product images.
- Recover an older version when required.
- Verify version IDs in the S3 Console.

## How can the DevOps team recover the previous file?

### **Solution**

Enable S3 Versioning.

1. Open AWS Console.
2. Search for S3.
3. Create a bucket or open an existing bucket.
4. Go to Properties.
5. Find Bucket Versioning.
6. Select Edit.
7. Enable Versioning.
8. Save changes.
9. Upload a file.
10. Modify the file and upload it again using the same key.
11. Open the file's versions to see previous versions.

**Advantages**

- Recover accidentally overwritten files.
- Recover deleted objects.
- Maintain file history.
- Protect important documents.
- Support data recovery.

**Important:** When versioning is enabled, deleting an object normally creates a Delete Marker rather than permanently deleting all versions.

# **3. S3 Replication**


## **What is S3 Replication?**

S3 Replication automatically copies objects from one S3 bucket to another S3 bucket.

We use replication for:

- Disaster recovery
- Data backup
- Compliance requirements
- Maintaining copies in multiple AWS Regions

There are two important types.

### **A. Cross-Region Replication (CRR)**

CRR copies objects from one AWS Region to another AWS Region.

**Real-time example:**

A company has its primary application in Mumbai (ap-south-1).

For disaster recovery, it wants to maintain another copy of important files in Singapore (ap-southeast-1).



**Architecture**

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/853c9e82-6ce8-46df-990e-d09f8d586bb3" />


### **B. Same-Region Replication (SRR)**

SRR copies objects between two S3 buckets in the same AWS Region.

**Example:**

- Production bucket: ecommerce-prod
- Backup bucket: ecommerce-backup
- Both buckets are in Mumbai.



### **Problem statement**

ABC Bank stores important customer documents, KYC files, loan applications and transaction reports in an Amazon S3 bucket located in the Mumbai Region.

Management is concerned about regional outages and wants to maintain another copy of these documents in the Singapore Region.

The DevOps team needs to configure S3 Cross Region Replication so that eligible new objects uploaded to the Mumbai bucket are automatically replicated to the Singapore bucket.

**Solution:**

Implement Cross-Region Replication.

**Steps:**

1. Create the source S3 bucket in Mumbai.
2. Create the destination S3 bucket in Singapore.
3. Enable Versioning on both buckets.
4. Open the source bucket.
5. Go to Management → Replication rules.
6. Create a replication rule.
7. Select the destination bucket.
8. Configure the IAM role.
9. Save the replication rule.

**Important interview points:**

- Versioning must be enabled on both buckets.
- Replication applies automatically to new objects after the rule is configured.
- Existing objects require an additional operation, such as S3 Batch Replication.
- Replication is asynchronous.
- Replication does not automatically replicate delete markers by default.

# **4. S3 Data Encryption**

## **What is Data Encryption?**

Encryption means converting readable data into an unreadable format so that unauthorized people cannot understand it.

**Real-time example:**

A banking company stores customer information in S3.

For example:

- Customer name
- Account information
- Transaction reports
- Financial documents

The company wants to protect this information.

We use encryption to protect data.

### **Types of S3 Encryption**

**A. Encryption at Rest**

Data is encrypted while stored inside S3.

Common options:

| Encryption | Explanation                                 |
| ---------- | ------------------------------------------- |
| SSE-S3     | AWS manages encryption keys                 |
| SSE-KMS    | AWS KMS manages encryption keys             |
| DSSE-KMS   | Dual-layer server-side encryption using KMS |
| SSE-C      | Customer provides encryption keys           |

**B. Encryption in Transit**

Data is protected while moving between the application and S3.

We generally use HTTPS/TLS.

### **Problem statement**

A banking company stores confidential customer documents in an S3 bucket. It wants to ensure that stored documents are encrypted.

**Solution:**

Enable server-side encryption.

Steps:

1. Open S3.
2. Select your bucket.
3. Go to Properties.
4. Find Default encryption.
5. Click Edit.
6. Select SSE-S3 or SSE-KMS.
7. Save changes.

**Advantages**

- Protects confidential information.
- Helps meet compliance requirements.
- Reduces the risk of unauthorized data exposure.
- Supports secure data storage.

**Interview question:** What is the difference between SSE-S3 and SSE-KMS?

Answer: In SSE-S3, AWS manages the encryption keys. In SSE-KMS, AWS KMS provides additional key management and access-control capabilities.

# **5. S3 Bucket Policies**


## **What is an S3 Bucket Policy?**

An S3 Bucket Policy is a JSON-based resource policy that controls who can access an S3 bucket and what actions they can perform.

We can control:

- Who can access the bucket?
- Who can upload files?
- Who can download files?
- Who can delete objects?
- Whether public access is allowed?


<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/046d2320-c36c-4a5d-a287-b7f8551fdd99" />


**Real-time example:**

Imagine an IT company has three departments:

| Department | Required access          |
| ---------- | ------------------------ |
| Developers | Upload application files |
| QA Team    | Download testing files   |
| Admin Team | Full bucket management   |

We can configure permissions using bucket policies and IAM policies.

### **Architecture diagram**



### **Problem statement**

A company wants to allow a developer to upload files to an S3 bucket but should not allow the developer to delete files.

**Solution:**

Create a bucket policy that allows `s3:PutObject` but does not grant `s3:DeleteObject`.

Example policy:

```

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:user/developer"
      },
      "Action": [
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::company-project-files/*"
    }
  ]
}

```

Replace the account ID, IAM user and bucket name with your actual details.

| JSON Element | Simple Meaning |
|---|---|
| Version | Policy language version |
| Statement | Contains permission rules |
| Sid | Name of the permission rule |
| Effect | Allow or Deny |
| Principal | Who gets the permission |
| Action | What action they can perform |
| Resource | Which S3 bucket or objects are affected |

**Important:** The example grants upload permission only through this policy. Other IAM policies or permissions may also affect the user's effective access.

**Advantages**

- Centralized bucket-level access control.
- Supports cross-account access.
- Restricts unauthorized access.
- Helps implement least-privilege security.

# **6. S3 Storage Classes**

Topic 5 from your image

## **What are S3 Storage Classes?**

S3 Storage Classes help us choose where and how to store data based on how frequently we access it.

Different storage classes have different storage costs, retrieval costs and availability characteristics.

**Real-time example:**

Imagine a company stores 10 years of customer records.

- Current month records: Accessed daily.
- Previous year records: Accessed occasionally.
- 10-year-old records: Rarely accessed.

Should we store everything in the same storage class?

Not necessarily. We can select storage classes based on access requirements.


### **Important S3 Storage Classes**

| Storage Class                 | When to use                                  | Example                    |
| ----------------------------- | -------------------------------------------- | -------------------------- |
| S3 Standard                   | Frequently accessed data                     | Website images             |
| S3 Intelligent-Tiering        | Unknown or changing access patterns          | Business documents         |
| S3 Standard-IA                | Infrequently accessed data                   | Monthly reports            |
| S3 One Zone-IA                | Infrequently accessed, recreatable data      | Secondary backups          |
| S3 Glacier Instant Retrieval  | Archive data requiring millisecond retrieval | Medical records            |
| S3 Glacier Flexible Retrieval | Long-term archive                            | Old financial reports      |
| S3 Glacier Deep Archive       | Very long-term archive                       | Compliance records         |
| S3 Express One Zone           | Very low-latency, high-performance workloads | High-performance analytics |

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/b864f221-7595-4466-ade0-0d7394ea6c00" />

![Uploading image.png…]()


### **Problem statement**

A company stores 5 years of financial reports in S3.

Current reports are accessed daily, but older reports are rarely accessed.

The company wants to reduce storage costs.

**Solution: S3 Lifecycle Management**

We can create lifecycle rules to transition objects automatically between storage classes.

Example:

These are example lifecycle timings, not mandatory AWS defaults.

### **Hands-on**

1. Open S3.
2. Select your bucket.
3. Go to Management.
4. Select Lifecycle rules.
5. Click Create lifecycle rule.
6. Give the rule a name.
7. Choose the objects to which it applies.
8. Configure transition actions.
9. Configure expiration if required.
10. Create the rule.

**Advantages**

- Reduces storage expenses.
- Automates data management.
- Supports long-term data archiving.
- Helps meet retention requirements.

# **7. S3 Logging and Monitoring**

Topic 6 from your image

## **What is S3 Logging and Monitoring?**

Logging and Monitoring help us understand what is happening inside our S3 buckets.

We can monitor:

- Who accessed the bucket?
- When was an object uploaded?
- How many requests were received?
- Was there an unauthorized access attempt?
- How much storage is being used?

### **Important AWS services and features**

| Service / Feature        | Purpose                                      |
| ------------------------ | -------------------------------------------- |
| S3 Server Access Logging | Records detailed bucket access requests      |
| AWS CloudTrail           | Tracks AWS API activity                      |
| CloudWatch               | Monitors metrics and creates alarms          |
| S3 Storage Lens          | Provides storage usage and activity insights |


### **Architecture diagram**


### **Problem statement**

A company stores important business files in S3.

The security team wants to identify who accessed the bucket and monitor unusual activity.

**Solution:**

Use CloudTrail and S3 logging.

**Hands-on:**

1. Open AWS CloudTrail.
2. Create a trail.
3. Configure an S3 bucket to store trail logs.
4. Enable S3 data events for the required bucket.
5. Open Event History to review supported management events.
6. Use CloudWatch metrics to monitor S3 requests and storage-related metrics.

**Important interview point:**

CloudTrail management events and S3 object-level data events are different.

For example:

- Management event: Creating an S3 bucket.
- Data event: Uploading or downloading an S3 object.

# **8. Hosting a Static Website on S3**

Topic 7 from your image

## **What is Static Website Hosting?**

Amazon S3 can host static websites without requiring an EC2 server.

A static website contains files such as:

- HTML
- CSS
- JavaScript
- Images

**Real-time example:**

Imagine a company wants to host its portfolio website.

Instead of creating an EC2 instance and installing Apache or Nginx, it can upload website files to an S3 bucket and enable static website hosting.



### **Architecture diagram**


### **Problem statement**

A small company wants to host its company website.

The website contains:

- index.html
- style.css
- logo.png
- contact.html

The company does not want to manage EC2 instances.

**Solution:**

Use S3 Static Website Hosting.

### **Hands-on steps**

1. Create an S3 bucket.
2. Upload your HTML, CSS and JavaScript files.
3. Open the bucket's Properties.
4. Find Static website hosting.
5. Click Edit.
6. Enable Static website hosting.
7. Select Host a static website.
8. Enter `index.html` as the index document.
9. Save changes.
10. Access the website endpoint.


## [Static Website Project](https://github.com/parimallpradhan/AWS-DevOps-Roadmap/blob/main/S3%20Bucket/Project-2%20-%20Static%20Website%20Hosting%20on%20Amazon%20S3.md)

**Important security point:**

The direct S3 website endpoint does not support HTTPS. For a production website, CloudFront with HTTPS and Origin Access Control is generally a better architecture. The S3 bucket can remain private when configured appropriately.

**Advantages**

- No EC2 server required.
- Easy website deployment.
- Highly scalable.
- Pay for storage and requests.
- Can integrate with CloudFront.

# **9. AWS Snow Family**

Topic 8 from your image

## **What is AWS Snow Family?**

AWS Snow Family provides physical devices to move large amounts of data into and out of AWS.

Imagine a company has 100 TB of data stored in its local data center.

Uploading 100 TB through the internet may take a very long time because of limited internet bandwidth.

AWS Snow Family helps transfer large amounts of data using physical devices.



### **Real-time example**

A media company has 100 TB of video files stored in its local data center.

It wants to migrate all the video files to Amazon S3.

Instead of transferring all data over the internet, the company can use an AWS Snow Family device.

### **Architecture diagram**


### **How does it work?**

1. Company requests a Snow Family device.
2. AWS ships the device to the company.
3. Company connects the device to its local network.
4. Copies its data to the device.
5. Ships the device back to AWS.
6. AWS imports the data into the designated AWS destination, such as S3.

### **Snow Family products**

| Device            | Main purpose                                       |
| ----------------- | -------------------------------------------------- |
| AWS Snowcone      | Smaller edge computing and data transfer workloads |
| AWS Snowball Edge | Large-scale data transfer and edge computing       |

**Advantages**

- Useful for large-scale data migration.
- Reduces dependency on internet bandwidth.
- Supports edge computing workloads.
- Useful for remote locations with limited connectivity.

# **10. AWS Storage Gateway – Hybrid Solution**

Topic 9 from your image

## **What is AWS Storage Gateway?**

AWS Storage Gateway connects an organization's on-premises environment with AWS cloud storage.

It helps companies use both:

- Local data center storage.
- AWS cloud storage.

This is called a Hybrid Cloud Storage Solution.

**Real-time example:**

Imagine a hospital has its own local data center.

It stores patient documents and medical reports on local servers.

The hospital also wants to maintain backups in AWS.

Using AWS Storage Gateway, it can connect its local infrastructure with AWS storage.



### **Architecture diagram**


### **Types of AWS Storage Gateway**

| Type            | Purpose                                                          | Example                   |
| --------------- | ---------------------------------------------------------------- | ------------------------- |
| S3 File Gateway | Access S3 using file protocols such as NFS and SMB               | Shared company files      |
| Volume Gateway  | Provides iSCSI block storage with cloud-backed or stored volumes | Server disk backup        |
| Tape Gateway    | Replaces physical backup tapes with virtual tapes                | Enterprise backup systems |

### **Problem statement**

A company stores 20 TB of files in its local data center.

It wants to maintain cloud backups without completely changing its existing infrastructure.

**Solution:**

Implement AWS Storage Gateway.

### **How it works**

1. Deploy Storage Gateway in the on-premises environment.
2. Configure the gateway.
3. Connect it to AWS.
4. Configure the required storage type.
5. Map the local file shares or storage volumes.
6. Transfer and maintain data in AWS according to the selected gateway type.

**Advantages**

- Hybrid cloud storage.
- Supports existing applications.
- Cloud-based backup.
- Helps reduce dependency on local storage infrastructure.

# **11. Complete AWS S3 Architecture – All Topics Together**

Let's connect all nine topics into one real-time company scenario.

**Scenario: E-commerce Application**

An e-commerce company wants to store product images, customer documents, application backups and website files in AWS S3.

It also wants to implement security, disaster recovery, monitoring and cost optimization.

### **Complete architecture diagram**



### **How the company uses these features**

| Requirement                      | AWS S3 solution        |
| -------------------------------- | ---------------------- |
| Recover previous files           | S3 Versioning          |
| Disaster recovery                | S3 Replication         |
| Protect confidential files       | Data Encryption        |
| Control access                   | Bucket Policies        |
| Reduce storage costs             | Storage Classes        |
| Track access and activity        | Logging and Monitoring |
| Host company website             | Static Website Hosting |
| Transfer huge amounts of data    | AWS Snow Family        |
| Connect local data center to AWS | Storage Gateway        |

# **12. Frequently Asked AWS S3 Interview Questions**

| Interview question                 | Simple answer                                                      |
| ---------------------------------- | ------------------------------------------------------------------ |
| What is Amazon S3?                 | Object storage service provided by AWS.                            |
| What is an S3 bucket?              | A container used to store objects.                                 |
| What is an S3 object?              | A file stored inside an S3 bucket.                                 |
| What is S3 Versioning?             | Maintains multiple versions of objects.                            |
| What is S3 Replication?            | Automatically copies objects between buckets.                      |
| What is CRR?                       | Cross-Region Replication.                                          |
| What is SRR?                       | Same-Region Replication.                                           |
| What is S3 Encryption?             | Protects stored data using encryption.                             |
| What is a Bucket Policy?           | JSON policy controlling bucket access.                             |
| What are S3 Storage Classes?       | Different storage options based on access requirements.            |
| What is S3 Lifecycle Management?   | Automatically transitions or expires objects based on rules.       |
| What is S3 Static Website Hosting? | Hosts static website files using S3.                               |
| What is AWS Snow Family?           | Physical devices for large-scale data transfer and edge computing. |
| What is AWS Storage Gateway?       | Connects on-premises infrastructure with AWS storage.              |
| Can we monitor S3?                 | Yes, using CloudTrail, CloudWatch, S3 logging and Storage Lens.    |



## **Assignments**


1. **Versioning:** Create an S3 bucket, upload a file, modify it, upload it again and restore the previous version.
2. **Replication:** Create two buckets in different AWS Regions and configure CRR.
3. **Encryption:** Enable SSE-S3 or SSE-KMS encryption.
4. **Bucket Policy:** Allow a user to upload objects without granting delete permission.
5. **Lifecycle:** Move objects from S3 Standard to Glacier using lifecycle rules.
6. **Monitoring:** Configure CloudTrail S3 data events and inspect object activity.
7. **Static Website:** Host a basic HTML website using S3.

