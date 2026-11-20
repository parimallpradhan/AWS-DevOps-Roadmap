## **What is Amazon S3?**

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


[AWS Storage - Part 4: Amazon S3 - DEV Community](https://images.openai.com/static-rsc-4/XIOlpDCwljoY5lCMoQ8a42_xcTAMXon5jIpMFriNyuGMND7fNvAANVu3UN2-o9k59LsJQfWYHS43PdHYKg8xYYA4oKXn2SZunaEOpr6bcQq4bYAljdivtqI23aTPVBDJZE4o-iDP6TiO6BtjPeMlemcurRIYEUcMbLDBviuST7k?purpose=inline)

[dev.to](https://dev.to/hulk-pham/aws-storage-part-4-amazon-s3-1kki?utm_source=chatgpt.com)

**Important S3 terminology**

| Component  | Meaning                                | Example             |
| ---------- | -------------------------------------- | ------------------- |
| Bucket     | Container to store objects             | ecommerce-images    |
| Object     | Actual file                            | mobile.jpg          |
| Key        | Unique object identifier within bucket | products/mobile.jpg |
| Region     | AWS geographical location              | ap-south-1          |
| Version ID | Identifies a particular version        | Version 123abc      |

# **2. S3 Versioning**

## **What is S3 Versioning?**

S3 Versioning allows us to maintain multiple versions of the same object inside an S3 bucket.

Whenever we upload a new file with the same object key, S3 keeps the previous version instead of simply replacing it.

**Real-time example:**

Imagine a company stores an employee salary Excel file.

Initially:

`Employee-Salary.xlsx` → Salary = ₹30,000

After one month, someone uploads a modified file:

`Employee-Salary.xlsx` → Salary = ₹40,000

After another month:

`Employee-Salary.xlsx` → Salary = ₹50,000

Without versioning, the previous file content would be replaced.

With versioning, we can retrieve older versions.

[Efficient Image Recovery at Scale Using Amazon S3 Version...](https://images.openai.com/static-rsc-4/GZKdOLGHwc7gHZguFO2Zajul-yc4_E3UO_8qPQO_ANQn_LjJYte08FnOuRiufIUq5AL2RfAfA0ECjMrlFK8nR2FWmHsmai0fTc3c8PTw1p2PZvCuLhzAYByzOOFU01OZvyBChg7sbPFSPdFdXZoxaB1cT2lpshAPUZhUlpduLnQ?purpose=inline)

[tech.trivago.com](https://tech.trivago.com/post/2018-09-03-s3-versioning?utm_source=chatgpt.com)

### **Problem statement**

A developer accidentally uploads an incorrect configuration file to an S3 bucket, replacing the previous working configuration.

How can the DevOps team recover the previous file?

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

Topic 2 from your image

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

[Supercharge Your Data Superhighway: Unleashing Cross-Region S3 Bucket Replication Awesomeness in AWS! | by Blessing Ogechi Nwojiji | Medium](https://images.openai.com/static-rsc-4/N9_g9XpBam1Z9YnZ0GuHJ2q7QAok8eUgsKp_CcnHrYLEDk9dVOLaBGP5gFCrGfMGLwvbROI7Lsf9_QJyYI6RWmKskGc18VraDLzbpSEj-9eEYwKU4xboczNhAi-J9JOlPOTx9QXz57DTSP7M6E64XsIBawpjDDMjGZamhv8S8sI?purpose=inline)

[medium.com](https://medium.com/%40nwojijiblessing/supercharge-your-data-superhighway-unleashing-cross-region-s3-bucket-replication-awesomeness-in-c556dfb95aa?utm_source=chatgpt.com)

**Architecture**

\#chatgpt-mermaid-\_r_cs\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_cs\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_cs\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_cs\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_cs\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_cs\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_cs\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_cs\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_cs\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_cs\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_cs\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_cs\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_cs\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_cs\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_cs\_ p{margin:0;}#chatgpt-mermaid-\_r_cs\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_cs\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_cs\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_cs\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_cs\_ .label text,#chatgpt-mermaid-\_r_cs\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_cs\_ .node rect,#chatgpt-mermaid-\_r_cs\_ .node circle,#chatgpt-mermaid-\_r_cs\_ .node ellipse,#chatgpt-mermaid-\_r_cs\_ .node polygon,#chatgpt-mermaid-\_r_cs\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_cs\_ .rough-node .label text,#chatgpt-mermaid-\_r_cs\_ .node .label text,#chatgpt-mermaid-\_r_cs\_ .image-shape .label,#chatgpt-mermaid-\_r_cs\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_cs\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_cs\_ .rough-node .label,#chatgpt-mermaid-\_r_cs\_ .node .label,#chatgpt-mermaid-\_r_cs\_ .image-shape .label,#chatgpt-mermaid-\_r_cs\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_cs\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_cs\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_cs\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_cs\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_cs\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_cs\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_cs\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_cs\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_cs\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_cs\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_cs\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_cs\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_cs\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_cs\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_cs\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_cs\_ .icon-shape,#chatgpt-mermaid-\_r_cs\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_cs\_ .icon-shape p,#chatgpt-mermaid-\_r_cs\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_cs\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_cs\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_cs\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_cs\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_cs\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_cs\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_cs\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_cs\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_cs\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_cs\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_cs\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_cs\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_cs\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_cs\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_cs\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_cs\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_cs\_ .node rect,#chatgpt-mermaid-\_r_cs\_ .node circle,#chatgpt-mermaid-\_r_cs\_ .node ellipse,#chatgpt-mermaid-\_r_cs\_ .node polygon,#chatgpt-mermaid-\_r_cs\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_cs\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_cs\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_cs\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_cs\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_cs\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}ApplicationS3 Bucket - MumbaiS3 Bucket - SingaporeDisaster RecoveryAutomatic replication

### **B. Same-Region Replication (SRR)**

SRR copies objects between two S3 buckets in the same AWS Region.

**Example:**

- Production bucket: ecommerce-prod
- Backup bucket: ecommerce-backup
- Both buckets are in Mumbai.

\#chatgpt-mermaid-\_r_d3\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_d3\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_d3\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_d3\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_d3\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_d3\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_d3\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_d3\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_d3\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_d3\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_d3\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_d3\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_d3\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_d3\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_d3\_ p{margin:0;}#chatgpt-mermaid-\_r_d3\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_d3\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_d3\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_d3\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_d3\_ .label text,#chatgpt-mermaid-\_r_d3\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_d3\_ .node rect,#chatgpt-mermaid-\_r_d3\_ .node circle,#chatgpt-mermaid-\_r_d3\_ .node ellipse,#chatgpt-mermaid-\_r_d3\_ .node polygon,#chatgpt-mermaid-\_r_d3\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_d3\_ .rough-node .label text,#chatgpt-mermaid-\_r_d3\_ .node .label text,#chatgpt-mermaid-\_r_d3\_ .image-shape .label,#chatgpt-mermaid-\_r_d3\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_d3\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_d3\_ .rough-node .label,#chatgpt-mermaid-\_r_d3\_ .node .label,#chatgpt-mermaid-\_r_d3\_ .image-shape .label,#chatgpt-mermaid-\_r_d3\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_d3\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_d3\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_d3\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_d3\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_d3\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_d3\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_d3\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_d3\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_d3\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_d3\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_d3\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_d3\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_d3\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_d3\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_d3\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_d3\_ .icon-shape,#chatgpt-mermaid-\_r_d3\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_d3\_ .icon-shape p,#chatgpt-mermaid-\_r_d3\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_d3\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_d3\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_d3\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_d3\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_d3\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_d3\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_d3\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_d3\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_d3\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_d3\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_d3\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_d3\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_d3\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_d3\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_d3\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_d3\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_d3\_ .node rect,#chatgpt-mermaid-\_r_d3\_ .node circle,#chatgpt-mermaid-\_r_d3\_ .node ellipse,#chatgpt-mermaid-\_r_d3\_ .node polygon,#chatgpt-mermaid-\_r_d3\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_d3\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_d3\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_d3\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_d3\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_d3\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Production ApplicationProduction S3 BucketBackup S3 BucketSame AWS RegionReplication

### **Problem statement**

A company stores important business documents in Mumbai. If the Mumbai Region experiences an outage, the company wants another copy of the documents in Singapore.

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

Topic 3 from your image

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

[AWS S3 Encryption: Way to Protect Your Data in S3 - CloudKatha](https://images.openai.com/static-rsc-4/GCpbQFQyg0zNY78GmnVIHiisMnpmlZ-yKzMqIazAXG4nJEN_O1PyPAaOKqUaaxJM0YaRJnJVEP2PsC1UD3OJt9LycQ3nAQFACCXMSdXyOwMbfINSBAobrxLglCu9WMeOHj99_HG7B91--2NrLp5cFxVUWf_HJgF4QMcXGd9cDLA?purpose=inline)

[cloudkatha.com](https://cloudkatha.com/aws-s3-encryption-way-to-protect-your-data-in-s3/?utm_source=chatgpt.com)

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

Topic 4 from your image

## **What is an S3 Bucket Policy?**

An S3 Bucket Policy is a JSON-based resource policy that controls who can access an S3 bucket and what actions they can perform.

We can control:

- Who can access the bucket?
- Who can upload files?
- Who can download files?
- Who can delete objects?
- Whether public access is allowed?

**Real-time example:**

Imagine an IT company has three departments:

| Department | Required access          |
| ---------- | ------------------------ |
| Developers | Upload application files |
| QA Team    | Download testing files   |
| Admin Team | Full bucket management   |

We can configure permissions using bucket policies and IAM policies.

### **Architecture diagram**

\#chatgpt-mermaid-\_r_da\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_da\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_da\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_da\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_da\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_da\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_da\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_da\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_da\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_da\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_da\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_da\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_da\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_da\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_da\_ p{margin:0;}#chatgpt-mermaid-\_r_da\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_da\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_da\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_da\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_da\_ .label text,#chatgpt-mermaid-\_r_da\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_da\_ .node rect,#chatgpt-mermaid-\_r_da\_ .node circle,#chatgpt-mermaid-\_r_da\_ .node ellipse,#chatgpt-mermaid-\_r_da\_ .node polygon,#chatgpt-mermaid-\_r_da\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_da\_ .rough-node .label text,#chatgpt-mermaid-\_r_da\_ .node .label text,#chatgpt-mermaid-\_r_da\_ .image-shape .label,#chatgpt-mermaid-\_r_da\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_da\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_da\_ .rough-node .label,#chatgpt-mermaid-\_r_da\_ .node .label,#chatgpt-mermaid-\_r_da\_ .image-shape .label,#chatgpt-mermaid-\_r_da\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_da\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_da\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_da\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_da\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_da\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_da\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_da\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_da\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_da\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_da\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_da\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_da\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_da\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_da\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_da\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_da\_ .icon-shape,#chatgpt-mermaid-\_r_da\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_da\_ .icon-shape p,#chatgpt-mermaid-\_r_da\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_da\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_da\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_da\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_da\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_da\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_da\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_da\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_da\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_da\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_da\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_da\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_da\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_da\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_da\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_da\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_da\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_da\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_da\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_da\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_da\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_da\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_da\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_da\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_da\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_da\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_da\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_da\_ .node rect,#chatgpt-mermaid-\_r_da\_ .node circle,#chatgpt-mermaid-\_r_da\_ .node ellipse,#chatgpt-mermaid-\_r_da\_ .node polygon,#chatgpt-mermaid-\_r_da\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_da\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_da\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_da\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_da\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_da\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}S3 BucketDevelopersQA TeamAdmin TeamUpload ObjectsDownload ObjectsManage Bucket

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

[Let’s Architect! Modern data architectures | AWS Architecture Blog](https://images.openai.com/static-rsc-4/ufomW17EKNwHLEaijadwMmWSzRai2jb0gzcSARmYJYUUTwnx6lZI4ygU_ziwKPln0D_gF1ZtaezMLMiVIujXHKs-oxSYOq-AX_UBqZVvY4unAdFrPeqDNBuI9BStrl7j_AvysZ1hKyztecXy4BoTySUw8Mx4gtqE0vVvhYGQP_M?purpose=inline)

[aws.amazon.com](https://aws.amazon.com/blogs/architecture/lets-architect-modern-data-architectures-2/?utm_source=chatgpt.com)

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

### **Problem statement**

A company stores 5 years of financial reports in S3.

Current reports are accessed daily, but older reports are rarely accessed.

The company wants to reduce storage costs.

**Solution: S3 Lifecycle Management**

We can create lifecycle rules to transition objects automatically between storage classes.

Example:

\#chatgpt-mermaid-\_r_dm\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_dm\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_dm\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_dm\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_dm\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dm\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_dm\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_dm\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_dm\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_dm\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_dm\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_dm\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_dm\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_dm\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_dm\_ p{margin:0;}#chatgpt-mermaid-\_r_dm\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dm\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dm\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dm\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_dm\_ .label text,#chatgpt-mermaid-\_r_dm\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dm\_ .node rect,#chatgpt-mermaid-\_r_dm\_ .node circle,#chatgpt-mermaid-\_r_dm\_ .node ellipse,#chatgpt-mermaid-\_r_dm\_ .node polygon,#chatgpt-mermaid-\_r_dm\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_dm\_ .rough-node .label text,#chatgpt-mermaid-\_r_dm\_ .node .label text,#chatgpt-mermaid-\_r_dm\_ .image-shape .label,#chatgpt-mermaid-\_r_dm\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_dm\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_dm\_ .rough-node .label,#chatgpt-mermaid-\_r_dm\_ .node .label,#chatgpt-mermaid-\_r_dm\_ .image-shape .label,#chatgpt-mermaid-\_r_dm\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_dm\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_dm\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_dm\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_dm\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_dm\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_dm\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_dm\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_dm\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_dm\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_dm\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_dm\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dm\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dm\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_dm\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dm\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_dm\_ .icon-shape,#chatgpt-mermaid-\_r_dm\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_dm\_ .icon-shape p,#chatgpt-mermaid-\_r_dm\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_dm\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_dm\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_dm\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_dm\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_dm\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_dm\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_dm\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_dm\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_dm\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_dm\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_dm\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_dm\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_dm\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_dm\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_dm\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_dm\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_dm\_ .node rect,#chatgpt-mermaid-\_r_dm\_ .node circle,#chatgpt-mermaid-\_r_dm\_ .node ellipse,#chatgpt-mermaid-\_r_dm\_ .node polygon,#chatgpt-mermaid-\_r_dm\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_dm\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_dm\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_dm\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_dm\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_dm\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Upload ReportS3 StandardS3 Standard-IAS3 Glacier Flexible RetrievalS3 Glacier Deep ArchiveAfter 30 daysAfter 90 daysAfter 365 days

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

[How to detect and monitor Amazon Simple Storage Service (S3) access with AWS CloudTrail and Amazon CloudWatch | AWS Cloud Operations Blog](https://images.openai.com/static-rsc-4/cxUN6wcbWz_qWolS54pEAzERAwuMO_Y5tsbX-5GDoS0b3sjleXJUS8yjromorZtNf1Ua3Ur_bpPs3ey46VuUIgogVhnfp40DgQWNrNLz_xd8_PwW_hor798I8lE_mG90bKl8n0Ue91_eOxG8XNr45cX522uEIjNKYgudzhVUMo0?purpose=inline)

[aws.amazon.com](https://aws.amazon.com/blogs/mt/how-to-detect-and-monitor-amazon-simple-storage-service-s3-access-with-aws-cloudtrail-and-amazon-cloudwatch/?utm_source=chatgpt.com)

### **Architecture diagram**

\#chatgpt-mermaid-\_r_dt\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_dt\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_dt\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_dt\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_dt\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dt\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_dt\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_dt\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_dt\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_dt\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_dt\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_dt\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_dt\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_dt\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_dt\_ p{margin:0;}#chatgpt-mermaid-\_r_dt\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dt\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dt\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dt\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_dt\_ .label text,#chatgpt-mermaid-\_r_dt\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dt\_ .node rect,#chatgpt-mermaid-\_r_dt\_ .node circle,#chatgpt-mermaid-\_r_dt\_ .node ellipse,#chatgpt-mermaid-\_r_dt\_ .node polygon,#chatgpt-mermaid-\_r_dt\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_dt\_ .rough-node .label text,#chatgpt-mermaid-\_r_dt\_ .node .label text,#chatgpt-mermaid-\_r_dt\_ .image-shape .label,#chatgpt-mermaid-\_r_dt\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_dt\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_dt\_ .rough-node .label,#chatgpt-mermaid-\_r_dt\_ .node .label,#chatgpt-mermaid-\_r_dt\_ .image-shape .label,#chatgpt-mermaid-\_r_dt\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_dt\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_dt\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_dt\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_dt\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_dt\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_dt\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_dt\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_dt\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_dt\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_dt\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_dt\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dt\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dt\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_dt\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_dt\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_dt\_ .icon-shape,#chatgpt-mermaid-\_r_dt\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_dt\_ .icon-shape p,#chatgpt-mermaid-\_r_dt\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_dt\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_dt\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_dt\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_dt\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_dt\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_dt\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_dt\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_dt\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_dt\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_dt\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_dt\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_dt\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_dt\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_dt\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_dt\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_dt\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_dt\_ .node rect,#chatgpt-mermaid-\_r_dt\_ .node circle,#chatgpt-mermaid-\_r_dt\_ .node ellipse,#chatgpt-mermaid-\_r_dt\_ .node polygon,#chatgpt-mermaid-\_r_dt\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_dt\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_dt\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_dt\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_dt\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_dt\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}User / ApplicationS3 BucketCloudTrailS3 Server Access LoggingCloudWatch MetricsAudit and API ActivityAccess LogsMonitoring and Alarms

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

[Designing and Building a Static Website on AWS | Cliffable](https://images.openai.com/static-rsc-4/2wwkjSqA0p2mSRQzWkZQnKlUutXLDbOHQeYp7n0yI6V-JlVpEWktrsQUMEhNwoHBcUBjt0B2tLSREX-gtjXh_kPaMTr66sITIfb1FjrGM99-ADtVhSpaWxyFLFLxrrNT7R7hihODg80T95CTymMQReoudIfaqA5NxAzXso0-CzI?purpose=inline)

[cliffable.com](https://cliffable.com/projects/static-site-on-aws.html?utm_source=chatgpt.com)

### **Architecture diagram**

\#chatgpt-mermaid-\_r_e4\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_e4\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_e4\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_e4\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_e4\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_e4\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_e4\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_e4\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_e4\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_e4\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_e4\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_e4\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_e4\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_e4\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_e4\_ p{margin:0;}#chatgpt-mermaid-\_r_e4\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_e4\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_e4\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_e4\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_e4\_ .label text,#chatgpt-mermaid-\_r_e4\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_e4\_ .node rect,#chatgpt-mermaid-\_r_e4\_ .node circle,#chatgpt-mermaid-\_r_e4\_ .node ellipse,#chatgpt-mermaid-\_r_e4\_ .node polygon,#chatgpt-mermaid-\_r_e4\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_e4\_ .rough-node .label text,#chatgpt-mermaid-\_r_e4\_ .node .label text,#chatgpt-mermaid-\_r_e4\_ .image-shape .label,#chatgpt-mermaid-\_r_e4\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_e4\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_e4\_ .rough-node .label,#chatgpt-mermaid-\_r_e4\_ .node .label,#chatgpt-mermaid-\_r_e4\_ .image-shape .label,#chatgpt-mermaid-\_r_e4\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_e4\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_e4\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_e4\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_e4\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_e4\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_e4\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_e4\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_e4\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_e4\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_e4\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_e4\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_e4\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_e4\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_e4\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_e4\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_e4\_ .icon-shape,#chatgpt-mermaid-\_r_e4\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_e4\_ .icon-shape p,#chatgpt-mermaid-\_r_e4\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_e4\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_e4\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_e4\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_e4\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_e4\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_e4\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_e4\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_e4\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_e4\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_e4\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_e4\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_e4\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_e4\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_e4\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_e4\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_e4\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_e4\_ .node rect,#chatgpt-mermaid-\_r_e4\_ .node circle,#chatgpt-mermaid-\_r_e4\_ .node ellipse,#chatgpt-mermaid-\_r_e4\_ .node polygon,#chatgpt-mermaid-\_r_e4\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_e4\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_e4\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_e4\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_e4\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_e4\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Website VisitorInternetCloudFrontS3 Bucketindex.htmlCSS / JS / Images

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

[Page Tool - A Modern Website Management Suite](https://images.openai.com/static-rsc-4/Rcyffiu2yIYHdxL2UA1970NGjJttezWdHvHPWYhOoYVuxejoM2Y685d5oiq_mEyg9Z0Qpl7tMWix1K8FNfrOeA7TdhlWN8AIgQD_i_UMs8JHjlA1z6_CCuLA_wc3jIF6CMVTXNSpqRN7Riyf7Qd_fx9ZPvw8ZsiMSaDrSu3cGLg?purpose=inline)

[pagecli.com](https://pagecli.com/guides/host-website-on-aws?utm_source=chatgpt.com)

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

[AWS Snowball Resources | Amazon Web Services](https://images.openai.com/static-rsc-4/IpmzwYtC8lhPDRpl2n-FrEGMKfeARb5MIX1fwuJjrvarhHXRvQAIsvRG16-JYvZ2lMS3eeIQlgyluVl9LqQ94INx-jFt-Zr801i9AAuzmg0M2TmfmG1oXtYpm1gTCL98PHMHJscBVSNnEgCyCGzA8FsIzomUXxgiiEQCr1kah9Y?purpose=inline)

[aws.amazon.com](https://aws.amazon.com/snowball/resources/?utm_source=chatgpt.com)

### **Real-time example**

A media company has 100 TB of video files stored in its local data center.

It wants to migrate all the video files to Amazon S3.

Instead of transferring all data over the internet, the company can use an AWS Snow Family device.

### **Architecture diagram**

\#chatgpt-mermaid-\_r_eb\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_eb\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_eb\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_eb\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_eb\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_eb\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_eb\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_eb\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_eb\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_eb\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_eb\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_eb\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_eb\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_eb\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_eb\_ p{margin:0;}#chatgpt-mermaid-\_r_eb\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_eb\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_eb\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_eb\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_eb\_ .label text,#chatgpt-mermaid-\_r_eb\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_eb\_ .node rect,#chatgpt-mermaid-\_r_eb\_ .node circle,#chatgpt-mermaid-\_r_eb\_ .node ellipse,#chatgpt-mermaid-\_r_eb\_ .node polygon,#chatgpt-mermaid-\_r_eb\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_eb\_ .rough-node .label text,#chatgpt-mermaid-\_r_eb\_ .node .label text,#chatgpt-mermaid-\_r_eb\_ .image-shape .label,#chatgpt-mermaid-\_r_eb\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_eb\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_eb\_ .rough-node .label,#chatgpt-mermaid-\_r_eb\_ .node .label,#chatgpt-mermaid-\_r_eb\_ .image-shape .label,#chatgpt-mermaid-\_r_eb\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_eb\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_eb\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_eb\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_eb\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_eb\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_eb\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_eb\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_eb\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_eb\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_eb\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_eb\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_eb\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_eb\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_eb\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_eb\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_eb\_ .icon-shape,#chatgpt-mermaid-\_r_eb\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_eb\_ .icon-shape p,#chatgpt-mermaid-\_r_eb\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_eb\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_eb\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_eb\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_eb\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_eb\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_eb\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_eb\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_eb\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_eb\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_eb\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_eb\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_eb\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_eb\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_eb\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_eb\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_eb\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_eb\_ .node rect,#chatgpt-mermaid-\_r_eb\_ .node circle,#chatgpt-mermaid-\_r_eb\_ .node ellipse,#chatgpt-mermaid-\_r_eb\_ .node polygon,#chatgpt-mermaid-\_r_eb\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_eb\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_eb\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_eb\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_eb\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_eb\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}Company Data CenterAWS Snow Family DeviceAWSAmazon S3Physical shipment

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

[AWS Storage Gateway: Connect On-Premises to Cloud Storage](https://images.openai.com/static-rsc-4/xMVzpAgUNZtWlOQYi343lrAdUDlamUuRZarfnIVTmmb6ao7C7mvLGYdryUi7AVePN6FezAQLdGY8BdbOOOYQ4Yol8PrqOGwxZp3WDiB4W09zVtm0x_PhUVb1lb-kMjIaT_LzwqWIAFgKaiMAtQwLNjk68cxhU-r_e2mgo_FuWJw?purpose=inline)

[appinventiv.com](https://appinventiv.com/blog/aws-storage-gateway-enhance-data-management-with-hybrid-storage-integration/?utm_source=chatgpt.com)

### **Architecture diagram**

\#chatgpt-mermaid-\_r_ei\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_ei\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_ei\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_ei\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_ei\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ei\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_ei\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_ei\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_ei\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_ei\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_ei\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_ei\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_ei\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_ei\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_ei\_ p{margin:0;}#chatgpt-mermaid-\_r_ei\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ei\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ei\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ei\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_ei\_ .label text,#chatgpt-mermaid-\_r_ei\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ei\_ .node rect,#chatgpt-mermaid-\_r_ei\_ .node circle,#chatgpt-mermaid-\_r_ei\_ .node ellipse,#chatgpt-mermaid-\_r_ei\_ .node polygon,#chatgpt-mermaid-\_r_ei\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_ei\_ .rough-node .label text,#chatgpt-mermaid-\_r_ei\_ .node .label text,#chatgpt-mermaid-\_r_ei\_ .image-shape .label,#chatgpt-mermaid-\_r_ei\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_ei\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_ei\_ .rough-node .label,#chatgpt-mermaid-\_r_ei\_ .node .label,#chatgpt-mermaid-\_r_ei\_ .image-shape .label,#chatgpt-mermaid-\_r_ei\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_ei\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_ei\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_ei\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_ei\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_ei\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_ei\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_ei\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_ei\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_ei\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_ei\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_ei\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ei\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ei\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_ei\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ei\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_ei\_ .icon-shape,#chatgpt-mermaid-\_r_ei\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_ei\_ .icon-shape p,#chatgpt-mermaid-\_r_ei\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_ei\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_ei\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_ei\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_ei\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_ei\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_ei\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_ei\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_ei\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_ei\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_ei\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_ei\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_ei\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_ei\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_ei\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_ei\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_ei\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_ei\_ .node rect,#chatgpt-mermaid-\_r_ei\_ .node circle,#chatgpt-mermaid-\_r_ei\_ .node ellipse,#chatgpt-mermaid-\_r_ei\_ .node polygon,#chatgpt-mermaid-\_r_ei\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_ei\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_ei\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_ei\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_ei\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_ei\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}On-Premises Data CenterStorage GatewayAWS CloudAmazon S3Amazon S3 Glacier

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

[🔐 Amazon S3 Security: Best Practices for Data Protection - DEV Community](https://images.openai.com/static-rsc-4/mRW4DhME9toiYMjeIVFG0cZcBeQJ_ZK1_I84T2rD-7c_bBw65uojQfqCShj1WEkcZyjU2GTqyauoRuFVmmGLDVF69VR4wKCBvcSvYbB1YENTQXdWgU5ZTt5so0SSy-Qzk1auH90Ac4zgNfeUFERxSBqHypKQnTDHNkKQ3l4Ry5E?purpose=inline)

[dev.to](https://dev.to/gurpreet_kaur_29/amazon-s3-security-best-practices-for-data-protection-4b0n?utm_source=chatgpt.com)

### **Complete architecture diagram**

\#chatgpt-mermaid-\_r_ep\_{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;fill:rgb(13, 13, 13);}@keyframes edge-animation-frame{from{stroke-dashoffset:0;}}@keyframes dash{to{stroke-dashoffset:0;}}#chatgpt-mermaid-\_r_ep\_ .edge-animation-slow{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 50s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_ep\_ .edge-animation-fast{stroke-dasharray:9,5!important;stroke-dashoffset:900;animation:dash 20s linear infinite;stroke-linecap:round;}#chatgpt-mermaid-\_r_ep\_ .error-icon{fill:rgb(243, 243, 243);}#chatgpt-mermaid-\_r_ep\_ .error-text{fill:rgb(13, 13, 13);stroke:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ep\_ .edge-thickness-normal{stroke-width:1px;}#chatgpt-mermaid-\_r_ep\_ .edge-thickness-thick{stroke-width:3.5px;}#chatgpt-mermaid-\_r_ep\_ .edge-pattern-solid{stroke-dasharray:0;}#chatgpt-mermaid-\_r_ep\_ .edge-thickness-invisible{stroke-width:0;fill:none;}#chatgpt-mermaid-\_r_ep\_ .edge-pattern-dashed{stroke-dasharray:3;}#chatgpt-mermaid-\_r_ep\_ .edge-pattern-dotted{stroke-dasharray:2;}#chatgpt-mermaid-\_r_ep\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_ep\_ .marker.cross{stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_ep\_ svg{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:16px;}#chatgpt-mermaid-\_r_ep\_ p{margin:0;}#chatgpt-mermaid-\_r_ep\_ .label{font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ep\_ .cluster-label text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ep\_ .cluster-label span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ep\_ .cluster-label span p{background-color:transparent;}#chatgpt-mermaid-\_r_ep\_ .label text,#chatgpt-mermaid-\_r_ep\_ span{fill:rgb(13, 13, 13);color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ep\_ .node rect,#chatgpt-mermaid-\_r_ep\_ .node circle,#chatgpt-mermaid-\_r_ep\_ .node ellipse,#chatgpt-mermaid-\_r_ep\_ .node polygon,#chatgpt-mermaid-\_r_ep\_ .node path{fill:rgb(222, 234, 251);stroke:rgb(83, 154, 248);stroke-width:1px;}#chatgpt-mermaid-\_r_ep\_ .rough-node .label text,#chatgpt-mermaid-\_r_ep\_ .node .label text,#chatgpt-mermaid-\_r_ep\_ .image-shape .label,#chatgpt-mermaid-\_r_ep\_ .icon-shape .label{text-anchor:middle;}#chatgpt-mermaid-\_r_ep\_ .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#chatgpt-mermaid-\_r_ep\_ .rough-node .label,#chatgpt-mermaid-\_r_ep\_ .node .label,#chatgpt-mermaid-\_r_ep\_ .image-shape .label,#chatgpt-mermaid-\_r_ep\_ .icon-shape .label{text-align:center;}#chatgpt-mermaid-\_r_ep\_ .node.clickable{cursor:pointer;}#chatgpt-mermaid-\_r_ep\_ .root .anchor path{fill:rgb(143, 143, 143)!important;stroke-width:0;stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_ep\_ .arrowheadPath{fill:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_ep\_ .edgePath .path{stroke:rgb(143, 143, 143);stroke-width:1px;}#chatgpt-mermaid-\_r_ep\_ .flowchart-link{stroke:rgb(143, 143, 143);fill:none;}#chatgpt-mermaid-\_r_ep\_ .edgeLabel{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_ep\_ .edgeLabel p{background-color:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_ep\_ .edgeLabel rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_ep\_ .labelBkg{background-color:rgba(252, 252, 252, 0.5);}#chatgpt-mermaid-\_r_ep\_ .cluster rect{fill:rgb(243, 243, 243);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_ep\_ .cluster text{fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ep\_ .cluster span{color:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ep\_ div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";font-size:12px;background:rgb(243, 243, 243);border:1px solid rgba(0, 0, 0, 0.1);border-radius:2px;pointer-events:none;z-index:100;}#chatgpt-mermaid-\_r_ep\_ .flowchartTitleText{text-anchor:middle;font-size:18px;fill:rgb(13, 13, 13);}#chatgpt-mermaid-\_r_ep\_ rect.text{fill:none;stroke-width:0;}#chatgpt-mermaid-\_r_ep\_ .icon-shape,#chatgpt-mermaid-\_r_ep\_ .image-shape{background-color:rgb(252, 252, 252);text-align:center;}#chatgpt-mermaid-\_r_ep\_ .icon-shape p,#chatgpt-mermaid-\_r_ep\_ .image-shape p{background-color:rgb(252, 252, 252);padding:2px;}#chatgpt-mermaid-\_r_ep\_ .icon-shape .label rect,#chatgpt-mermaid-\_r_ep\_ .image-shape .label rect{opacity:0.5;background-color:rgb(252, 252, 252);fill:rgb(252, 252, 252);}#chatgpt-mermaid-\_r_ep\_ .label-icon{display:inline-block;height:1em;overflow:visible;vertical-align:-0.125em;}#chatgpt-mermaid-\_r_ep\_ .node .label-icon path{fill:currentColor;stroke:revert;stroke-width:revert;}#chatgpt-mermaid-\_r_ep\_ .node .neo-node{stroke:rgb(83, 154, 248);}#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].node rect,#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].cluster rect,#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].node polygon{stroke:url(#chatgpt-mermaid-\_r_ep\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].swimlane.cluster rect{filter:none;}#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].node path{stroke:url(#chatgpt-mermaid-\_r_ep\_-gradient);stroke-width:1px;}#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].node .outer-path{filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].node .neo-line path{stroke:rgb(83, 154, 248);filter:none;}#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].node circle{stroke:url(#chatgpt-mermaid-\_r_ep\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].node circle .state-start{fill:#000000;}#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].icon-shape .icon{fill:url(#chatgpt-mermaid-\_r_ep\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_ep\_ [data-look="neo"].icon-shape .icon-neo path{stroke:url(#chatgpt-mermaid-\_r_ep\_-gradient);filter:drop-shadow( 1px 2px 2px rgba(185,185,185,1));}#chatgpt-mermaid-\_r_ep\_ .node text{font-size:14px;font-weight:600;letter-spacing:normal;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_ep\_ .edgeLabels text{font-size:13px;font-weight:600;letter-spacing:-0.08px;fill:rgb(0, 79, 153);}#chatgpt-mermaid-\_r_ep\_ .node tspan[font-weight="normal"],#chatgpt-mermaid-\_r_ep\_ .edgeLabels tspan[font-weight="normal"]{font-weight:600;}#chatgpt-mermaid-\_r_ep\_ .edgeLabel .label rect{opacity:1;rx:13px;ry:13px;fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-width:1px;}#chatgpt-mermaid-\_r_ep\_ .node rect,#chatgpt-mermaid-\_r_ep\_ .node circle,#chatgpt-mermaid-\_r_ep\_ .node ellipse,#chatgpt-mermaid-\_r_ep\_ .node polygon,#chatgpt-mermaid-\_r_ep\_ .node path{fill:rgb(229, 243, 255);stroke:rgba(0, 0, 0, 0.1);stroke-width:1px;}#chatgpt-mermaid-\_r_ep\_ .node rect{rx:16px;ry:16px;}#chatgpt-mermaid-\_r_ep\_ .mermaid-decision .label-container{fill:rgb(245, 250, 255);stroke:rgb(206, 219, 229);stroke-dasharray:2,2;}#chatgpt-mermaid-\_r_ep\_ .edgePaths .flowchart-link{stroke:rgb(143, 143, 143);stroke-width:1px;stroke-linecap:round;stroke-linejoin:round;}#chatgpt-mermaid-\_r_ep\_ .marker{fill:rgb(143, 143, 143);stroke:rgb(143, 143, 143);}#chatgpt-mermaid-\_r_ep\_ :root{--mermaid-font-family:-apple-system-body,ui-sans-serif,-apple-system,system-ui,"Segoe UI",Helvetica,"Apple Color Emoji",Arial,sans-serif,"Segoe UI Emoji","Segoe UI Symbol";}E-Commerce ApplicationAmazon S3 - Primary BucketS3 VersioningEncryption - SSE-S3 / SSE-KMSBucket PoliciesLifecycle ManagementCloudTrail / LoggingStatic Website HostingCross-Region ReplicationS3 DR BucketS3 GlacierCloudWatch MonitoringCloudFrontOn-Premises Data CenterStorage GatewaySnow Family Device

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

# **13. Suggested Teaching Plan**

Since these are intermediate S3 topics, I recommend teaching them across three sessions rather than rushing all nine topics into one hour.

**Session 1 – S3 Security and Data Protection**

90 minutes

- S3 Versioning – 20 minutes
- S3 Replication – 25 minutes
- Data Encryption – 20 minutes
- Bucket Policies – 25 minutes

**Session 2 – S3 Cost Optimization and Monitoring**

60 minutes

- Storage Classes – 25 minutes
- Lifecycle Management – 15 minutes
- Logging and Monitoring – 20 minutes

**Session 3 – Advanced S3 Use Cases**

60 minutes

- Static Website Hosting – 20 minutes
- AWS Snow Family – 15 minutes
- Storage Gateway – 25 minutes

## **Practical assignments for students**

Ask students to implement these scenarios:

1. **Versioning:** Create an S3 bucket, upload a file, modify it, upload it again and restore the previous version.
2. **Replication:** Create two buckets in different AWS Regions and configure CRR.
3. **Encryption:** Enable SSE-S3 or SSE-KMS encryption.
4. **Bucket Policy:** Allow a user to upload objects without granting delete permission.
5. **Lifecycle:** Move objects from S3 Standard to Glacier using lifecycle rules.
6. **Monitoring:** Configure CloudTrail S3 data events and inspect object activity.
7. **Static Website:** Host a basic HTML website using S3.

**My recommendation:** Start with Versioning, Replication, Encryption and Bucket Policies. These four topics are particularly important for AWS Cloud Support and DevOps Engineer interviews because they cover data protection, disaster recovery and security.
