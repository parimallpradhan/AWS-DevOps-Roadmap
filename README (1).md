# 90-Day AWS & DevOps Training Roadmap

A structured 90-day learning plan covering Cloud Computing, Linux, AWS,
DevOps tools, CI/CD, containers, Kubernetes, Terraform, and a final
end-to-end project.

## Program Overview

-   **Duration:** 90 days
-   **Suggested class duration:** 1 hour per day
-   **Learning approach:** Theory, instructor demonstration, hands-on
    practice, and revision
-   **Outcome:** Build practical skills to deploy AWS infrastructure and
    implement an end-to-end DevOps workflow.

### Suggested Daily Session Structure

  Activity                                     Duration
  ------------------------------------ ----------------
  Theory and concepts                        15 minutes
  Instructor practical demonstration         30 minutes
  Student hands-on practice                  10 minutes
  Revision and questions                      5 minutes
  **Total**                              **60 minutes**

> Additional lab practice outside the one-hour session is recommended,
> especially for networking, Jenkins, Kubernetes, and Terraform.

------------------------------------------------------------------------

## 90-Day Learning Roadmap

### Phase 1: Cloud and Linux Foundations (Days 1--10)

**Goal:** Understand cloud computing concepts and become comfortable
working with Linux.

  ------------------------------------------------------------------------
                           Day Topic                 Practical /
                                                     Assignment
  ---------------------------- --------------------- ---------------------
                             1 Cloud Computing       Understand cloud
                               Introduction          computing and its
                                                     benefits

                             2 Public, Private &     Compare cloud
                               Hybrid Cloud          deployment models

                             3 IaaS, PaaS & SaaS     Identify real-world
                                                     use cases

                             4 Linux Introduction &  Install Ubuntu on
                               Installation          VirtualBox or another
                                                     suitable environment

                             5 Linux Basic Commands  Practice navigation
                                                     and file commands

                             6 Linux File System &   Install and remove
                               Package Management    packages

                             7 Linux Users, Groups & Create users and
                               Permissions           configure permissions

                             8 Linux Process &       Manage processes and
                               Service Management    services

                             9 Shell Scripting       Write basic shell
                                                     scripts

                            10 Linux Revision &      Complete a Linux
                               Assessment            practical assignment
  ------------------------------------------------------------------------

### Phase 2: AWS Core Services (Days 11--25)

**Goal:** Learn the essential AWS services used to build and operate
cloud infrastructure.

  ------------------------------------------------------------------------
                           Day Topic                 Practical /
                                                     Assignment
  ---------------------------- --------------------- ---------------------
                            11 AWS Introduction &    Explore the AWS
                               Global Infrastructure Management Console

                            12 IAM -- Users, Groups  Create IAM users and
                               & Policies            groups

                            13 IAM Roles & MFA       Configure roles and
                                                     multi-factor
                                                     authentication

                            14 EC2 Introduction      Launch an EC2
                                                     instance

                            15 EC2 Instance Types &  Create and use an AMI
                               AMI                   

                            16 EBS & EBS Snapshots   Attach volumes and
                                                     create snapshots

                            17 EC2 User Data & Key   Automate basic server
                               Pairs                 configuration

                            18 S3 Fundamentals       Create buckets and
                                                     upload files

                            19 S3 Versioning &       Configure versioning
                               Lifecycle             and lifecycle rules

                            20 S3 Storage Classes &  Explore archival
                               Glacier               storage

                            21 AWS CLI               Configure AWS CLI and
                                                     execute commands

                            22 RDS                   Create a MySQL RDS
                                                     instance

                            23 DynamoDB              Create a NoSQL table

                            24 ElastiCache &         Understand caching
                               Database Overview     use cases

                            25 AWS Core Services     Complete an EC2 +
                               Revision              S3 + RDS assignment
  ------------------------------------------------------------------------

### Phase 3: AWS Networking & Infrastructure (Days 26--40)

