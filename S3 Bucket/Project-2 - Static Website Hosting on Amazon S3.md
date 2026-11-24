# Project-2 - Static Website Hosting on Amazon S3

## Problem Statement

A tourism company wants to publish a simple website (HTML, CSS, JavaScript and images) on the internet.

Hosting it on an EC2 instance would mean:

- Launching and paying for a server that runs 24/7.
- Installing, securing and patching a web server such as Apache or Nginx.
- Managing scaling and availability by hand.

For a website made only of static files, this is unnecessary effort and cost. The company needs a **simple, low-cost, serverless way** to host static content without managing any web server.

## Project Name

**Static Website Hosting using Amazon S3 (Tourism Website Demo)**

## Project Flow

```
Create S3 bucket → Allow public access → Upload website files → Add bucket policy → Enable static website hosting → Open website endpoint
```

1. Create an S3 bucket with a unique name.
2. Turn off *Block all public access* (for a basic public demo).
3. Upload `index.html` and the other website files (CSS, JS, images).
4. Add a bucket policy that allows public read access to the objects.
5. Enable **Static website hosting** and set `index.html` as the index document.
6. Open the **bucket website endpoint** in a browser to verify the site.

> No EC2 web server is needed. Use **CloudFront** in front of S3 for production.

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Architecture](#2-architecture)
3. [Prerequisites](#3-prerequisites)
4. [Step 1: Create an S3 Bucket](#4-step-1-create-an-s3-bucket)
5. [Step 2: Disable Block Public Access](#5-step-2-disable-block-public-access)
6. [Step 3: Upload Website Files](#6-step-3-upload-website-files)
7. [Step 4: Add the Bucket Policy](#7-step-4-add-the-bucket-policy)
8. [Step 5: Enable Static Website Hosting](#8-step-5-enable-static-website-hosting)
9. [Step 6: Open the Website Endpoint and Verify](#9-step-6-open-the-website-endpoint-and-verify)
10. [Step 7: Use CloudFront for Production (Recommended)](#10-step-7-use-cloudfront-for-production-recommended)
11. [Step 8: Clean Up (Optional)](#11-step-8-clean-up-optional)
12. [Troubleshooting](#12-troubleshooting)
13. [Key Learning Outcomes](#13-key-learning-outcomes)

---

## 1. Project Overview

Amazon S3 can host a **static website**, which is a site made of files that do not need server-side processing:

- HTML pages
- CSS stylesheets
- JavaScript files
- Images

You upload the files to a bucket, enable static website hosting, and S3 serves them directly over HTTP at a **bucket website endpoint**.

**Benefits**

- No EC2 instance or web server to install and maintain.
- Low cost, pay only for storage and requests.
- Highly durable and scalable by design.
- Quick to set up, suitable for portfolios, landing pages and tourism or brochure sites.

**Note:** The basic setup in this project makes the bucket publicly readable and serves content over HTTP only. For production, put **CloudFront** in front of S3.

---

## 2. Architecture

![Architecture Diagram](images/architecture.png)

| Component | Purpose |
|-----------|---------|
| Amazon S3 bucket | Stores `index.html`, CSS, JS and images |
| Bucket policy | Allows public read (`s3:GetObject`) on the website files |
| Static website hosting | Serves `index.html` as the home page at the bucket website endpoint |
| CloudFront (optional) | CDN in front of S3 for production (HTTPS, caching, better performance) |

---

## 3. Prerequisites

- An active **AWS account**
- Access to the **AWS Management Console** with permission to use Amazon S3
- Website files ready on your computer: `index.html` plus any CSS, JavaScript and image files
- A globally unique bucket name, for example `my-tourism-website-2026`
- Basic knowledge of HTML

---

## 4. Step 1: Create an S3 Bucket

1. Log in to the **AWS Management Console**.
2. Open **Amazon S3**.
3. Click **Create bucket**.
4. Enter a unique bucket name, for example:
   ```
   my-tourism-website-2026
   ```
5. Select your **AWS Region**, such as `us-east-1`.

---

## 5. Step 2: Disable Block Public Access

For a basic public static website demo:

1. In the **Block Public Access settings for this bucket** section, **uncheck** *Block all public access*.
2. Tick the checkbox to **acknowledge the warning**.
3. Click **Create bucket**.

> **Security note:** This makes it possible for the bucket to be public. Only do this for buckets that contain files you want everyone to see, and never store private data in this bucket.

---

## 6. Step 3: Upload Website Files

1. Open the bucket you just created.
2. Click **Upload**.
3. Click **Add files** and select your `index.html` file.
4. Upload any additional HTML, CSS, JavaScript and image files your website requires.
5. Click **Upload** to finish.

---

## 7. Step 4: Add the Bucket Policy

1. In the bucket, go to **Permissions → Bucket policy**.
2. Click **Edit** and add the following policy. Replace `my-tourism-website-2026` with **your actual bucket name**:

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "PublicReadWebsiteFiles",
               "Effect": "Allow",
               "Principal": "*",
               "Action": "s3:GetObject",
               "Resource": "arn:aws:s3:::my-tourism-website-2026/*"
           }
       ]
   }
   ```

3. Click **Save changes**.

---

## 8. Step 5: Enable Static Website Hosting

1. Open the **Properties** tab of the bucket.
2. Scroll down to **Static website hosting** and click **Edit**.
3. Select **Enable**.
4. Choose **Host a static website**.
5. Enter `index.html` as the **Index document**.
6. Click **Save changes**.

---

## 9. Step 6: Open the Website Endpoint and Verify

1. Go back to **Properties → Static website hosting**.
2. Copy the **Bucket website endpoint**. It looks like this:
   ```
   http://my-tourism-website-2026.s3-website-us-east-1.amazonaws.com
   ```
3. Open the endpoint in your browser.
4. Verify that your website loads, including its CSS, JavaScript and images.

---

## 10. Step 7: Use CloudFront for Production (Recommended)

The S3 website endpoint is fine for a demo, but for a production website:

1. Create an **Amazon CloudFront** distribution with the S3 bucket as the origin.
2. Use CloudFront to get **HTTPS**, caching and lower latency for visitors worldwide.
3. Optionally restrict direct bucket access so that content is served only through CloudFront (Origin Access Control).

---

## 11. Step 8: Clean Up (Optional)

To avoid unnecessary charges after the demo:

1. Open the bucket and select all objects, then click **Delete**.
2. Go back to the bucket list, select the bucket, and click **Delete**.
3. If you created a CloudFront distribution, disable and delete it as well.

---

## 12. Troubleshooting

| Problem | Possible Cause | Fix |
|---------|---------------|-----|
| `403 Forbidden` when opening the endpoint | Bucket policy missing or incorrect, or Block Public Access still on | Re-check the bucket policy and the bucket name in the ARN; make sure *Block all public access* is off |
| Bucket policy fails to save | Block Public Access is still enabled | Go to **Permissions → Block public access**, edit and turn it off, then save the policy again |
| `404 Not Found` / `NoSuchKey` | `index.html` not uploaded, or the file name does not match the Index document setting | Confirm the file is in the bucket root and is named exactly `index.html` (names are case-sensitive) |
| Page loads but CSS, JS or images are missing | Files not uploaded, or wrong paths in the HTML | Upload all required files and check the folder structure and paths in `index.html` |
| Browser downloads the file instead of showing the page | Used the object URL instead of the website endpoint | Use the **Bucket website endpoint** from Properties → Static website hosting |
| Site shows "Not secure" / no HTTPS | S3 website endpoints support HTTP only | Put CloudFront in front of the bucket for HTTPS |
| Changes not visible after re-upload | Browser cache (or CloudFront cache) | Hard refresh with Ctrl+F5; if using CloudFront, create an invalidation |
| Bucket name already taken | Bucket names are globally unique | Choose a different name, for example add a number or your name |

---

## 13. Key Learning Outcomes

- Understood how to host a **static website on Amazon S3** without any EC2 web server.
- Learned how to create an S3 bucket and manage **Block Public Access** settings.
- Learned how to write and apply a **bucket policy** to allow public read access.
- Learned how to enable **Static website hosting** and set the index document.
- Understood the difference between the **object URL** and the **bucket website endpoint**.
- Learned why **CloudFront** is recommended for production (HTTPS, caching, performance, security).
- Gained awareness of the security implications of public buckets.
