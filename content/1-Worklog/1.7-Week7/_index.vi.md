---
title: "Worklog Tuần 7"
date: "2025-10-20"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

- Học và nghiên cứu thêm những kiến thức về Cloud
- Hoàn thành các Mooc trong Skil Builder ôn chứng chỉ Certificate Cloud Practicioner

### Các công việc cần triển khai trong tuần này:


| Thứ | Công việc | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập |
|---|---|---|---|---|
| 2 | **Domain 1: Cloud Concepts**<br>- 5 tiêu chí Cloud Computing.<br>- Phân biệt Availability, Reliability, Resiliency.<br>- Scaling vs. Elasticity.<br>- **AWS Well-Architected Framework** (6 trụ cột). | 20/10/2025 | 20/10/2025 | |
| 3 | **Domain 1: Cloud Adoption & Economics**<br>- AWS Cloud Adoption Framework (CAF) & các giai đoạn.<br>- Chiến lược di chuyển (**7 R's**) & Migration Services.<br>- Cloud Economics, Pricing Models & TCO. | 21/10/2025 | 21/10/2025 | |
| 4 | **Domain 2: Security & Compliance**<br>- **Shared Responsibility Model** (Mô hình trách nhiệm chung).<br>- Quản lý truy cập: Root, IAM, Cognito, Policies.<br>- Bảo mật mạng & tài nguyên: Security Group, NACL, WAF. | 22/10/2025 | 22/10/2025 | |
| 5 | **Domain 3: Technology & Services (Part 1)**<br>- **Global Infra:** Regions, AZs, Edge Locations (CloudFront, Global Accelerator).<br>- **Compute:** EC2 (Types, Config), Containers, Serverless.<br>- **Database:** RDS, Aurora, DynamoDB, ElastiCache, Redshift & Migration tools. | 23/10/2025 | 23/10/2025 | |
| 6 | **Domain 3: Technology & Services (Part 2)**<br>- **Networking:** VPC (Core components, Security, Connectivity), DNS.<br>- **Storage:** S3, EBS, EFS, Storage Gateway, Backup.<br>- **Advanced Services:** AI/ML, Analytics, Monitoring (CloudWatch), Integration (SQS/SNS), DevOps tools, IoT. | 24/10/2025 | 24/10/2025 | |



### Kết quả đạt được tuần 7:

#### 1. Domain 1: Cloud Concepts - Lợi ích của AWS Cloud

**Điện toán đám mây cơ bản:**

- Nắm vững 5 tiêu chí của điện toán đám mây (On-demand self-service, Broad network access, Resource pooling, Rapid elasticity, Measured service)
- Hiểu rõ về hạ tầng đám mây AWS
- Phân biệt rõ các khái niệm:
  - **Availability** (Khả năng sẵn có): Hệ thống luôn hoạt động và có thể truy cập được
  - **Durability** (Khả năng chịu đựng): Dữ liệu được bảo vệ khỏi mất mát
  - **Resilience** (Khả năng phục hồi): Hệ thống có thể phục hồi nhanh sau sự cố
- Hiểu khác biệt giữa **Scaling** (Mở rộng quy mô) và **Elasticity** (Tính đàn hồi)

**AWS Well-Architected Framework:**

- Nắm vững các nguyên tắc thiết kế chung (General Design Principles)
- Hiểu rõ 6 trụ cột chính:
  1. Operational Excellence (Xuất sắc hoạt động)
  2. Security (Bảo mật)
  3. Reliability (Độ tin cậy)
  4. Performance Efficiency (Hiệu suất)
  5. Cost Optimization (Tối ưu chi phí)
  6. Sustainability (Tính bền vững)

**Di chuyển lên AWS Cloud:**

- Hiểu về **AWS Cloud Adoption Framework (CAF)** với 6 perspectives
- Nắm vững các giai đoạn chấp nhận đám mây (Cloud Adoption Stages)
- Học thuộc **7 chiến lược di chuyển (7 R's)**:
  1. Rehost (Lift and Shift)
  2. Replatform (Lift, Tinker, and Shift)
  3. Repurchase (Drop and Shop)
  4. Refactor/Re-architect
  5. Retire
  6. Retain
  7. Relocate
- Hiểu về các dịch vụ và kịch bản di chuyển

**Cloud Economics:**

- Hiểu về Total Cost of Ownership (TCO)
- Các phương pháp giảm chi phí trên AWS
- Mô hình thanh toán và giá cả của AWS

#### 2. Domain 2: Security and Compliance

**AWS Shared Responsibility Model:**

- Trách nhiệm của AWS (Security OF the Cloud)
- Trách nhiệm của khách hàng (Security IN the Cloud)
- Trách nhiệm thay đổi dựa trên loại dịch vụ (IaaS, PaaS, SaaS)

**Security, Governance & Compliance:**

- Các khái niệm bảo mật cơ bản của AWS
- Quản trị và tuân thủ trên AWS Cloud
- Các dịch vụ và công cụ bảo mật

**Access Management:**

- AWS Root User và best practices
- AWS IAM (Identity and Access Management)
- Amazon Cognito
- IAM Policies và cách hoạt động
- Least Privilege Principle

**Security Components:**

- **Security Groups**: Firewall ở tầng instance
- **Network ACLs (NACLs)**: Firewall ở tầng subnet
- **AWS WAF** (Web Application Firewall): Bảo vệ ứng dụng web

#### 3. Domain 3: Cloud Technology and Services (Phần 1)

**3.1 Deployment và Operating Methods:**

- Các phương pháp triển khai và vận hành
- Các loại Cloud: Public, Private, Hybrid
- So sánh dịch vụ Public vs Private
- Các tùy chọn kết nối

**3.2 AWS Global Infrastructure:**

- Cấu trúc hạ tầng toàn cầu AWS (Regions, Availability Zones)
- Tiện ích mở rộng khu vực (Local Zones, Wavelength Zones)
- Edge Services: CloudFront vs Global Accelerator
- Khái niệm về Availability Zones và Disaster Recovery

**3.3 AWS Compute Resources:**

- **Amazon EC2**: Các loại instance, AMI, cấu hình
- **EC2 Storage**: EBS, Instance Store
- **Containers**: ECS, EKS, Fargate
- **Serverless Computing**: AWS Lambda
- So sánh High Availability vs Scalability

**3.4 AWS Database Resources:**

- **Amazon RDS**: Managed relational database
- **Amazon Aurora**: MySQL/PostgreSQL compatible
- **Amazon DynamoDB**: NoSQL database
- **In-Memory Databases**: ElastiCache, DynamoDB Accelerator (DAX)
- **Amazon Redshift**: Data warehouse
- **Migration Services**: AWS Snow Family, AWS DMS, AWS DataSync

#### 4. Domain 3: Cloud Technology and Services (Phần 2)

**3.5 AWS Network Resources:**

- **Amazon VPC** và các thành phần cốt lõi:
  - Subnets (Public/Private)
  - Route Tables
  - Internet Gateway
  - NAT Gateway
- **VPC Security**: Security Groups, NACLs
- **VPC Gateways**: Internet Gateway, NAT Gateway, Virtual Private Gateway
- **VPC & Hybrid Connectivity**: VPN, Direct Connect
- **DNS & Routing**: Route 53

**3.6 AWS Storage Resources:**

- **Các loại lưu trữ đám mây**: Object, Block, File
- **Amazon S3**: Object storage, storage classes
- **File Storage**: EFS vs FSx
- **Block Storage**: EBS vs Instance Store
- **EBS Volume Types**: gp2, gp3, io1, io2, st1, sc1
- **AWS Storage Gateway**: Hybrid storage
- **Backup Solutions**: AWS Backup

**3.7 AI/ML và Analytics Services:**

- Cơ bản về AI/ML
- **3 cấp độ AWS ML**:
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

**3.8 Các Dịch Vụ AWS Khác:**

- **Monitoring & Observability**: CloudWatch, X-Ray, EventBridge
- **Application Integration**: SQS, SNS
- **Business & Customer Services**: Amazon Connect, SES, AWS Activate, AWS IQ
- **Developer & DevOps Tools**: CodeCommit, CodeBuild, CodeDeploy, CodePipeline
- **End-User Computing**: AppStream 2.0, WorkSpaces, WorkSpaces Web
- **Frontend & Mobile**: AWS Amplify, AWS AppSync
- **IoT Services**: AWS IoT Core, AWS IoT Greengrass

**Tổng kết:** Tuần 7 đã hoàn thành việc học tập toàn diện về 3 domains chính cho chứng chỉ AWS Cloud Practitioner. Nắm vững các khái niệm cloud computing cơ bản, hiểu rõ về bảo mật và tuân thủ trên AWS, cũng như làm quen với hầu hết các dịch vụ AWS quan trọng. Đã có nền tảng kiến thức vững chắc để chuẩn bị cho kỳ thi chứng chỉ.