**Goal:** Design and deploy networked, scalable AWS infrastructure.

  ------------------------------------------------------------------------
                           Day Topic                 Practical /
                                                     Assignment
  ---------------------------- --------------------- ---------------------
                            26 VPC Fundamentals      Understand AWS
                                                     networking

                            27 Custom VPC & Subnets  Create a custom VPC

                            28 Internet Gateway &    Connect a public
                               Route Tables          subnet to the
                                                     internet

                            29 Security Groups &     Configure network
                               NACLs                 security

                            30 NAT Gateway           Configure private
                                                     subnet internet
                                                     access

                            31 DHCP Options, DNS &   Explore network
                               VPC Peering           connectivity

                            32 Elastic Load          Understand ALB, NLB
                               Balancing             and load balancing

                            33 Application Load      Create an ALB
                               Balancer              

                            34 Target Groups &       Register multiple EC2
                               Health Checks         instances

                            35 Auto Scaling          Create a launch
                               Fundamentals          template and Auto
                                                     Scaling Group

                            36 Auto Scaling Policies Configure scaling
                                                     policies

                            37 Auto Scaling with     Build a scalable web
                               Load Balancer         application

                            38 CloudWatch            Create metrics,
                                                     dashboards and alarms

                            39 CloudTrail            Review AWS account
                                                     activity

                            40 AWS Networking        Deploy a highly
                               Project               available web
                                                     application
  ------------------------------------------------------------------------

### Phase 4: Advanced AWS Services (Days 41--50)

**Goal:** Explore AWS automation, application, monitoring, storage and
security services.

  ------------------------------------------------------------------------
                           Day Topic                 Practical /
                                                     Assignment
  ---------------------------- --------------------- ---------------------
                            41 CloudFormation        Understand
                               Fundamentals          infrastructure as
                                                     code

                            42 CloudFormation        Create an EC2
                               Templates & JSON      resource using a
                                                     template

                            43 AWS Lambda            Create a Lambda
                                                     function

                            44 Lambda Triggers       Trigger Lambda using
                                                     S3

                            45 SNS & SQS             Configure
                                                     notifications and
                                                     queues

                            46 SES & Elastic         Explore application
                               Beanstalk             deployment services

                            47 CloudFront & Route 53 Explore CDN and DNS

                            48 AWS KMS & Security    Understand encryption
                                                     and key management

                            49 Storage Gateway,      Understand hybrid
                               Snowball & DMS        storage and migration

                            50 AWS Security Revision Complete an AWS
                                                     security assignment
  ------------------------------------------------------------------------

### Phase 5: DevOps Fundamentals & Git (Days 51--58)

**Goal:** Understand the DevOps lifecycle and manage source code with
Git and GitHub.

  ------------------------------------------------------------------------
                           Day Topic                 Practical /
                                                     Assignment
  ---------------------------- --------------------- ---------------------
                            51 Introduction to       Study SDLC, DevOps
                               DevOps                lifecycle and culture

                            52 DevOps Tools &        Understand the DevOps
                               Architecture          toolchain

                            53 Git Fundamentals      Install Git and
                                                     configure identity

                            54 Git Commands          Practice add, commit,
                                                     push and pull

                            55 GitHub                Create repositories
                                                     and upload code

                            56 Git Branching &       Practice branching
                               Merging               strategies

                            57 GitHub Collaboration  Practice pull
                                                     requests and conflict
                                                     resolution

                            58 Git Project           Create and manage a
                                                     GitHub project
  ------------------------------------------------------------------------

### Phase 6: Docker & Containerization (Days 59--66)

**Goal:** Package applications into containers and understand container
orchestration.

  ------------------------------------------------------------------------
                           Day Topic                 Practical /
                                                     Assignment
  ---------------------------- --------------------- ---------------------
                            59 Docker Introduction & Install Docker
                               Architecture          

                            60 Docker Images &       Pull and run
                               Containers            containers

                            61 Dockerfile            Build custom Docker
                                                     images

                            62 Docker Volumes        Persist application
                                                     data

                            63 Docker Networking     Configure container
                                                     communication

                            64 Docker Compose        Run multi-container
                                                     applications

                            65 Docker Hub & Image    Push images to Docker
                               Management            Hub

                            66 Docker Swarm &        Deploy a basic Swarm
                               Container             application
                               Orchestration         
  ------------------------------------------------------------------------

### Phase 7: Maven, Ansible & Jenkins (Days 67--76)

