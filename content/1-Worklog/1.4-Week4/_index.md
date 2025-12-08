---
title: "Week 4 Worklog"
date: "2025-09-29"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

- Learn comprehensive knowledge about the diverse storage services on AWS.
- Focus deeply on the core service **Amazon S3** (Simple Storage Service), an object storage service, including its characteristics (like 11 nines durability, replication across 3 AZs), and Storage Classes.
- Learn about important features like **Lifecycle Management**, **Versioning**, and **Static Website Hosting**.
- Large-scale data migration solutions (the **Snow Family**), hybrid storage solutions connecting on-premise with the cloud (Storage Gateway), the centralized backup management service (**AWS Backup**), and the basic concepts and strategies for **Disaster Recovery (DR)**.

### Tasks to be carried out this week:

| Day | Task | Start Date | End Date | Resources & Notes |
|---|---|---|---|---|
| Mon | **Amazon S3:**<br>- Architecture (Object storage, 3 AZ, durability).<br>- **Storage Classes** & **Lifecycle Management**.<br>- Features: Static Website, CORS, Versioning.<br>- Security: Bucket Policies, ACLs, S3 Endpoints.<br>- Performance optimization & S3 Glacier. | 29/09/2025 | 29/09/2025 | [Module 04](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module4/note4.md) |
| Tue | **Snow Family:** Bulk data migration (Snowball, Snowmobile) & Edge computing.<br>**AWS Storage Gateway:** Hybrid cloud storage solutions (File, Volume, Tape Gateway) connecting On-premise to AWS. | 30/09/2025 | 30/09/2025 | [Module 04](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module4/note4.md) |
| Wed | **Disaster Recovery (DR):** RTO/RPO metrics and 4 AWS DR strategies.<br>**AWS Backup:** Centralized backup management, scheduling, and retention policies for AWS services. | 01/10/2025 | 01/10/2025 | [Module 04](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module4/note4.md) |
| Thu | **Lab 000057:** S3 Basics (Create Bucket, Upload, Host Static Website).<br>**Lab 000013:** Configure AWS Backup Plan & Notification.<br>**Lab 000014:** VM Import/Export operations. | 02/10/2025 | 02/10/2025 | [Module 04](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module4/note4.md) |
| Fri | **Lab 000024:** Storage Gateway setup & File Sharing.<br>**Lab 000025:** Deploy Amazon FSx with AWS Managed AD.<br>**Extra Study:** AWS Skill Builder (Block & Object Storage Learning Plans). | 03/10/2025 | 03/10/2025 | [Module 04](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module4/note4.md) |

### Week 4 Achievements:

- **S3 Service (Basics):** Clearly understand that **Amazon S3** is an object storage service, not block storage, operating on a WORM (Write Once, Read Many) model.
- **Lesson on Durability:** Know that S3 is designed for 11 nines (99.999999999%) of durability by automatically replicating data across 3 Availability Zones (AZs).
- **S3 Cost Optimization Techniques:** Differentiate between Storage Classes such as **S3 Standard** (frequent access), **S3 Standard-IA** (infrequent access), and **S3 Glacier** (long-term, low-cost archival, requires retrieval).
- **S3 Automation Techniques:**
    + Know how to use **Object Life Cycle Management** to automatically transition data to cheaper tiers (e.g., from Standard to Glacier) over time.
    + Understand **Trigger Events** (e.g., triggering a serverless function upon file upload).
- **S3 Security Techniques:** Differentiate between two access control mechanisms: **S3 ACL** (legacy mechanism) and **S3 Bucket Policy** (easier to define access permissions).
- **Lesson on Data Protection (S3):** Clearly understand the **Versioning** feature, which allows restoring previous versions of a file, helping to protect against accidental deletion or ransomware attacks.
- **S3 Networking Techniques:**
    + Know how to use an **S3 Endpoint** to access S3 from within a VPC over the AWS private network without needing the Internet.
    + Know how to host a **Static Website** on S3 and configure **CORS**.
- **Data Migration Service (Migration):** Recognize the **Snow Family** (Snowball, Snowmobile) as the *physical* solution for large-scale (Petabyte, Exabyte) data migration from on-premise.
- **Hybrid Storage Service:** Understand **Storage Gateway** as a hybrid storage solution, allowing on-premise applications to use protocols (NFS, SMB, iSCSI) to store data on S3/Glacier.
- **Lesson on Disaster Recovery (DR):** Understand the 2 basic concepts for designing DR: **RTO** (recovery time) and **RPO** (acceptable data loss).
- **Backup Service (Backup):** Know that **AWS Backup** is a centralized management service that helps automate backups (schedule, retention) for multiple AWS resources (EBS, RDS, EFS...).
- **Hands-on:** Understand the practical steps to create an S3 bucket, host a static website, and configure AWS Backup.