---
title: "Week 7 Worklog"
date: "2025-10-20"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

- Learn and research more about Cloud knowledge
- Complete MOOCs in Skill Builder to review for Cloud Practitioner Certificate

### Tasks to be carried out this week:

| Day | Task | Start Date | End Date | Resources & Notes |
|---|---|---|---|---|
| Mon | **Domain 1: Cloud Concepts**<br>- 5 Cloud Computing criteria.<br>- Availability vs. Reliability vs. Resiliency.<br>- Scaling vs. Elasticity.<br>- **AWS Well-Architected Framework** (6 pillars). | 20/10/2025 | 20/10/2025 | |
| Tue | **Domain 1: Cloud Adoption & Economics**<br>- AWS Cloud Adoption Framework (CAF) & Stages.<br>- Migration Strategies (**The 7 R's**) & Scenarios.<br>- Cloud Economics, Pricing & Total Cost of Ownership (TCO). | 21/10/2025 | 21/10/2025 | |
| Wed | **Domain 2: Security & Compliance**<br>- **Shared Responsibility Model**.<br>- Access Management: Root, IAM, Cognito, Policies.<br>- Security Components: Security Groups, NACL, WAF. | 22/10/2025 | 22/10/2025 | |
| Thu | **Domain 3: Technology & Services (Part 1)**<br>- **Global Infra:** Regions, AZs, Edge (CloudFront vs. Global Accelerator).<br>- **Compute:** EC2 families, Containers, Serverless computing.<br>- **Database:** RDS, Aurora, DynamoDB, Redshift & DB Migration. | 23/10/2025 | 23/10/2025 | |
| Fri | **Domain 3: Technology & Services (Part 2)**<br>- **Networking:** VPC architecture, Hybrid Connectivity, DNS.<br>- **Storage:** Object (S3), Block (EBS), File (EFS), Backup.<br>- **Other Services:** AI/ML, Analytics, Monitoring, App Integration, DevOps, IoT. | 24/10/2025 | 24/10/2025 | |

### Week 7 Achievements:

#### 1. Domain 1: Cloud Concepts - Benefits of AWS Cloud

**Cloud Computing Basics:**

- Mastered 5 characteristics of cloud computing (On-demand self-service, Broad network access, Resource pooling, Rapid elasticity, Measured service)
- Understood AWS cloud infrastructure clearly
- Distinguished concepts clearly:
  - **Availability**: System is always operational and accessible
  - **Durability**: Data is protected from loss
  - **Resilience**: System can recover quickly after incidents
- Understood the difference between **Scaling** and **Elasticity**

**AWS Well-Architected Framework:**

- Mastered General Design Principles
- Understood clearly the 6 main pillars:
  1. Operational Excellence
  2. Security
  3. Reliability
  4. Performance Efficiency
  5. Cost Optimization
  6. Sustainability

**Migration to AWS Cloud:**

- Understood **AWS Cloud Adoption Framework (CAF)** with 6 perspectives
- Mastered Cloud Adoption Stages
- Learned **7 migration strategies (7 R's)**:
  1. Rehost (Lift and Shift)
  2. Replatform (Lift, Tinker, and Shift)
  3. Repurchase (Drop and Shop)
  4. Refactor/Re-architect
  5. Retire
  6. Retain
  7. Relocate
- Understood migration services and scenarios

**Cloud Economics:**

- Understood Total Cost of Ownership (TCO)
- Cost reduction methods on AWS
- AWS billing and pricing models

#### 2. Domain 2: Security and Compliance

**AWS Shared Responsibility Model:**

- AWS responsibility (Security OF the Cloud)
- Customer responsibility (Security IN the Cloud)
- Responsibility changes based on service type (IaaS, PaaS, SaaS)

**Security, Governance & Compliance:**

- AWS basic security concepts
- Governance and compliance on AWS Cloud
- Security services and tools

**Access Management:**

- AWS Root User and best practices
- AWS IAM (Identity and Access Management)
- Amazon Cognito
- IAM Policies and how they work
- Least Privilege Principle

**Security Components:**

- **Security Groups**: Instance-level firewall
- **Network ACLs (NACLs)**: Subnet-level firewall
- **AWS WAF** (Web Application Firewall): Web application protection

#### 3. Domain 3: Cloud Technology and Services (Part 1)

**3.1 Deployment and Operating Methods:**

- Deployment and operation methods
- Cloud types: Public, Private, Hybrid
- Compare Public vs Private services
- Connectivity options

**3.2 AWS Global Infrastructure:**

- AWS global infrastructure structure (Regions, Availability Zones)
- Regional expansion utilities (Local Zones, Wavelength Zones)
- Edge Services: CloudFront vs Global Accelerator
- Concepts of Availability Zones and Disaster Recovery

**3.3 AWS Compute Resources:**

- **Amazon EC2**: Instance types, AMI, configuration
- **EC2 Storage**: EBS, Instance Store
- **Containers**: ECS, EKS, Fargate
- **Serverless Computing**: AWS Lambda
- Compare High Availability vs Scalability

**3.4 AWS Database Resources:**

- **Amazon RDS**: Managed relational database
- **Amazon Aurora**: MySQL/PostgreSQL compatible
- **Amazon DynamoDB**: NoSQL database
- **In-Memory Databases**: ElastiCache, DynamoDB Accelerator (DAX)
- **Amazon Redshift**: Data warehouse
- **Migration Services**: AWS Snow Family, AWS DMS, AWS DataSync

#### 4. Domain 3: Cloud Technology and Services (Part 2)

**3.5 AWS Network Resources:**

- **Amazon VPC** and core components:
  - Subnets (Public/Private)
  - Route Tables
  - Internet Gateway
  - NAT Gateway
- **VPC Security**: Security Groups, NACLs
- **VPC Gateways**: Internet Gateway, NAT Gateway, Virtual Private Gateway
- **VPC & Hybrid Connectivity**: VPN, Direct Connect
- **DNS & Routing**: Route 53

**3.6 AWS Storage Resources:**

- **Cloud storage types**: Object, Block, File
- **Amazon S3**: Object storage, storage classes
- **File Storage**: EFS vs FSx
- **Block Storage**: EBS vs Instance Store
- **EBS Volume Types**: gp2, gp3, io1, io2, st1, sc1
- **AWS Storage Gateway**: Hybrid storage
- **Backup Solutions**: AWS Backup

**3.7 AI/ML and Analytics Services:**

- AI/ML basics
- **3 levels of AWS ML**:
  1. AI Services (Rekognition, Comprehend, etc.)
  2. ML Services (SageMaker)
  3. ML Frameworks & Infrastructure
- **Analytics Services**:
  - Amazon Athena: Query S3 data
  - Amazon Macie: Data security
  - Amazon Redshift: Data warehouse
  - Amazon Kinesis: Real-time data streaming
  - Amazon Glue: ETL service
  - Amazon QuickSight: BI tool
  - Amazon EMR: Big data processing

**3.8 Other AWS Services:**

- **Monitoring & Observability**: CloudWatch, X-Ray, EventBridge
- **Application Integration**: SQS, SNS
- **Business & Customer Services**: Amazon Connect, SES, AWS Activate, AWS IQ
- **Developer & DevOps Tools**: CodeCommit, CodeBuild, CodeDeploy, CodePipeline
- **End-User Computing**: AppStream 2.0, WorkSpaces, WorkSpaces Web
- **Frontend & Mobile**: AWS Amplify, AWS AppSync
- **IoT Services**: AWS IoT Core, AWS IoT Greengrass

**Summary:** Week 7 completed comprehensive learning of 3 main domains for AWS Cloud Practitioner certificate. Mastered basic cloud computing concepts, understood security and compliance on AWS clearly, and became familiar with most important AWS services. Built a solid knowledge foundation to prepare for the certification exam.