**Goal:** Automate application builds, configuration management and
CI/CD.

  ------------------------------------------------------------------------
                           Day Topic                 Practical /
                                                     Assignment
  ---------------------------- --------------------- ---------------------
                            67 Maven Fundamentals    Install Maven and
                                                     build a Java
                                                     application

                            68 Continuous Testing    Execute automated
                                                     test cases

                            69 Ansible Introduction  Install Ansible and
                                                     configure inventory

                            70 Ansible Ad-hoc        Manage remote Linux
                               Commands              servers

                            71 Ansible Playbooks     Write automation
                                                     playbooks

                            72 Ansible Roles         Create reusable
                                                     Ansible roles

                            73 Jenkins Introduction  Install and configure
                                                     Jenkins

                            74 Jenkins Jobs & GitHub Create a Jenkins job
                               Integration           

                            75 Jenkins Pipeline      Create a CI/CD
                                                     pipeline using a
                                                     Jenkinsfile

                            76 End-to-End CI/CD      Build a GitHub →
                                                     Maven → Jenkins →
                                                     Docker pipeline
  ------------------------------------------------------------------------

### Phase 8: Kubernetes & Terraform (Days 77--85)

**Goal:** Deploy containerized applications and automate infrastructure
provisioning.

  ------------------------------------------------------------------------
                           Day Topic                 Practical /
                                                     Assignment
  ---------------------------- --------------------- ---------------------
                            77 Kubernetes            Understand cluster
                               Introduction &        architecture
                               Architecture          

                            78 Kubernetes            Set up a Kubernetes
                               Installation          learning cluster

                            79 Kubernetes Pods &     Deploy an application
                               Deployments           using YAML

                            80 Kubernetes Services   Configure ClusterIP,
                                                     NodePort and
                                                     LoadBalancer

                            81 Kubernetes ConfigMaps Manage application
                               & Secrets             configuration

                            82 Kubernetes Ingress &  Configure Ingress and
                               Scaling               replicas

                            83 Terraform             Install Terraform and
                               Fundamentals          understand HCL

                            84 Terraform Providers,  Connect Terraform
                               Variables & State     with AWS

                            85 Terraform AWS         Create VPC, EC2 and
                               Infrastructure        S3 using Terraform
  ------------------------------------------------------------------------

### Phase 9: Capstone Project & Career Preparation (Days 86--90)

**Goal:** Combine the skills learned and demonstrate them through a
project.

  ------------------------------------------------------------------------
                           Day Topic                 Practical /
                                                     Assignment
  ---------------------------- --------------------- ---------------------
                            86 Project Architecture  Design the AWS
                                                     infrastructure and
                                                     application workflow

                            87 Infrastructure        Provision AWS
                               Deployment            resources using
                                                     Terraform

                            88 CI/CD & Kubernetes    Deploy an application
                               Deployment            using Jenkins and
                                                     Kubernetes

                            89 Resume & Interview    Prepare a resume and
                               Preparation           AWS/DevOps interview
                                                     questions

                            90 Final Project         Present the project
                               Presentation & Mock   and complete a final
                               Interview             assessment
  ------------------------------------------------------------------------

------------------------------------------------------------------------

## Suggested Hands-On Projects

### Project 1: AWS Web Hosting

**Suggested services:** EC2, Apache/Nginx, S3 and IAM.

**Tasks:** - Launch an EC2 instance. - Install and configure a web
server. - Host a sample website. - Upload static assets to S3. - Apply
appropriate IAM permissions.

**Roadmap alignment:** Days 14--25.

### Project 2: Highly Available AWS Architecture

**Suggested services:** VPC, EC2, Application Load Balancer, Auto
Scaling and CloudWatch.

**Tasks:** - Create a VPC with public and private subnets. - Configure
routing and security. - Launch multiple application instances. -
Configure a load balancer and health checks. - Configure Auto Scaling
and CloudWatch alarms.

**Roadmap alignment:** Days 26--40.

### Project 3: CI/CD Pipeline

**Suggested tools:** GitHub, Maven, Jenkins and Docker.

**Tasks:** - Store application source code in GitHub. - Build the
application using Maven. - Configure Jenkins automation. - Build a
Docker image. - Publish the image to a container registry.

**Roadmap alignment:** Days 59--76.

### Project 4: Kubernetes Application Deployment

