# Project : Shopping Website Product Images using Amazon S3 + EC2

**Project Name:** Shopping Website Product Images – EC2 Web Server + Amazon S3 Image Storage

**Project Flow:**

```
Seller uploads images → S3 Bucket (private) → IAM Role (read-only) → EC2 (Ubuntu + Apache) → Customer opens website
```

1. Create a private S3 bucket and upload the product images.
2. Create an IAM role with read-only access to the bucket.
3. Launch an Ubuntu EC2 instance and attach the IAM role.
4. Install Apache and AWS CLI on EC2.
5. Pull the product images from S3 to the web root using AWS CLI.
6. Create `index.html` and browse the website using the EC2 public IP.



---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Architecture](#2-architecture)
3. [Prerequisites](#3-prerequisites)
4. [Step 1: Create an S3 Bucket](#4-step-1-create-an-s3-bucket)
5. [Step 2: Upload Product Images](#5-step-2-upload-product-images)
6. [Step 3: Create an IAM Role with S3 Read-Only Access](#6-step-3-create-an-iam-role-with-s3-read-only-access)
7. [Step 4: Launch an Ubuntu EC2 Instance and Attach the IAM Role](#7-step-4-launch-an-ubuntu-ec2-instance-and-attach-the-iam-role)
8. [Step 5: Install Apache and AWS CLI](#8-step-5-install-apache-and-aws-cli)
9. [Step 6: Download Product Images from S3 to EC2](#9-step-6-download-product-images-from-s3-to-ec2)
10. [Step 7: Create the Shopping Website (index.html)](#10-step-7-create-the-shopping-website-indexhtml)
11. [Step 8: Verify the Website](#11-step-8-verify-the-website)
12. [Troubleshooting](#12-troubleshooting)
13. [Key Learning Outcomes](#13-key-learning-outcomes)

---

## 1. Project Overview

An online shopping company has an e-commerce website hosted on an EC2 server. Sellers regularly upload product images such as:

- `mobile.jpg`
- `laptop.jpg`
- `headphones.jpg`
- `shoes.jpg`

**The problem:** Initially, all product images are stored directly on the EC2 server along with the website files. As the business grows and thousands of product images need to be stored:

- EC2 disk usage keeps increasing.
- Image management becomes difficult.
- If multiple EC2 servers are used for high availability, keeping the same images on every server becomes complicated.

**The solution:** Use **Amazon S3** for product image storage while keeping the website on **EC2**.

- **EC2** hosts the shopping website (Apache web server).
- **S3** stores the product images (durable, scalable, centrally managed).
- When a customer opens the website, `index.html` is served from EC2 and the product images are delivered from the image set stored in S3.

> EC2 is used for the shopping website, and S3 is used to store the product images.

---



## 2. Architecture

<img width="936" height="676" alt="image" src="https://github.com/user-attachments/assets/b6461916-f325-4cc4-8336-faac2a40e9e2" />

```
                 +-----------------------+
                 |   Seller / Admin      |
                 |  uploads mobile.jpg,  |
                 |  laptop.jpg ...       |
                 +-----------+-----------+
                             |
                             v
                 +-----------------------+
                 |   Amazon S3 Bucket    |
                 |  (Block Public Access |
                 |       = ON)           |
                 +-----------+-----------+
                             ^
                             | read-only (s3:GetObject, s3:ListBucket)
                 +-----------+-----------+
                 |       IAM Role        |
                 |  (attached to EC2)    |
                 +-----------+-----------+
                             |
                 +-----------+-----------+
                 |   EC2 (Ubuntu)        |
                 |   Apache2 Web Server  |
                 |   /var/www/html/      |
                 |    - index.html       |
                 |    - mobile.jpg       |
                 |    - laptop.jpg       |
                 +-----------+-----------+
                             |
                    HTTP (Port 80)
                             |
                             v
                 +-----------------------+
                 |  Customer's Browser   |
                 +-----------------------+
```

| Component | Purpose |
|-----------|---------|
| Amazon S3 | Central, durable storage for product images |
| IAM Role | Gives EC2 secure read-only access to the bucket (no access keys stored on the server) |
| EC2 (Ubuntu) | Hosts the website |
| Apache2 | Web server serving `index.html` |
| Security Group | Allows HTTP (80) and restricted SSH (22) |

---

## 3. Prerequisites

- An active **AWS account**
- Access to the **AWS Management Console** with permission to use S3, IAM and EC2
- Product images ready on your laptop (e.g. `mobile.jpg`, `laptop.jpg`)
- An **EC2 key pair** (`.pem` file) for SSH access
- An SSH client (Terminal, PuTTY, etc.)
- Your own public IP address (to restrict SSH access in the Security Group)
- Basic knowledge of Linux commands and HTML

---

## 4. Step 1: Create an S3 Bucket

1. Open **AWS Console → S3 → Create bucket**.
2. Enter a globally unique bucket name, for example:
   ```
   shopping-product-images-2026-12345
   ```
3. Select your AWS Region, for example `ap-south-1`.
4. Keep **Block all public access** **enabled**.
5. Click **Create bucket**.

---

## 5. Step 2: Upload Product Images

1. Open the bucket you just created.
2. Keep **Block all public access** enabled (the images stay private).
3. Click **Upload → Add files** and select your product images, such as `mobile.jpg` and `laptop.jpg`.
4. Click **Upload**.

---

## 6. Step 3: Create an IAM Role with S3 Read-Only Access

Create an IAM role so that EC2 can read from the bucket securely.

1. Open **AWS Console → IAM → Roles → Create role**.
2. **Trusted entity type:** AWS service → **Use case:** EC2.
3. Attach a read-only policy for the required S3 bucket:
   - Quick option: `AmazonS3ReadOnlyAccess`
   - Recommended (least privilege): create a custom policy limited to your bucket:
     ```json
     {
       "Version": "2012-10-17",
       "Statement": [
         {
           "Effect": "Allow",
           "Action": ["s3:GetObject", "s3:ListBucket"],
           "Resource": [
             "arn:aws:s3:::shopping-product-images-2026-12345",
             "arn:aws:s3:::shopping-product-images-2026-12345/*"
           ]
         }
       ]
     }
     ```
4. Give the role a name, for example `EC2-S3-ReadOnly-Role`.
5. Click **Create role**.

---

## 7. Step 4: Launch an Ubuntu EC2 Instance and Attach the IAM Role

1. Open **AWS Console → EC2 → Launch instance**.
2. Choose **Ubuntu** as the AMI and select an instance type (e.g. `t2.micro` / `t3.micro`).
3. Select your key pair.
4. Configure the **Security Group**:

   | Type | Port | Source |
   |------|------|--------|
   | HTTP | 80 | `0.0.0.0/0` (website visitors) |
   | SSH | 22 | **My IP** (restricted) |

5. Under **Advanced details → IAM instance profile**, select `EC2-S3-ReadOnly-Role`.
   *(For an already running instance: **Actions → Security → Modify IAM role** and attach the role.)*
6. Click **Launch instance**.

---

## 8. Step 5: Install Apache and AWS CLI

1. Connect to the EC2 instance using SSH:
   ```bash
   ssh -i your-key.pem ubuntu@EC2-PUBLIC-IP
   ```
2. Install Apache and AWS CLI:
   ```bash
   sudo apt update
   sudo apt install awscli apache2 -y
   ```
   > If `awscli` is not available as an apt package on your Ubuntu version, install AWS CLI v2 from the official AWS documentation.
3. Start and enable Apache:
   ```bash
   sudo systemctl enable --now apache2
   ```

---

## 9. Step 6: Download Product Images from S3 to EC2

1. List the buckets (this also confirms the IAM role is working):
   ```bash
   aws s3 ls
   ```
2. Download the images into the Apache web root:
   ```bash
   sudo aws s3 cp s3://YOUR-BUCKET-NAME/mobile.jpg /var/www/html/mobile.jpg
   sudo aws s3 cp s3://YOUR-BUCKET-NAME/laptop.jpg /var/www/html/laptop.jpg
   ```
   **OR** download everything in the bucket at once:
   ```bash
   sudo aws s3 cp s3://YOUR-BUCKET-NAME/ /var/www/html/ --recursive
   ```
3. Confirm the files are present:
   ```bash
   ls -l /var/www/html/
   ```

---

## 10. Step 7: Create the Shopping Website (index.html)

1. Open the file:
   ```bash
   sudo vi /var/www/html/index.html
   ```
2. Add the shopping website HTML (the image names must match the files you downloaded):
   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Shopping Store</title>
   </head>
   <body>
       <h1>Welcome to My Shopping Store</h1>

       <h2>Mobile Phone</h2>
       <img src="mobile.jpg" alt="Mobile Phone" width="200">
       <p>Price: ₹15,000</p>

       <h2>Laptop</h2>
       <img src="laptop.jpg" alt="Laptop" width="200">
       <p>Price: ₹45,000</p>
   </body>
   </html>
   ```
3. Save the file and restart Apache:
   ```bash
   sudo systemctl restart apache2
   ```

> **Note:** If you use different image file names, update the `src` values accordingly. File names containing spaces also work, but simple names like `mobile.jpg` are easier to manage.

---

## 11. Step 8: Verify the Website

1. Copy the **EC2 public IP address** from the EC2 console.
2. Open the following in a browser:
   ```
   http://EC2-PUBLIC-IP
   ```
3. Verify that:
   - The page **My Shopping Store** loads.
   - Both product images (mobile and laptop) display correctly along with their prices.

---

## 12. Troubleshooting

| Problem | Possible Cause | Fix |
|---------|---------------|-----|
| Website not opening in browser | Security Group does not allow port 80, or Apache is not running | Add an HTTP (80) inbound rule; run `sudo systemctl status apache2` and start it if needed |
| `Unable to locate credentials` when running `aws s3 ls` | IAM role not attached to the EC2 instance | Attach the role: EC2 → Actions → Security → Modify IAM role |
| `AccessDenied` / `403` on `aws s3 cp` | IAM policy does not cover the bucket, or the bucket name is wrong | Check the policy's bucket ARN and the bucket name in your command |
| `NoSuchBucket` / `404` error | Typo in bucket name or wrong region | Run `aws s3 ls` and copy the exact bucket name |
| Broken image icon on the page | Image name in `index.html` does not match the file in `/var/www/html/` | Check with `ls /var/www/html/` and correct the `src` value (names are case-sensitive) |
| Images exist but are not displayed | File permissions or the file was not copied | Verify with `ls -l /var/www/html/`; re-run `aws s3 cp` with `sudo` |
| SSH connection timed out | Your IP changed or port 22 is not open to your IP | Update the SSH rule in the Security Group to your current IP |
| Old page still showing | Browser cache or Apache not restarted | Hard refresh (Ctrl+F5) and run `sudo systemctl restart apache2` |

---

## 13. Key Learning Outcomes

- Understood why product images should be moved off the EC2 server to **Amazon S3** (scalability, durability, easier management).
- Learned how to create and secure an **S3 bucket** with **Block all public access** enabled.
- Learned how to use an **IAM role** with least-privilege, read-only access instead of storing access keys on EC2.
- Learned how to launch an **Ubuntu EC2 instance**, attach an IAM role, and configure a **Security Group** (HTTP 80 and restricted SSH 22).
- Gained hands-on experience installing and managing **Apache** and **AWS CLI** on Linux.
- Practised copying data between S3 and EC2 using `aws s3 ls` and `aws s3 cp`.
- Learned how to host a simple static shopping page and troubleshoot common access and URL issues.
- Understood the separation of compute (EC2) and storage (S3), which makes multi-server high availability easier.
