---
title: "Worklog Tuần 4"
date: "2025-09-29"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---


### Mục tiêu tuần 4:

- Tìm hiểu kiến thức toàn diện về các dịch vụ lưu trữ đa dạng trên AWS. 
- Tập trung sâu vào dịch vụ cốt lõi là **Amazon S3** (Simple Storage Service), một dịch vụ lưu trữ đối tượng, bao gồm các đặc tính (như độ bền 11 số 9, nhân bản 3 AZ), các lớp lưu trữ (Storage Classes).
- Học về các tính năng quan trọng như quản lý vòng đời **(Lifecycle Management)**, **Versioning** (lập phiên bản), và **Static Website Hosting**.
- Các giải pháp di dời dữ liệu quy mô lớn (dòng **Snow Family**), giải pháp lưu trữ hybrid kết nối on-premise với cloud (Storage Gateway), dịch vụ quản lý sao lưu tập trung (**AWS Backup**), và các khái niệm, chiến lược cơ bản về **Disaster Recovery (DR)**.

### Các công việc cần triển khai trong tuần này:



| Thứ | Công việc | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập |
|---|---|---|---|---|
| 2 | **Amazon S3:**<br>- Kiến trúc (Object storage, 3 AZ, durability).<br>- Các lớp lưu trữ (**Storage Classes**) & Quản lý vòng đời (**Lifecycle**).<br>- Tính năng: Static Website, CORS, Versioning.<br>- Bảo mật: Bucket Policy, ACL, S3 Endpoint.<br>- Tối ưu hiệu năng & S3 Glacier. | 29/09/2025 | 29/09/2025 | [Module 04](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module4/note4.md) |
| 3 | **Snow Family:** Di chuyển dữ liệu quy mô lớn (Snowball, Snowmobile) & xử lý tại biên (Edge).<br>**AWS Storage Gateway:** Giải pháp lưu trữ Hybrid (File, Volume, Tape Gateway) kết nối On-premise với AWS. | 30/09/2025 | 30/09/2025 | [Module 04](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module4/note4.md) |
| 4 | **Disaster Recovery (DR):** Các chỉ số RTO/RPO và 4 chiến lược DR trên AWS.<br>**AWS Backup:** Quản lý sao lưu tập trung, lập lịch và chính sách lưu giữ cho nhiều dịch vụ AWS. | 01/10/2025 | 01/10/2025 | [Module 04](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module4/note4.md) |
| 5 | **Lab 000057:** S3 cơ bản (Bucket, Upload, Static Website).<br>**Lab 000013:** Cấu hình AWS Backup Plan & Notification.<br>**Lab 000014:** VM Import/Export (Chuyển máy ảo lên AWS và ngược lại). | 02/10/2025 | 02/10/2025 | [Module 04](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module4/note4.md) |
| 6 | **Lab 000024:** Cấu hình Storage Gateway & File Sharing.<br>**Lab 000025:** Triển khai Amazon FSx với Managed AD.<br>**Nghiên cứu thêm:** AWS Skill Builder (Block & Object Storage Plans). | 03/10/2025 | 03/10/2025 | [Module 04](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module4/note4.md) |


### Kết quả đạt được tuần 4:

- **Dịch vụ S3 (Cơ bản):** Hiểu rõ **Amazon S3** là dịch vụ lưu trữ đối tượng (object storage), không phải lưu trữ khối, hoạt động theo mô hình WORM (Ghi 1 lần, đọc nhiều lần).
- **Bài học về Độ bền (Durability):** Nắm được S3 được thiết kế cho độ bền 11 số 9 (99.999999999%) bằng cách tự động nhân bản dữ liệu trên 3 Availability Zone (AZ).
- **Kĩ thuật Tối ưu chi phí S3:** Phân biệt được các lớp lưu trữ (Storage Classes) như **S3 Standard** (truy cập thường xuyên), **S3 Standard IA** (không thường xuyên), và **S3 Glacier** (lưu trữ dài hạn, chi phí thấp, phải retrieve).
- **Kĩ thuật Tự động hóa S3:**
    + Biết cách dùng **Object Life Cycle Management** để tự động chuyển dữ liệu xuống các lớp rẻ hơn (ví dụ: từ Standard sang Glacier) theo thời gian.
    + Hiểu về **Trigger Event** (ví dụ: kích hoạt serverless function khi upload file).
- **Kĩ thuật Bảo mật S3:** Phân biệt hai cơ chế kiểm soát truy cập: **S3 ACL** (cơ chế cũ) và **S3 Bucket Policy** (dễ dàng xác định quyền truy cập hơn).
- **Bài học về Bảo vệ Dữ liệu (S3):** Hiểu rõ tính năng **Versioning** (lập phiên bản) cho phép khôi phục lại các phiên bản cũ của file, giúp chống xóa nhầm hoặc tấn công ransomware.
- **Kĩ thuật Mạng S3:**
    + Nắm được cách dùng **S3 Endpoint** để truy cập S3 từ trong VPC qua mạng riêng của AWS mà không cần Internet.
    + Biết cách host **Static Website** trên S3 và cấu hình **CORS**.
- **Dịch vụ Di dời Dữ liệu (Migration):** Nhận biết dòng **Snow Family** (Snowball, Snowmobile) là giải pháp di dời dữ liệu *vật lý* quy mô lớn (Petabyte, Exabyte) từ on-premise.
- **Dịch vụ Lưu trữ Hybrid:** Hiểu **Storage Gateway** là giải pháp lưu trữ lai, cho phép các ứng dụng on-premise sử dụng các giao thức (NFS, SMB, iSCSI) để lưu trữ dữ liệu lên S3/Glacier.
- **Bài học về Disaster Recovery (DR):** Nắm được 2 khái niệm cơ bản để thiết kế DR là **RTO** (thời gian phục hồi) và **RPO** (lượng dữ liệu chấp nhận mất).
- **Dịch vụ Sao lưu (Backup):** Biết **AWS Backup** là dịch vụ quản lý tập trung, giúp tự động hóa việc sao lưu (schedule, retention) cho nhiều tài nguyên AWS (EBS, RDS, EFS...).
- **Thực hành:** Nắm được các bước thực hành tạo S3 bucket, host website tĩnh, và cấu hình AWS Backup.