**Suggested tools:** Docker and Kubernetes.

**Tasks:** - Deploy a containerized application. - Create Kubernetes
Deployments and Services. - Configure application settings. - Explore
Ingress and scaling.

**Roadmap alignment:** Days 77--85.

### Project 5: End-to-End AWS DevOps Project

**Suggested workflow:**

``` text
Developer
   |
   v
GitHub Repository
   |
   v
Jenkins CI/CD Pipeline
   |
   v
Maven Build and Test
   |
   v
Docker Image Build
   |
   v
Container Registry
   |
   v
Kubernetes Deployment
   |
   v
AWS Infrastructure
   ^
   |
Terraform
```

**Tasks:** - Provision infrastructure using Terraform. - Store
application code in GitHub. - Automate builds and tests with Jenkins. -
Build and publish Docker images. - Deploy the application to
Kubernetes. - Demonstrate monitoring and troubleshooting.

**Roadmap alignment:** Days 86--90, building on the earlier tool
exercises.

------------------------------------------------------------------------

## Weekly Progress Tracker

Use the checkboxes below to track completion.

-   [ ] Week 1 -- Cloud fundamentals and Linux basics
-   [ ] Week 2 -- Linux and AWS introduction
-   [ ] Week 3 -- IAM, EC2 and S3
-   [ ] Week 4 -- AWS storage and databases
-   [ ] Week 5 -- VPC and networking
-   [ ] Week 6 -- Load balancing and Auto Scaling
-   [ ] Week 7 -- Advanced AWS services and security
-   [ ] Week 8 -- DevOps fundamentals and Git
-   [ ] Week 9 -- Docker and containerization
-   [ ] Week 10 -- Maven and Ansible
-   [ ] Week 11 -- Jenkins and CI/CD
-   [ ] Week 12 -- Kubernetes and Terraform
-   [ ] Final 6 days -- Capstone project and interviews

## Teaching and Assessment Guidelines

For each topic:

1.  Explain the concept and its real-world use.
2.  Demonstrate the service or tool.
3.  Give students a guided hands-on exercise.
4.  Assign independent practice.
5.  Ask students to explain what they built.
6.  Conduct short revision questions or an assessment.

### Recommended Assessment Pattern

-   Daily practical exercises.
-   Weekly revision and doubt-solving.
-   Weekly technical assessments.
-   GitHub repository for assignments.
-   Architecture diagram explanations.
-   Final end-to-end project demonstration.
-   Resume review and mock interviews.

## Important Lab and Cost-Safety Notes

-   Use an AWS account with appropriate budget alerts and billing
    visibility.
-   Follow least-privilege IAM practices.
-   Never commit AWS access keys, passwords, tokens or other secrets to
    GitHub.
-   Review and delete unused cloud resources after labs.
-   Check current AWS pricing before creating paid resources such as NAT
    Gateways, load balancers and managed databases.
-   Use isolated learning environments for Kubernetes and container
    experiments.

------------------------------------------------------------------------

## Final Learning Outcomes

By completing this roadmap and its practical assignments, students
should be able to:

-   Explain cloud computing, AWS and DevOps fundamentals.
-   Work with Linux commands and shell scripts.
-   Deploy and manage AWS compute, storage, database and networking
    services.
-   Apply IAM and basic AWS security practices.
-   Build Docker images and run containers.
-   Automate configuration using Ansible.
-   Build CI/CD workflows using Jenkins.
-   Deploy applications using Kubernetes.
-   Provision infrastructure using Terraform.
-   Present an end-to-end AWS DevOps project.

------------------------------------------------------------------------

**Suggested repository name:** `90-days-aws-devops-roadmap`

**Suggested repository structure:**

``` text
90-days-aws-devops-roadmap/
│
├── README.md
├── phase-01-cloud-linux/
├── phase-02-aws-core-services/
├── phase-03-aws-networking/
├── phase-04-advanced-aws/
├── phase-05-devops-git/
├── phase-06-docker/
├── phase-07-maven-ansible-jenkins/
├── phase-08-kubernetes-terraform/
├── phase-09-capstone-project/
└── assignments/
```

Use the phase folders to store notes, diagrams, commands, screenshots,
YAML files, scripts, Terraform code and project documentation as you
progress.
