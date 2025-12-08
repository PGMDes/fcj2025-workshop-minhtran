---
title: "Week 2 Worklog"
date: "2025-09-15"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

- **Understand AWS VPC:** Grasp the basic concepts of VPC (Virtual Private Cloud) as an isolated logical network environment, including key components like Subnets (Public and Private), Route Tables, and ENI.
- **Traffic Control and Security:** Learn to configure security layers (Security Groups and NACLs) and control network traffic flow to/from the Internet (Internet Gateway and NAT Gateway).
- **Complex Network Connectivity:** Differentiate and know how to use methods for connecting VPCs (VPC Peering) and the central connection model (Transit Gateway).
- **Build a Hybrid Cloud Environment:** Learn about solutions for connecting on-premises networks with AWS, including VPN (Site-to-Site) and private connections (AWS Direct Connect).
- **Application Load Balancing:** Understand the function of Elastic Load Balancing (ELB) and differentiate between various load balancer types (ALB, NLB, CLB, GLB) to ensure high availability and scalability for applications.


### Tasks to be carried out this week:

| Day | Task | Start Date | End Date | Resources & Notes |
|---|---|---|---|---|
| Mon | - Understand **VPC** architecture & core components: Subnets, Route Table, ENI, Endpoints.<br>- Gateways: Internet Gateway, NAT Gateway.<br>- Security: Security Group, NACL, Flow Logs. | 15/09/2025 | 15/09/2025 | [Module 02](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module2/note2.md) |
| Tue | - Network connectivity: **VPC Peering**, **Transit Gateway**.<br>- Hybrid connectivity solutions: **VPN** (Site-to-Site, Client-to-Site) & **AWS Direct Connect**. | 16/09/2025 | 16/09/2025 | [Module 02](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module2/note2.md) |
| Wed | - Overview of **Elastic Load Balancing (ELB)**.<br>- Architecture & use cases for: Application (ALB), Network (NLB), Classic (CLB), and Gateway Load Balancer. | 17/09/2025 | 17/09/2025 | [Module 02](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module2/note2.md) |
| Thu | - **Lab 03:** Init VPC, configure Firewall & Site-to-Site VPN.<br>- **Lab 58:** SSM Session Manager (EC2 connection, logs, Port Forwarding).<br>- **Lab 19:** VPC Peering setup (Network ACL, Route tables, DNS). | 18/09/2025 | 18/09/2025 | [Module 02](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module2/note2.md) |
| Fri | - **Lab 20:** **Transit Gateway** configuration (multi-VPC connection, Route Tables).<br>- **Lab 10:** **Hybrid DNS** (Outbound/Inbound Endpoints, Resolver Rules).<br>- Extra study: AWS Advanced Networking Specialty. | 19/09/2025 | 19/09/2025 | [Module 02](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module2/note2.md) <br> [Research Link](https://www.amazon.com/Certified-Advanced-Networking-Official-Study/dp/1119439833) |

### Week 2 Achievements:

- **Explain** what VPC is, its role in AWS, and its core components (Subnet, Route Table, ENI).
- **Clearly differentiate** between a Public Subnet (with an Internet Gateway) and a Private Subnet (using a NAT Gateway for Internet access).
- **Compare and contrast** the two main firewall mechanisms: Security Group (stateful, applies to ENI) and NACL (stateless, applies to Subnet).
- **Present** how to privately connect from a VPC to AWS services (like S3) without going over the Internet using a VPC Endpoint.
- **Evaluate** the pros and cons of two VPC connection solutions: VPC Peering (1:1 connection, no transitive support) and Transit Gateway (hub-and-spoke model, simplifies management).
- **Describe** methods for establishing a hybrid cloud connection, including Site-to-Site VPN (over the Internet) and AWS Direct Connect (private physical connection).
- **Classify** and **select** the appropriate Elastic Load Balancer type for specific scenarios:
   + **Application Load Balancer (ALB):** For HTTP/HTTPS traffic (Layer 7), supports path-based routing.
   + **Network Load Balancer (NLB):** For TCP/TLS traffic (Layer 4), requires ultra-high performance and static IP.
   + **Gateway Load Balancer (GLB):** Used for integrating virtual appliances.
- **Identify** the necessary labs to reinforce knowledge of VPC, Peering, Transit Gateway, and related services.



