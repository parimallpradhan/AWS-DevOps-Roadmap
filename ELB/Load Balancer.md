# **AWS High Availability & Load Balancer Architecture**

We will understand:

1. High Availability (HA)
2. Load Balancer Architecture
3. Classic Load Balancer (CLB)
4. Application Load Balancer (ALB)
5. Network Load Balancer (NLB)
6. Gateway Load Balancer (GWLB)
7. Hands-on architecture and interview questions

## **1. What is High Availability (HA)?**

Concept with real-time example

High Availability means designing an application so that it continues to work even if one server or component fails.

### **Problem statement**

An e-commerce company runs its website on a single EC2 instance.

[AWS Architecture Diagrams Solution | ConceptDraw.com](https://images.openai.com/static-rsc-4/sOrL4s3_SutN5DxEzmrF9lSJuJ029AUkpWhKIfz0hz9ThAdObxkuG8U0c-1mMyIlgVr3Yrm9mzTgHSX8DLVKwmq26RaEBx37BJNSxSuB7ASlxGVKyCVclxAEPpEiqqp3SUEfqD2yBjtUeoCEeAHJeB882wYMgQDh3ppyXoX834U?purpose=inline)

[conceptdraw.com](https://www.conceptdraw.com/solution-park/computer-networks-aws?utm_source=chatgpt.com)

If the EC2 instance stops working:

- Customers cannot open the website.
- Customers cannot place orders.
- The business may lose revenue.

This is called a **Single Point of Failure (SPOF)**.

### **Solution: High Availability architecture**

Instead of using one EC2 instance, deploy multiple EC2 instances across different Availability Zones.

[Building Resilient Cloud Architecture with EC2, Auto Scaling & Load Balancer — My Real-World DevOps Best Practice's. | by NANDAN M | Medium](https://images.openai.com/static-rsc-4/hzVZ_2TKF4mx51aASyCYfzg00t1IPyveIKb3b2U91JkQorW3DCJHPNxGTvlNMhMocIPr-lLMBjWugOWhc5lbzPc4VTcW2LY55qmib5PrjAc3pg4i4hc5eVUU0P7cYQxOqCPxt6RU52X_JxqJ5TYx7LnN_LPKwvanl115M8_3Vj8?purpose=inline)

[medium.com](https://medium.com/%40nandanm603/building-resilient-cloud-architecture-with-ec2-auto-scaling-load-balancer-my-real-world-4448a7d6be03?utm_source=chatgpt.com)

Architecture flow

Customer → Load Balancer → EC2 Instance 1 (AZ-A)

　　　　　　　　　　→ EC2 Instance 2 (AZ-B)

If EC2 Instance 1 fails, the Load Balancer sends traffic to EC2 Instance 2.

**Important:** High Availability does not mean that failure never happens. It means the application is designed to continue working when a component fails.

## **2. What is a Load Balancer?**

A Load Balancer distributes incoming traffic across multiple backend servers.

[SDC#20 - Load Balancers - by Saurabh Dashora](https://images.openai.com/static-rsc-4/rGpbVk-3Phnb6PwmTWGLO9ItSEhZpyx79gWOIzJHqMX37Rb1Z4rjjhjQi_ne3SnKfZhy5fzQerovQbhOEF1-Ehyzyp4S0wqXqDqhFYsGhtXqrEsRcA9E_lANj3YWVsn0OHIqbFce1YI-BAQMkKK6jxI7ngDFD1Kef-a-KS2PqUI?purpose=inline)

[newsletter.systemdesigncodex.com](https://newsletter.systemdesigncodex.com/p/load-balancers?utm_source=chatgpt.com)

### **Real-time example**

Imagine a shopping mall with three entry gates.

- Customers arrive at the mall.
- A security person directs customers to different gates.
- If one gate is closed, customers can use the other gates.

A Load Balancer works similarly.

| Component               | AWS example   |
| ----------------------- | ------------- |
| Customers               | Website users |
| Entry gate              | Load Balancer |
| Mall gates              | EC2 instances |
| Gate availability check | Health checks |

### **Benefits**

- Distributes traffic across multiple servers
- Improves application availability
- Supports scaling
- Performs health checks
- Prevents sending traffic to unhealthy targets

## **3. High Availability Architecture with AWS Load Balancer**

E-commerce application example

### **Problem statement — Jira ticket**

AWS-101

Junior DevOps Engineer

**Title:** Implement High Availability for E-commerce Website

**Description:**

The e-commerce website is currently running on a single EC2 instance. Whenever the server goes down, customers are unable to access the website.

The DevOps team must deploy multiple EC2 instances across different Availability Zones and configure a Load Balancer to distribute traffic.

**Acceptance criteria:**

- Website should remain accessible if one EC2 instance fails.
- Traffic should be distributed across healthy EC2 instances.
- Load Balancer should perform health checks.
- Architecture should support future scaling.

### **Solution architecture**

AWS architecture

```
                  Customers
                     |
                     |
              Internet Gateway
                     |
                     |
            Application Load
                Balancer
                     |
          +----------+----------+
          |                     |
          v                     v
      AZ-A (Mumbai)         AZ-B (Mumbai)
      EC2 Instance 1        EC2 Instance 2
      Web Server             Web Server
          |                     |
          +----------+----------+
                     |
               Application
```

In AWS, an Availability Zone is one or more discrete data centers with independent infrastructure within an AWS Region.

For High Availability:

- Deploy EC2 instances in different AZs.
- Configure a Load Balancer across those AZs.
- Configure health checks.
- Use an Auto Scaling Group to replace failed instances and adjust capacity.

An Application Load Balancer can distribute requests across registered targets in multiple AZs and route traffic only to healthy targets.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

Elastic Load Balancing+1



**Important teaching point:** Two EC2 instances in the same AZ provide server redundancy, but not protection against an AZ-level failure.

## **4. Types of AWS Load Balancers**

AWS Elastic Load Balancing provides four types of Load Balancers.

[Introduction To AWS ELB - Part Two](https://images.openai.com/static-rsc-4/P-j7GMLLga-vKajMGy-_beqd1qLVjq1jT34AXrDqLPwwOlsqJAXZPYgVHAH0xb2eUnGlVgm1T6MOZ0k1lMOcrWZJrwxE0gASdsrh3-hYHu-o2SpDcjmuSlvuB03zzzAbpo1aPYYK28mjH3mfkOzh6hM9N04Zs-ToW-Gq9PIZg-s?purpose=inline)

**Classic Load Balancer (CLB)**

Previous generation • Layer 4 and Layer 7

[AWS Application Load Balancer (ALB) 使用時の注意点 | 大阪のAWSパートナー | ターン・アンド・フロンティア](https://images.openai.com/static-rsc-4/5fbOAgdONQgXRE6Z03PCMu1d7OHXttmaAjCUjdYNd4rw3vtZvvGOtu_VYtbbTJyVMWEWQ4yUBMrYP-H2B7QIrxV3nJfsoziMNAWJ4npbSsEhHGMeENXiLUDeRpU63VwyQZiiE4LfGogFFHbwytR_6ZMWTRPK8oYNRlKtCZB_HhU?purpose=inline)

**Application Load Balancer (ALB)**

Layer 7 • HTTP and HTTPS

[Workload Architecture - ELB Best Practices Guides](https://images.openai.com/static-rsc-4/B3EWhJ8MLlQ3RW71YQWBM-Jr6LkE1Im-iYr__BGr1CTVjFqdhGrRf3HdYlwpqbN5MU2-QTjkB6b19TTAWXFCYTY7wrMeOwanWHcnM48hBun1Jze9rbpMnDdp_9iA74tNk3QYyow3-v8OCj1upVwv24m5lzqd_UOcmtZIRQ2HYEw?purpose=inline)

**Network Load Balancer (NLB)**

Layer 4 • TCP, UDP, TLS

[Integrate your custom logic or appliance with AWS Gateway Load Balancer | Networking & Content Delivery](https://images.openai.com/static-rsc-4/aGl2NrairPl3wK6KIahfhoD9gqfy6I43cC-UulYKfUt0vEUIHJOsQiuRFUjtGVBlYapQ49JRnMKgBqVzLVUklGNKdcqK8HECcdNNiGAMxHfwN8hBBVdAb8wB-TZyuSNr0HdF2MCgptK0oYJKWEUdlrLmBlKgT1cSWvGqSYg4Pgw?purpose=inline)

**Gateway Load Balancer (GWLB)**

Layer 3 • Network traffic and security appliances

AWS recommends current-generation ALB, NLB, and GWLB for new architectures. CLB is the previous generation.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

Elastic Load Balancing+1



## **5. Classic Load Balancer (CLB)**

[Mit dem Internet verbundene Classic Load Balancer - ELB](https://images.openai.com/static-rsc-4/bXn1uHgGljgCl2bhKnv6OQaFcGujugGNbnc6rN5hNWhn_F8t8n0j4wfvgHL2mSSRkWFPLIENYX5sRIBwgUQ27LUUZ8q_n1JtyySmdUfpcZhi8_hwB1AHUi_s_HC8roEn77szG_FCPa7mvL16FXW8Yz6j2AzDy7yy3LhBQ-rHawc?purpose=inline)

[docs.aws.amazon.com](https://docs.aws.amazon.com/de_de/elasticloadbalancing/latest/classic/elb-internet-facing-load-balancers.html?utm_source=chatgpt.com)

### **What is CLB?**

Classic Load Balancer is the older generation of AWS Load Balancer.

It supports traffic at:

- Layer 4 — TCP and SSL
- Layer 7 — HTTP and HTTPS

### **Architecture**

```
       Customer
          |
          v
     Classic LB
          |
     +----+----+
     |         |
     v         v
   EC2-1     EC2-2
```

### **Example use case**

A company has an older application running on EC2 instances.

The company wants to distribute traffic across multiple EC2 instances without redesigning the application.

CLB can be used for this legacy application.

### **Key points**

- Supports HTTP, HTTPS, TCP and SSL listeners.
- Performs health checks.
- Distributes traffic across registered EC2 instances.
- Instances are registered directly with CLB, rather than through target groups.
- It is a legacy load balancer.

**Interview answer:** CLB is the previous generation of AWS Elastic Load Balancing. For new applications, AWS generally recommends ALB or NLB depending on the traffic requirements.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

Elastic Load Balancing+1



## **6. Application Load Balancer (ALB)**

[🚀 Building Production-Ready Infrastructure: A Complete Guide to AWS Multi-AZ Load-Balanced Architecture. | by Osenat Alonge | Medium](https://images.openai.com/static-rsc-4/foFo8ziTO5gqCeFartXG9YKcDr0Xooy_D44J-3CCVEllgVUqh0vylzj8f1U4g-cltq1aU0Oiov8yj6rtZQm0OJo5QG78XOG3lvrkEW2URTM60fz1-0NuY4Wt_Ro7pei1-rEkYBsmc_DDzTfM-KsR0q9_nNGNnYGU8VCfDDtgdpU?purpose=inline)

[medium.com](https://medium.com/%40osenat.alonge/building-production-ready-infrastructure-a-complete-guide-to-aws-multi-az-load-balanced-c5e62de256ef?utm_source=chatgpt.com)

### **What is ALB?**

Application Load Balancer works at **Layer 7 (Application Layer)** of the OSI model.

It understands application-level traffic such as HTTP and HTTPS.

ALB can route requests based on:

- URL path
- Hostname
- HTTP headers
- Query strings
- Source IP address

### **Problem statement — E-commerce application**

An e-commerce company has three application services:

- Product service
- Payment service
- Order service

The company wants to run all three services behind one Load Balancer.

### **Solution: ALB path-based routing**

```
                 Customer
                    |
                    v
              Application LB
                    |
       +------------+------------+
       |            |            |
       v            v            v
   /products     /payments     /orders
       |            |            |
       v            v            v
 Product TG     Payment TG    Order TG
       |            |            |
    EC2-1         EC2-2        EC2-3
```

How ALB routes traffic

| Customer URL        | Target          |
| ------------------- | --------------- |
| `shop.com/products` | Product service |
| `shop.com/payments` | Payment service |
| `shop.com/orders`   | Order service   |

### **ALB components**

- **Listener:** Checks incoming connection requests on a configured protocol and port, such as HTTP port 80 or HTTPS port 443.
- **Listener rule:** Defines how requests should be routed.
- **Target group:** Contains registered backend targets such as EC2 instances, IP addresses, or containers.
- **Health check:** Checks whether backend targets are healthy.

### **ALB benefits**

- Path-based routing
- Host-based routing
- HTTP and HTTPS support
- WebSocket support
- Integration with AWS WAF
- Supports microservices and container applications

### **When to use ALB?**

Use ALB when you are hosting:

- E-commerce websites
- Web applications
- REST APIs
- Microservices
- HTTP/HTTPS-based applications

**Interview answer:** ALB is a Layer 7 Load Balancer used for HTTP and HTTPS traffic. It supports content-based routing, such as path-based and host-based routing.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

Elastic Load Balancing+1



## **7. Network Load Balancer (NLB)**

[notes.kodekloud.com](https://notes.kodekloud.com/docs/AWS-Solutions-Architect-Associate-Certification/Services-Networking/Load-Balancers/page?utm_source=chatgpt.com)

### **What is NLB?**

Network Load Balancer works at **Layer 4 (Transport Layer)**.

It distributes traffic based on network connection information, such as IP addresses and ports.

NLB supports:

- TCP
- UDP
- TLS
- QUIC

### **Problem statement — Banking application**

A banking company runs a high-traffic transaction application.

The application requires:

- Very high performance
- Low latency
- TCP-based communication
- Ability to handle large numbers of connections

The company needs a Load Balancer suitable for these requirements.

### **Solution: NLB architecture**

```
               Banking Clients
                      |
                      v
               Network LB
                      |
               TCP / UDP
                      |
          +-----------+-----------+
          |                       |
          v                       v
      EC2 Server 1           EC2 Server 2
      Transaction             Transaction
      Service                Service
```

### **NLB features**

- Operates at Layer 4.
- Handles TCP and UDP traffic.
- Supports static IP addresses per enabled AZ.
- Supports very high connection rates and low latency.
- Can preserve the client source IP in supported configurations.
- Supports targets across multiple AZs.

### **When to use NLB?**

Use NLB for:

- Banking transaction systems
- TCP-based applications
- Gaming servers
- IoT applications
- Applications requiring static IP addresses
- High-performance network workloads

**Interview answer:** NLB is a Layer 4 Load Balancer designed for TCP, UDP, TLS and other supported transport-level traffic. It is suitable for high-performance, low-latency workloads.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

Elastic Load Balancing+2



## **8. Gateway Load Balancer (GWLB)**

[Scaling network traffic inspection using AWS Gateway Load Balancer | Networking & Content Delivery](https://images.openai.com/static-rsc-4/tRu-f7OECdEMwupF5f5mJuY9UXyn-52Q_LFwmo-fLy1bHyBmbxoT-XMRiXIgX2JoyFUVvvR6vmIid58-tYfCsIVEIfDp8XWH3pbi9lZh15jvhkAXapS635mRk2FnJes45Bz26-AVa8ST4TvgstKS55VUpUXgqFxNinOJ-_9NoKc?purpose=inline)

[aws.amazon.com](https://aws.amazon.com/blogs/networking-and-content-delivery/scaling-network-traffic-inspection-using-aws-gateway-load-balancer/?utm_source=chatgpt.com)

### **What is GWLB?**

Gateway Load Balancer is used to deploy, scale, and manage virtual network appliances.

It works at **Layer 3 (Network Layer)** and helps route network traffic through security appliances.

Examples of appliances:

- Firewall
- Intrusion Detection System (IDS)
- Intrusion Prevention System (IPS)
- Deep packet inspection appliance

### **Problem statement — E-commerce security**

An e-commerce company wants to inspect incoming and outgoing network traffic using a third-party firewall.

The company has multiple application servers.

The security team wants traffic to pass through the firewall before reaching the application servers.

### **Solution: GWLB architecture**

```
              Internet Traffic
                     |
                     v
                Internet
                 Gateway
                     |
                     v
              Gateway Load
                 Balancer
                     |
          +----------+----------+
          |                     |
          v                     v
      Firewall 1           Firewall 2
          |                     |
          +----------+----------+
                     |
                     v
              Application
                Servers
```

### **How GWLB works**

1. Traffic enters the network.
2. GWLB forwards traffic to a virtual security appliance.
3. The appliance inspects the traffic.
4. The appliance forwards the traffic back through GWLB.
5. Traffic continues to its destination if permitted.

GWLB uses the **GENEVE protocol on UDP port 6081** to exchange traffic with supported virtual appliances.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

Elastic Load Balancing+1



### **When to use GWLB?**

Use GWLB when you need:

- Centralized firewall inspection
- Network security appliances
- IDS/IPS deployment
- Traffic inspection across multiple applications
- Scalable third-party virtual appliances

**Interview answer:** GWLB distributes traffic across virtual network appliances such as firewalls and IDS/IPS systems. It operates at Layer 3 and uses GENEVE encapsulation to communicate with appliances.

## **9. Load Balancer comparison table**

This table is useful for your students' GitHub README and interview preparation.

| Feature                     | CLB                   | ALB              | NLB                 | GWLB                     |
| --------------------------- | --------------------- | ---------------- | ------------------- | ------------------------ |
| Full form                   | Classic LB            | Application LB   | Network LB          | Gateway LB               |
| OSI layer                   | L4 / L7               | L7               | L4                  | L3                       |
| Traffic                     | TCP, SSL, HTTP, HTTPS | HTTP, HTTPS      | TCP, UDP, TLS, QUIC | IP traffic to appliances |
| Routing                     | Basic                 | Content-based    | Connection-based    | Appliance-based          |
| Path routing                | No                    | Yes              | No                  | No                       |
| Host routing                | No                    | Yes              | No                  | No                       |
| Target groups               | No                    | Yes              | Yes                 | Yes                      |
| Main purpose                | Legacy applications   | Web applications | High performance    | Security inspection      |
| Recommended for new designs | Generally no          | Yes              | Yes                 | Yes                      |

Note: The table summarizes common use cases. Actual protocol and feature support depends on the listener, target group, and configuration.

## **10. How to choose the correct Load Balancer?**

Simple decision flow for students

Ask what kind of traffic or service you need to handle.

**What is your requirement?**

HTTP / HTTPS

Websites, APIs, microservices

ALB

TCP / UDP

High performance, low latency

NLB

Firewall / IDS / IPS

Inspect network traffic

GWLB

Existing legacy app

Older ELB architecture

CLB

## **11. Hands-on lab — Create an ALB for High Availability**

Beginner lab

### **Lab requirements**

| Resource      | Configuration             |
| ------------- | ------------------------- |
| VPC           | Default VPC or custom VPC |
| AZs           | 2                         |
| EC2 instances | 2                         |
| Web server    | Apache                    |
| Load Balancer | Application Load Balancer |
| Target group  | HTTP, port 80             |
| Health check  | `/`                       |

### **Step 1: Launch two EC2 instances**

Launch two Ubuntu EC2 instances in different Availability Zones.

Example:

- `ecommerce-web-01` → AZ-A
- `ecommerce-web-02` → AZ-B

Install Apache on both instances.

```
sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```

### **Step 2: Create different web pages**

On EC2 instance 1:

```
echo "Welcome to E-commerce Server 1" | sudo tee /var/www/html/index.html
```

On EC2 instance 2:

```
echo "Welcome to E-commerce Server 2" | sudo tee /var/www/html/index.html
```

### **Step 3: Create a Target Group**

AWS Console → EC2 → Target Groups → Create target group

Configure:

- Target type: Instances
- Protocol: HTTP
- Port: 80
- Health check path: `/`
- Register both EC2 instances

Wait until both targets show **Healthy**.

### **Step 4: Create an Application Load Balancer**

AWS Console → EC2 → Load Balancers → Create Load Balancer → Application Load Balancer

Configure:

- Scheme: Internet-facing
- IP address type: IPv4
- Select at least two AZ subnets
- Listener: HTTP port 80
- Default action: Forward to your target group

For an ALB, select subnets in at least two different AZs for a standard regional High Availability setup.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.aws.amazon.com\&sz=32)

Elastic Load Balancing



### **Step 5: Configure Security Groups**

ALB Security Group

Allow inbound:

| Type | Port | Source    |
| ---- | ---- | --------- |
| HTTP | 80   | 0.0.0.0/0 |

EC2 Security Group

Allow inbound:

| Type | Port | Source             |
| ---- | ---- | ------------------ |
| HTTP | 80   | ALB Security Group |

This ensures that web traffic reaches the EC2 instances through the Load Balancer rather than directly from the internet.

### **Step 6: Test High Availability**

1. Copy the ALB DNS name.
2. Open it in a browser.
3. Refresh the page several times.
4. You should see responses from the two backend servers.
5. Stop one EC2 instance.
6. Wait for its target health status to become unhealthy.
7. Refresh the ALB DNS name.

The website should continue responding from the healthy EC2 instance.

**Lab conclusion:** The Load Balancer distributes traffic and avoids sending requests to unhealthy registered targets. For automatic replacement of failed EC2 instances, integrate the architecture with an Auto Scaling Group.

## **12. Frequently asked interview questions**

### **Q1. What is High Availability?**

High Availability means designing an application so it continues to operate even if one or more components fail.

### **Q2. What is a Load Balancer?**

A Load Balancer distributes incoming traffic across multiple backend servers to improve availability and performance.

### **Q3. What is the difference between ALB and NLB?**

ALB works at Layer 7 and routes HTTP/HTTPS requests based on content.

NLB works at Layer 4 and distributes TCP, UDP, TLS and other supported transport traffic.

### **Q4. Which Load Balancer supports path-based routing?**

Application Load Balancer.

Example:

`/products` → Product service

`/payments` → Payment service

### **Q5. Which Load Balancer is used for firewall inspection?**

Gateway Load Balancer.

### **Q6. What is a Target Group?**

A Target Group is a collection of registered backend targets to which a Load Balancer forwards traffic.

Targets may include EC2 instances, IP addresses, or other supported target types.

### **Q7. What is a health check?**

A health check verifies whether a backend target is healthy.

For example, ALB can check:

`http://EC2-IP/`

If the target fails health checks, the Load Balancer stops routing new requests to it.

### **Q8. What is the difference between Listener and Target Group?**

- Listener receives incoming traffic on a configured port and protocol.
- Target Group contains backend targets that receive forwarded traffic.

### **Q9. Can Load Balancer distribute traffic across multiple AZs?**

Yes. Load Balancers can distribute traffic across enabled Availability Zones, improving fault tolerance.

### **Q10. Is Load Balancer alone enough for High Availability?**

Not always.

A typical HA architecture includes:

- Load Balancer
- Multiple EC2 instances
- Multiple Availability Zones
- Health checks
- Auto Scaling Group
- Highly available database or storage design

### **Final concept to explain to students**

**High Availability is the architecture goal. Load Balancer is one of the components used to achieve that goal.**

For a typical modern e-commerce website:

Customer → ALB → EC2 instances in multiple AZs → Database

For a high-performance TCP application:

Client → NLB → Backend servers

For a network security inspection architecture:

Network traffic → GWLB → Firewall appliances → Application

Official AWS references:

- [What is Elastic Load Balancing?](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html?utm_source=chatgpt.com)
- [Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html?WT.mc_id=ravikirans\&utm_source=chatgpt.com)
- [Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html?utm_source=chatgpt.com)
- [Gateway Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/?utm_source=chatgpt.com)
- [Classic Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/?utm_source=chatgpt.com)
