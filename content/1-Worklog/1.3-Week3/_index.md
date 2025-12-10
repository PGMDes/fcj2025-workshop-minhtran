---
title: "Week 3 Worklog"
date: "2025-09-22"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

- Understand comprehensive knowledge of **virtual server (Compute VM)** services on AWS.
- Focus on the core service **Amazon EC2**, including configuration selection (**Instance Types**), storage types (**EBS, Instance Store**), and automation **(User data, Auto Scaling)**.
- Learn about related services such as **Amazon Lightsail** (low-cost service), shared file storage solutions **(EFS for Linux and FSx for Windows/Linux)**, and the **AWS MGN** application migration service to migrate servers to AWS or build **Disaster Recovery**.

### Tasks to be carried out this week:

| Day | Task | Start Date | End Date | Resources & Notes |
|---|---|---|---|---|
| Mon | **Amazon EC2:**<br>- Architecture, Instance Types, AMI, Key Pairs.<br>- Storage: **EBS** vs. **Instance Store**.<br>- Configuration: User Data, Meta Data.<br>- Management: **Auto Scaling** & Pricing Options. | 22/09/2025 | 22/09/2025 | [Module 03](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module3/note3.md) |
| Tue | **Amazon Lightsail:** Low-cost VPS & VPC Peering.<br>**Amazon EFS/FSx:**<br>- EFS: Network file storage for Linux (NFS).<br>- FSx: Storage for Windows/Linux (SMB) & deduplication.<br>**AWS MGN:** Server Migration & Disaster Recovery (DR) setup. | 23/09/2025 | 23/09/2025 | [Module 03](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module3/note3.md) |
| Wed | **Lab 000004:** Basic EC2 operations (Create instance, Snapshot, App install).<br>**Lab 000027:** Resource Management via Tags and Resource Groups. | 24/09/2025 | 24/09/2025 | [Module 03](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module3/note3.md) |
| Thu | **Lab 000008:** Resource Monitoring with CloudWatch (Agent, Dashboard).<br>**Lab 000006:** Deploy Auto Scaling Group (Launch Template, Target Group, Load Balancer). | 25/09/2025 | 25/09/2025 | [Module 03](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module3/note3.md) |
| Fri | **Lab 000045:** Amazon Lightsail Deep Dive (LB, RDS, Migrate to EC2).<br>**Extra Study:** Microsoft Workloads on AWS, Linux/Windows OS administration. | 26/09/2025 | 26/09/2025 | [Module 03](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module3/note3.md) <br> [Research Link](https://www.youtube.com/playlist?list=PLhr1KZpdzukdJ%7CIxuIUM7pMB7aJ2_FfTP) |

### Week 3 Achievements:

- **EC2 Service:** Clearly understand that **EC2** is the core virtual server service of AWS.
- **EC2 Configuration Techniques:** Know how to select **Instance Type** (CPU, RAM, Network configuration) and use **AMI** to provision the operating system for the server.
- **EC2 Security Techniques:** Understand how to use **Key Pair** (public/private key) to encrypt login information, instead of using passwords.
- **Storage Service (Storage):** Clearly differentiate the 2 main disk storage types for EC2:
    + **EBS (Elastic Block Store):** Is a network drive, operates independently, data is replicated 3x within 1 AZ (99.999% availability), can be backed up using snapshots.
    + **Instance Store:** Is a physical drive (NVME) with extremely high speed, but the data is temporary (will be erased when EC2 is stopped), often used for cache/buffer or swap.
- **Automation Techniques (Automation):**
    + Know how to use **User Data** to run a script once when the server boots up (e.g., install a web server).
    + Understand what **Meta Data** is and how to use it to retrieve information (IP, hostname) about the server from within itself, used for automation scripts.
- **Scaling Techniques (Scaling):** Master the concept of **EC2 Auto Scaling** to automatically increase (scale-out) or decrease (scale-in) the number of servers based on load (e.g., when ActiveConnectionCount is high or low).
- **Cost Optimization Techniques (Pricing):** Recognize the 4 EC2 pricing models: **On-demand** (per hour/second, most expensive), **Reserved Instance** (1-3 year commitment), **Saving Plans** (1-3 year commitment, more flexible), and **Spot Instance** (low price, utilizes surplus resources but can be reclaimed).
- **Lightsail Service:** Understand **Amazon Lightsail** is a low-cost, simplified VM service, suitable for light workloads, and know how to peer it with a VPC.
- **File Storage Service (File Storage):** Differentiate between the 2 shared file storage services for multiple servers:
    + **EFS (Elastic File System):** Used for **Linux** (NFSv4 protocol), charges based on storage used.
    + **FSx:** Used for **Windows/Linux** (SMB protocol), supports deduplication feature to reduce costs.
- **Migration Service (Migration):** Understand **AWS MGN** is a service to migrate servers from on-premise to AWS or to build a low-cost **Disaster Recovery (DR)** system via a staging area.
- **Hands-on:** Understand the basic hands-on steps with EC2 (create, snapshot), deploy a complete Auto Scaling Group (with Load Balancer), and get familiar with Lightsail.
