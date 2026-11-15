# **Project 1 – AWS Web Hosting Using EC2, Nginx, S3 and IAM**

<img width="1536" height="1024" alt="AWS Web Hosting Architecture Infographic" src="https://github.com/user-attachments/assets/682f3384-57d1-4576-a9bb-861b3e337402" />


## **1. Project overview**

[🌐 Secure NGINX Web Server on AWS with Let’s Encrypt | by Ashwini Singh | Medium](https://images.openai.com/static-rsc-4/tJ7H0_kkBfaGzfyMCLAW1mI8bi3_xmufffG7Q1C8vFijZN-Tsa1GON-7sQSRG_zOOdvbbokxKSujU7udcLWgnqRIQU9hf5ZrcM3EudluAsiLBg8CgeKvnlKAmz50_obXgB2JHVInZoVNST98-CH6be_1DH6wZyi8_hoG782aigc?purpose=inline)

[Understanding Amazon S3: Scalable Object Storage in AWS | by RITIKA GAURKHEDE | Medium](https://images.openai.com/static-rsc-4/bsqM97mHA-2LzRyPj7N1WE5LfUGoGHJNbO9xA8BmRwO597X1wmT83-QSrZC6RjO5WG6K4HOCUUEdLFMcus2S88NtG-l7FgRH2PV0uWTPh0-IWOgsTXaBWBWdmpgxulKWXbWkM2KmNyi9EvPgusVpZCcDum3f9DkBsB7qATNJZq0?purpose=inline)

[Deploying a Static Marketing/Portfolio Website on Ubuntu Using Nginx | by Wilfred oamen | Jan, 2026 | Medium](https://images.openai.com/static-rsc-4/5I28EYJ80Spwdlp0wdeZGNjQOFEhvQ8Jk78E5R62uwVB0WV-N_X8GEXatf62qMEDGWOzWPWxQW8DQT6PEs4QEo3tmhawea6eonnNQWpcDPrWN9YcLTmwtaSO-cJU7mQo_KBhuJlrDys89IWy7J9Z2Iy0XXhaE24eH1TnlgUiSR8?purpose=inline)

9

**Project name:** Secure Static Website Hosting on AWS Using EC2, Nginx, S3 and IAM

**Real-time scenario:**

Suppose an organization wants to host its company website on AWS.

Previously, the company hosted its website on an on-premises server. It faced several problems:

- Server maintenance and hardware costs.
- Difficulty increasing server capacity.
- Website downtime during server issues.
- Managing website images and other static files.
- Security risks from storing AWS credentials directly on servers.

The organization decides to migrate its website to AWS.

Our responsibility is to build a secure and scalable foundation for hosting the website.

## **2. Problem statement**

An organization wants to migrate its existing static website from an on-premises environment to AWS.

The organization requires:

1. A publicly accessible website.
2. An EC2 instance to host the website.
3. Nginx to serve website content.
4. An S3 bucket to store website images and static assets.
5. IAM permissions to allow EC2 to access S3 securely.
6. No hardcoded AWS access keys on the EC2 instance.
7. Secure access to AWS resources.

**Expected outcome:** Users should be able to access the website through the public IP address of the EC2 instance, while website assets are stored securely in S3.

## **3. Project architecture**

[Simple web site with hidden depths in AWS | by Brian Welch | Medium](https://images.openai.com/static-rsc-4/EIte1s0CoZPc4oyjGr-VNTyFG9rDxmrTBjGH6HMaWiLv7W0CZhrgrWEV6m-njbGr-3v42v5DDpVkWIcaTFi6VzSRSFOHDn0neXgG5BEyN_CEW5oyYe7E6vT7htBvI4m8ON2EUXIGxfJTmyOfxn0azGj8J2crKFYw1ZVv4HwqhrI?purpose=inline)

[medium.com](https://medium.com/%40btwelch/simple-web-site-with-hidden-depths-in-aws-3294b336175c?utm_source=chatgpt.com)

### **Architecture explanation**

| Component          | Responsibility                          |
| ------------------ | --------------------------------------- |
| Internet users     | Access the website                      |
| AWS Security Group | Controls inbound and outbound traffic   |
| EC2                | Hosts the website                       |
| Nginx              | Web server serving HTML/CSS             |
| S3                 | Stores website images and static assets |
| IAM Role           | Gives EC2 permission to access S3       |
| IAM Policy         | Defines permitted S3 operations         |

### **Request flow**

1. User opens the website using the EC2 public IP.
2. The request reaches the EC2 instance through port 80.
3. The Security Group permits HTTP traffic.
4. Nginx receives the request.
5. Nginx serves the website's HTML and CSS.
6. Website images and other static assets are stored in S3 and synchronized to the website directory by the EC2 instance.
7. EC2 uses its attached IAM role to access S3 without storing access keys.

## **4. Tools and AWS services**

[Amazon EC2 | Integrations | Opal Security](https://images.openai.com/static-rsc-4/HSk8YHPa6JA14sHlG7c1BIR-AlCKhBxVeJuwjDBuKFv0wCszN1hDGDjwq-Txab19tCqxYoocuiFOhFq8Yhd9R6oP21ruzP6QYOSMHqySIYkoYsG7EC9Pr3DNr6lmz8_MQY4secqbsHxSJ4GQEmd1TqjS70vkl5h_qgmZI58BL4I?purpose=inline)

**Amazon EC2**

Virtual machine to host the website.

[NGINX RTMP module - NGINX Extras Documentation](https://images.openai.com/static-rsc-4/VeJSLrCVL2QKRZkZ7frzcIbjgdgZoVn9LV-rfvRREGTFbaFJVgHgNJRhlTmVFmUl0k7JFiWPKT0CPqwnH2xWc1w_78wmeF3qK5ES6AUYlbycJrSPMbvcnZveVEYSTKLhXo7m-Fd9ZDqkt61EwO9lu9wVZd6Zzrk2wCSOZCuoyhQ?purpose=inline)

**Nginx**

Web server to serve website content.

[Amazon S3 Simple Storage Service Logo Vector Png | AWS S3 Bucket Icon  - freepng](https://images.openai.com/static-rsc-4/rB8GMmjRGUBIfO9GRNEL6l37e3jVW1hoDOCdtBff_Wr7VxkdCHtrta2g8EOf4zncP-U_xh6GGgSiEkpH5sASXFUOS_FyAJByqom1RHN_8AH3G2_0e-dOIH9z8H7GWykzTw3-woJ0v9yGGL6R4soSj66bGyOOPAMJOgN_sNVgnU0?purpose=inline)

**Amazon S3**

Object storage for website assets.

[AWS IAM (Identity and Access Management) :  PNG, AI, EPS, CDR, PDF, SVG Download - iconLogoVector](https://images.openai.com/static-rsc-4/KzQdQERgpQ_9mfyiZ2WtpQA7gWk6P7mtursaiDW5hIZEugYbH1Y6NJLz5yZWyr3x9oJtPhhuPTnZRdhhOw3aFV4zd-KjQcKvztz73QyvAYfuK6GZ570W3pjfwFhGoiyEHjU7__LBms2lJcaZ29-__ffhdznHMmR67aP_iEECDjs?purpose=inline)

**AWS IAM**

Secure access management using roles and policies.

[File:AWS Simple Icons Virtual Private Cloud.svg - Wikimedia Commons](https://images.openai.com/static-rsc-4/fA-FIO3BaQnjvT9q_CrRVNLqEdnVAJdLHnaEU_KJnBlAFerDii0p4BWXkVnPe3U8e9S-B3Twq4cz_ltqKSuTA4ropYTRADJYchEtsXgsn4nGT6hx_AzJLnBBjiWJYhSFG1t7kRo5aJ0mpYeThGjEskNKtYuFFXgDRC846nQDIdQ?purpose=inline)

**Amazon VPC and Security Groups**

Network isolation and traffic control.

[Linux Icon Sets at GetDrawings | Free download](https://images.openai.com/static-rsc-4/esdbOSBMXd1TlQY6DdAizYOjF_flvtdZba1CbXCldrh7P2lkK4alfMAcZ4yPg03CrZodrdMqYreKCh4bB-MscSBl3yxtc5tc3Nw_5rrF3akj1Y8mhSTviGR7sifpEkQvjHvEjEw5OcHwsPU7_yN-Mi4rFwjReotRJKsVATHTXsU?purpose=inline)

**Amazon Linux 2023**

Operating system for the EC2 instance.

**Additional tools:** AWS Management Console, SSH, Git and GitHub.

## **5. Step-by-step implementation**

We will use the following implementation approach:

**Implementation sequence**

1. Prepare AWS environment and region
2. Create an S3 bucket
3. Create IAM policy and IAM role
4. Launch EC2 instance
5. Attach IAM role to EC2
6. Install and configure Nginx
7. Upload website assets to S3
8. Connect EC2 to S3 using IAM
9. Deploy website and test access
10. Document everything on GitHub

### **Step 1. Prepare AWS environment**

Log in to the AWS Management Console:

[Open AWS Management Console](https://console.aws.amazon.com/?utm_source=chatgpt.com)

Choose your AWS region. For this project, use:

- Region: Mumbai
- Region code: `ap-south-1`
- Operating system: Amazon Linux 2023
- Instance type: `t3.micro` (check current Free Tier eligibility and pricing)

Create a project folder on your local machine:

```
mkdir aws-web-hosting-project
cd aws-web-hosting-project
```

### **Step 2. Create an S3 bucket**

Open AWS Console → S3 → Create bucket.

[Introducing VPC Flow Logs for AWS Transit Gateway | Networking & Content Delivery](https://images.openai.com/static-rsc-4/RRo5mfbDUT350IocOjxSC8JDQ99G8I83HQCzJzM0Bq0vg-ev21uX_buIUtSZGzWv4WIhvvAQu1TYL2G3TgY7-d_tnUtCtq_WmQVI-yBFqi36XGp6YmKtMa0W5PUBnVqca6Kx88RpvUQ2_OTQc6wCOYenOX7-ugPKLK2B3AlgNy0?purpose=inline)

[aws.amazon.com](https://aws.amazon.com/blogs/networking-and-content-delivery/introducing-vpc-flow-logs-for-aws-transit-gateway/?utm_source=chatgpt.com)

Use these settings:

| Setting             | Value                        |
| ------------------- | ---------------------------- |
| Bucket name         | aws-web-assets-yourname-2026 |
| Region              | ap-south-1                   |
| Object Ownership    | ACLs disabled                |
| Block Public Access | Enabled                      |
| Encryption          | SSE-S3                       |

Remember: S3 bucket names must be globally unique.

Click Create bucket.

Create the following folder structure in S3:

```
aws-web-assets-yourname-2026/
│
└── website/
    ├── images/
    └── css/
```

We will store website images and CSS files in this bucket.

**Security decision:** Keep the S3 bucket private. The EC2 instance will access the objects through its IAM role.

### **Step 3. Create IAM policy**

We need to allow EC2 to read objects from our S3 bucket.

Go to:

AWS Console → IAM → Policies → Create policy → JSON.

Use this policy, replacing the bucket name with your actual bucket name.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket"
      ],
      "Resource": "arn:aws:s3:::aws-web-assets-yourname-2026"
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::aws-web-assets-yourname-2026/website/*"
    }
  ]
}
```

Policy name:

```
EC2-S3-Website-ReadOnly-Policy
```

This policy allows:

- Listing the specified bucket.
- Reading website files from the specified prefix.
- No uploading or deleting objects from EC2.

### **Step 4. Create IAM role**

Navigate to:

IAM → Roles → Create role.

Configure:

| Setting        | Value                          |
| -------------- | ------------------------------ |
| Trusted entity | AWS service                    |
| Service        | EC2                            |
| Permissions    | EC2-S3-Website-ReadOnly-Policy |
| Role name      | EC2-S3-Website-Role            |

Click Create role.

[Securely connect to Amazon RDS for PostgreSQL with AWS Session Manager and IAM authentication | AWS Database Blog](https://images.openai.com/static-rsc-4/7luku04tomMvmCvQoNuyB6bEQ1LfCIhi1UvWZY6RdQol15Ye5d1OcmzjQLvtcy9HScokpcURrsXSFGyMusOOM-PrLfHeakj3AKVUEEjYIyI8Cc4-KFJjY_qN2Em_jBBd7udSQCVz9eZJIi0sfeuY-uev1oxt2jDX3mxVTmCLlWY?purpose=inline)

[aws.amazon.com](https://aws.amazon.com/blogs/database/securely-connect-to-amazon-rds-for-postgresql-with-aws-session-manager-and-iam-authentication/?utm_source=chatgpt.com)

**Important concept for students:**

An IAM policy defines permissions. An IAM role provides temporary credentials to an authorized AWS service or identity. An EC2 instance can obtain those credentials through its instance profile.

We do not need to create AWS access keys for this project.

### **Step 5. Launch EC2 instance**

Navigate to:

AWS Console → EC2 → Instances → Launch instances.

[Beginners guide to AWS EC2 - DEV Community](https://images.openai.com/static-rsc-4/9GkYLlbWMaEbdt_2XkWp4me0Ko6VmVk_jMuYohTz1zGC4blb0-EVDAh1Ke_FIMHh01VoqbMD0jvn5Fni3JC9GvjEHkJacABTAqXblegKxFmr40ovAxG2iLfhxvqx4zcMBtxWubolcNPijLOetjFUyOWxM5jGnlvxPba64cjuZuI?purpose=inline)

[dev.to](https://dev.to/vivekalhat/beginners-guide-to-aws-ec2-2adk?utm_source=chatgpt.com)

Configure:

| Configuration         | Value                     |
| --------------------- | ------------------------- |
| Name                  | AWS-Web-Hosting-Server    |
| AMI                   | Amazon Linux 2023         |
| Instance type         | t3.micro                  |
| Key pair              | Create or select key pair |
| VPC                   | Default VPC for lab       |
| Auto-assign public IP | Enabled                   |
| Storage               | 8 GiB gp3                 |

Create a Security Group:

| Type | Port | Source     |
| ---- | ---- | ---------- |
| SSH  | 22   | My IP only |
| HTTP | 80   | 0.0.0.0/0  |

Do not expose SSH to everyone.

Launch the instance.

### **Step 6. Attach IAM role to EC2**

After EC2 is running:

1. Select your EC2 instance.
2. Click Actions.
3. Select Security.
4. Select Modify IAM role.
5. Choose `EC2-S3-Website-Role`.
6. Click Update IAM role.

[AWS Builder Center](https://images.openai.com/static-rsc-4/iJi4TQJLviYZQzEpquXYdf9PQ-BJv5Tx_VdxlxhkirucKSc-FkZdQv53OxPOesZZgP_xXK2DwKGnZnPcO6Tv1naTkg6ChMocB4Zvjx_3OB7j81QFKYXgcCHO4AvRysxkoEg2SM5HZaX_uzBUOWLdq_ibnGxo3Y-YqrMK7vQOxhM?purpose=inline)

[builder.aws.com](https://builder.aws.com/content/2iCmBIvLS5GaQFui5o8BMHDSSpJ/securely-access-resources-with-iam-service-roles?utm_source=chatgpt.com)

Now EC2 can securely access S3 using its IAM role.

### **Step 7. Connect to EC2 and install Nginx**

Select your EC2 instance and click Connect → EC2 Instance Connect.

Run:

```
sudo dnf update -y
```

Install Nginx:

```
sudo dnf install nginx -y
```

Start Nginx:

```
sudo systemctl start nginx
```

Enable Nginx at system startup:

```
sudo systemctl enable nginx
```

Check service status:

```
sudo systemctl status nginx
```

Expected result:

```
Active: active (running)
```

Get your EC2 public IP from the EC2 console.

Open this URL in your browser:

```
http://YOUR_EC2_PUBLIC_IP
```

[Exploring Microsoft Radius Application Platform - The New Stack](https://images.openai.com/static-rsc-4/TVh8NxOjrWasvQG3Ae95i_dL5bEu1nzCiftb6WYyr_LjVr4xiLzAtNVMkOMzC6ltoVuIbgWdRjISZ7WqIkfxo7zjjKHoeRP3LtK6wQOdnmlLpvhqERsg61q_SmMtQ8oMgSVNPldOcUffitxZS8h-BHqaUXWQmQKL24qPYpJdOz0?purpose=inline)

[thenewstack.io](https://thenewstack.io/exploring-microsoft-radius-application-platform/?utm_source=chatgpt.com)

You should see the Nginx welcome page.

### **Step 8. Create website files**

On your EC2 instance:

```
sudo mkdir -p /var/www/html/assets/images
sudo mkdir -p /var/www/html/assets/css
```

Create the website:

```
sudo nano /var/www/html/index.html
```

Add the following HTML:

```
<!DOCTYPE html>
<html>
<head>
    <title>AWS Web Hosting Project</title>

    <link rel="stylesheet"
          href="/assets/css/style.css">
</head>

<body>

    <header>
        <h1>Welcome to AWS Web Hosting</h1>
        <p>Hosted using Amazon EC2 and Nginx</p>
    </header>

    <main>
        <h2>Our AWS Cloud Project</h2>

        <p>
          This website is hosted on an EC2 instance.
          Static assets are stored in Amazon S3.
        </p>

        <img src="/assets/images/aws-cloud.jpg"
             alt="AWS Cloud"
             width="400">

    </main>

    <footer>
        <p>Project: AWS Web Hosting</p>
    </footer>

</body>
</html>
```

Create the CSS file:

```
sudo nano /var/www/html/assets/css/style.css
```

Add:

```
body {
    font-family: Arial, sans-serif;
    text-align: center;
    background: #f2f5f9;
    margin: 0;
}

header {
    background: #232f3e;
    color: white;
    padding: 30px;
}

main {
    padding: 40px;
}

img {
    border-radius: 10px;
}

footer {
    background: #232f3e;
    color: white;
    padding: 15px;
}
```

### **Step 9. Upload website assets to S3**

From your local machine, upload an image and CSS file to the S3 bucket.

For example:

```
aws s3 cp aws-cloud.jpg \
s3://aws-web-assets-yourname-2026/website/images/aws-cloud.jpg
```

```
aws s3 cp style.css \
s3://aws-web-assets-yourname-2026/website/css/style.css
```

You can also upload files using S3 Console → Bucket → Upload.

### **Step 10. Configure EC2 to access S3**

Return to the EC2 terminal.

Check whether AWS CLI is available:

```
aws --version
```

If not installed, install AWS CLI v2 using the official AWS installation instructions.

Check the EC2 IAM role:

```
aws sts get-caller-identity
```

This should return the assumed role identity.

Now download the S3 assets:

```
aws s3 cp \
s3://aws-web-assets-yourname-2026/website/images/aws-cloud.jpg \
/var/www/html/assets/images/aws-cloud.jpg
```

Download CSS:

```
aws s3 cp \
s3://aws-web-assets-yourname-2026/website/css/style.css \
/var/www/html/assets/css/style.css
```

Alternatively, synchronize the entire asset directory:

```
aws s3 sync \
s3://aws-web-assets-yourname-2026/website/ \
/var/www/html/assets/
```

Fix ownership and permissions if required:

```
sudo chown -R nginx:nginx /var/www/html
sudo chmod -R 755 /var/www/html
```

### **Step 11. Test website**

Open your browser:

```
http://YOUR_EC2_PUBLIC_IP
```

Expected result

[DevOps & Cloud Infrastructure by JK Mahbub on Dribbble](https://images.openai.com/static-rsc-4/d--3W_1rkQ-Hyvrhft22c1sJRlgQeqcqAbymoYFzxSP8_KRw39gf6x1nTlS2y9oJq76Z3EXblvyXGVsy0LMhPuqoC4-41wmSqWFRBjrr6Vcy-DSkfu5ucucp-hs3E7vx0lA7NeqPIUl2909n1uZd9boVy09NJ-M4tJ3f1h-ZuxI?purpose=inline)

[dribbble.com](https://dribbble.com/shots/27071063-DevOps-Cloud-Infrastructure?utm_source=chatgpt.com)

Verify:

- Website opens successfully.
- HTML content is displayed.
- CSS styling works.
- Image is displayed.
- Nginx service is running.
- EC2 can access S3.
- No AWS access keys are stored on EC2.

## **6. Final architecture diagram for GitHub**

Save this as `architecture.mmd` or include it in your README using a Mermaid code block. GitHub supports Mermaid rendering.

\#chatgpt-mermaid-\_r_hl\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_hl\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_hl\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_hl\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_hl\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_hl\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_hl\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_hl\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_hl\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_hl\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_hl\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_hl\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_hl\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_hl\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_hl\_ p{margin:0;}#chatgpt-mermaid-\_r_hl\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_hl\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_hl\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_hl\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_hl\_ .label text,#chatgpt-mermaid-\_r_hl\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_hl\_ .node rect,#chatgpt-mermaid-\_r_hl\_ .node circle,#chatgpt-mermaid-\_r_hl\_ .node ellipse,#chatgpt-mermaid-\_r_hl\_ .node polygon,#chatgpt-mermaid-\_r_hl\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_hl\_ .rough-node .label text,#chatgpt-mermaid-\_r_hl\_ .node .label text,#chatgpt-mermaid-\_r_hl\_ .image-shape .label,#chatgpt-mermaid-\_r_hl\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_hl\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_hl\_ .rough-node .label,#chatgpt-mermaid-\_r_hl\_ .node .label,#chatgpt-mermaid-\_r_hl\_ .image-shape .label,#chatgpt-mermaid-\_r_hl\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_hl\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_hl\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_hl\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_hl\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_hl\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_hl\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_hl\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_hl\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_hl\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_hl\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_hl\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_hl\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_hl\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_hl\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_hl\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_hl\_ .icon-shape,#chatgpt-mermaid-\_r_hl\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_hl\_ .icon-shape p,#chatgpt-mermaid-\_r_hl\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_hl\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_hl\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_hl\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_hl\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_hl\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_hl\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_hl\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_hl\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_hl\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_hl\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_hl\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_hl\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_hl\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_hl\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_hl\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_hl\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_hl\_ .node rect,#chatgpt-mermaid-\_r_hl\_ .node circle,#chatgpt-mermaid-\_r_hl\_ .node ellipse,#chatgpt-mermaid-\_r_hl\_ .node polygon,#chatgpt-mermaid-\_r_hl\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_hl\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_hl\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_hl\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_hl\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_hl\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Internet UsersEC2 Public IPSecurity GroupEC2 InstanceNginx Web ServerWebsite HTML and CSSS3 Private BucketIAM RoleIAM Read-Only PolicyHTTP Port 80Temporary credentialss3:GetObjectWebsite assets

## **7. Troubleshooting guide**

| Problem               | Possible reason                   | Solution                         |
| --------------------- | --------------------------------- | -------------------------------- |
| Website not opening   | Port 80 blocked                   | Check Security Group             |
| SSH connection failed | Port 22 restricted incorrectly    | Verify your public IP            |
| Nginx not running     | Service stopped                   | `sudo systemctl start nginx`     |
| AccessDenied from S3  | IAM permissions missing           | Check role and policy            |
| AWS credentials error | Role not attached                 | Attach EC2 IAM role              |
| Image not displaying  | Incorrect path                    | Check HTML and S3 object key     |
| CSS not loading       | File missing or permissions issue | Check asset path and permissions |

Useful commands:

```
sudo systemctl status nginx
```

```
sudo journalctl -u nginx -n 50
```

```
aws sts get-caller-identity
```

```
aws s3 ls s3://aws-web-assets-yourname-2026/website/
```

```
curl -I http://localhost
```

## **8. GitHub repository structure**

Create a public GitHub repository:

**Repository name:** `aws-web-hosting-ec2-s3-iam`

Recommended folder structure:

```
aws-web-hosting-ec2-s3-iam/
│
├── README.md
│
├── architecture/
│   └── architecture.mmd
│
├── website/
│   ├── index.html
│   └── assets/
│       ├── css/
│       │   └── style.css
│       └── images/
│           └── aws-cloud.jpg
│
├── iam/
│   └── ec2-s3-readonly-policy.json
│
├── screenshots/
│   ├── ec2-instance.png
│   ├── s3-bucket.png
│   ├── iam-role.png
│   ├── nginx-running.png
│   └── website-output.png
│
└── docs/
    ├── implementation.md
    ├── troubleshooting.md
    └── cleanup.md
```

### **GitHub documentation**

Your `README.md` should explain the complete project, not just contain commands.

The following is a GitHub-ready README template.

# AWS Web Hosting Using EC2, Nginx, S3 and IAM

## 1. Project Overview

This project demonstrates how to host a static website on AWS using Amazon EC2, Nginx, Amazon S3 and IAM.

The website is hosted on an EC2 instance, while static assets such as images and CSS files are stored in a private S3 bucket. An IAM role attached to EC2 provides secure access to S3 without storing AWS access keys on the server.

## 2. Problem Statement

An organization wants to migrate its website from an on-premises server to AWS.

The organization needs:

- Public website access.
- Reliable website hosting using EC2.
- Nginx web server configuration.
- Centralized storage of static assets using S3.
- Secure EC2-to-S3 communication using IAM roles.
- No hardcoded AWS credentials.

**Solution:** Deploy a website on EC2 with Nginx, store static assets in a private S3 bucket, and use an IAM instance role to retrieve the assets.

## 3. Architecture

```
flowchart TD
    A[Internet Users]
    B[EC2 Public IP]
    C[Security Group]
    D[EC2 Instance]
    E[Nginx]
    F[Website HTML and CSS]
    G[Private S3 Bucket]
    H[IAM Role]
    I[IAM Policy]

    A -->|HTTP 80| B
    B --> C
    C --> D
    D --> E
    E --> F
    D -->|Temporary credentials| H
    H --> I
    I -->|Read objects| G
    G -->|Website assets| D
```

## 4. AWS Services and Tools

| Service / Tool    | Purpose                          |
| ----------------- | -------------------------------- |
| Amazon EC2        | Website hosting                  |
| Amazon S3         | Static asset storage             |
| AWS IAM           | Identity and access management   |
| IAM Role          | Secure EC2 access to S3          |
| IAM Policy        | Define S3 read permissions       |
| Nginx             | Web server                       |
| Amazon Linux 2023 | Operating system                 |
| Security Group    | Network traffic control          |
| AWS CLI           | AWS command-line operations      |
| Git and GitHub    | Source control and documentation |

## 5. Prerequisites

- AWS account.
- Basic Linux knowledge.
- Basic HTML and CSS knowledge.
- Basic AWS EC2, S3 and IAM knowledge.
- SSH client or EC2 Instance Connect.
- GitHub account.

## 6. Implementation Steps

### Step 1: Create an S3 bucket

Create a bucket with a globally unique name.

Example:

`aws-web-assets-yourname-2026`

Region: `ap-south-1`

Keep Block Public Access enabled and enable default encryption.

Create the following folders:

```
website/
├── images/
└── css/
```

### Step 2: Create IAM policy

Create a policy named:

`EC2-S3-Website-ReadOnly-Policy`

Policy JSON:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket"],
      "Resource": "arn:aws:s3:::aws-web-assets-yourname-2026"
    },
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": "arn:aws:s3:::aws-web-assets-yourname-2026/website/*"
    }
  ]
}
```

Replace the example bucket name with your actual bucket name.

### Step 3: Create IAM role

Create an IAM role:

- Trusted entity: AWS service.
- Use case: EC2.
- Attach policy: EC2-S3-Website-ReadOnly-Policy.
- Role name: EC2-S3-Website-Role.

### Step 4: Launch EC2 instance

Configuration:

| Parameter     | Value                  |
| ------------- | ---------------------- |
| Name          | AWS-Web-Hosting-Server |
| AMI           | Amazon Linux 2023      |
| Instance type | t3.micro               |
| Region        | ap-south-1             |
| Storage       | 8 GiB gp3              |
| Public IP     | Enabled                |

Security Group:

| Type | Port | Source    |
| ---- | ---- | --------- |
| SSH  | 22   | My IP     |
| HTTP | 80   | 0.0.0.0/0 |

### Step 5: Attach IAM role

Select EC2 instance.

Actions → Security → Modify IAM role.

Attach:

`EC2-S3-Website-Role`

### Step 6: Install Nginx

Connect to EC2 and execute:

```
sudo dnf update -y
sudo dnf install nginx -y

sudo systemctl start nginx
sudo systemctl enable nginx

sudo systemctl status nginx
```

### Step 7: Create website

Create directories:

```
sudo mkdir -p /var/www/html/assets/images
sudo mkdir -p /var/www/html/assets/css
```

Create `index.html` and `style.css` using the examples in the website directory.

### Step 8: Upload assets to S3

From your local machine:

```
aws s3 cp aws-cloud.jpg \
s3://aws-web-assets-yourname-2026/website/images/aws-cloud.jpg
```

```
aws s3 cp style.css \
s3://aws-web-assets-yourname-2026/website/css/style.css
```

### Step 9: Verify IAM access from EC2

Check AWS CLI:

```
aws --version
```

Check the assumed identity:

```
aws sts get-caller-identity
```

Check S3 access:

```
aws s3 ls s3://aws-web-assets-yourname-2026/website/
```

### Step 10: Download S3 assets

Execute on EC2:

```
aws s3 sync \
s3://aws-web-assets-yourname-2026/website/ \
/var/www/html/assets/
```

Set permissions:

```
sudo chown -R nginx:nginx /var/www/html
sudo chmod -R 755 /var/www/html
```

### Step 11: Test website

Open:

`http://YOUR_EC2_PUBLIC_IP`

Verify:

- Website loads successfully.
- Nginx is running.
- CSS styling is visible.
- Images are displayed.
- EC2 can read S3 objects.
- IAM role works without hardcoded access keys.

## 7. Important Linux Commands

```
sudo systemctl status nginx
sudo systemctl restart nginx
sudo systemctl enable nginx
sudo journalctl -u nginx -n 50
curl -I http://localhost
```

## 8. Security Implementation

- Keep the S3 bucket private.
- Enable S3 Block Public Access.
- Enable S3 default encryption.
- Use IAM roles instead of hardcoded credentials.
- Follow least-privilege IAM permissions.
- Restrict SSH to your IP address.
- Allow HTTP only where required.
- Never upload private keys, passwords or AWS credentials to GitHub.

## 9. Testing and Validation

| Test                         | Expected Result  |
| ---------------------------- | ---------------- |
| Access EC2 public IP         | Website opens    |
| Check Nginx service          | Active (running) |
| Check IAM identity           | Assumed EC2 role |
| List S3 website prefix       | Objects visible  |
| Download S3 assets           | Successful       |
| Access S3 without permission | AccessDenied     |
| Website image display        | Image loads      |
| Website CSS                  | Styling works    |

## 10. Troubleshooting

| Issue                   | Resolution                          |
| ----------------------- | ----------------------------------- |
| Website not accessible  | Check Security Group port 80        |
| SSH connection failure  | Check port 22 and key pair          |
| Nginx not running       | Start Nginx service                 |
| S3 AccessDenied         | Verify IAM role and policy          |
| Credentials unavailable | Verify EC2 role attachment          |
| Image not visible       | Check object key and file path      |
| CSS not loading         | Check file location and permissions |

## 11. Cleanup

To avoid unnecessary AWS charges:

1. Stop or terminate the EC2 instance.
2. Delete the S3 objects.
3. Delete the S3 bucket.
4. Delete the IAM role.
5. Delete the IAM policy if it is no longer required.
6. Delete unused key pairs and security groups where appropriate.

Remember that stopping EC2 does not eliminate all possible charges, such as EBS storage or allocated public IPv4 charges. Check your billing dashboard.

## 12. Learning Outcomes

After completing this project, you will understand:

- How to launch and configure an EC2 instance.
- How to install and configure Nginx.
- How to create and manage S3 buckets.
- How to create IAM roles and policies.
- How EC2 accesses S3 using temporary credentials.
- How to deploy a static website.
- How to troubleshoot website hosting issues.
- How to document cloud projects on GitHub.

## 13. Future Enhancements

- Configure HTTPS using an SSL certificate.
- Use Route 53 for domain mapping.
- Add an Application Load Balancer.
- Configure Auto Scaling.
- Use CloudWatch for monitoring.
- Automate deployment using a CI/CD pipeline.
- Provision infrastructure using Terraform.

## 14. Project Author

**Project:** AWS Web Hosting Using EC2, Nginx, S3 and IAM

**Category:** AWS Cloud / DevOps

**Level:** Beginner to Intermediate

**Status:** Hands-on implementation project

**Repository:** Add your GitHub repository URL here.

## **9. Project completion checklist**

Use this checklist while implementing the project:

**Implementation progress**

0/14 completed

S3 bucket created and kept private

IAM policy created

IAM role created for EC2

EC2 instance launched

Security Group configured

IAM role attached to EC2

Nginx installed and running

Website HTML and CSS created

Website assets uploaded to S3

EC2 successfully accessed S3

Website successfully opened in browser

Screenshots added to GitHub

README.md completed

AWS resources cleaned up

## **10. My recommendation: Implement it as a real-time project**

For a good portfolio project, don't stop after seeing the Nginx welcome page.

Complete these three demonstrations:

1. **Website hosting:** Show the website running through the EC2 public IP.
2. **IAM security:** Show that EC2 can retrieve S3 objects without storing AWS credentials.
3. **S3 integration:** Upload a new image to S3, synchronize it to EC2, and show it on the website.

One important distinction: in this architecture, S3 stores the assets and EC2 synchronizes them locally. Nginx serves the local copies. This keeps the bucket private and makes the architecture easy to understand.

**Next step:** Start with Step 1 and implement the project in AWS. I can guide you through each step, including AWS Console configuration, Linux commands, troubleshooting and GitHub documentation.

☁️Continue AWS project tomorrowTap to set up
