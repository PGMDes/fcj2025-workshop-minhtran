---
title: "Worklog Tuần 3"
date: "2025-09-22"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

- Hiểu kiến thức toàn diện về các dịch vụ **máy chủ ảo (Compute VM)** trên AWS. 
- Tập trung vào dịch vụ cốt lõi là **Amazon EC2**, bao gồm cách lựa chọn cấu hình (**Instance Types**), các loại lưu trữ (**EBS, Instance Store**), và cách tự động hóa **(User data, Auto Scaling)**. 
- Tìm hiểu về các các dịch vụ liên quan như **Amazon Lightsail** (dịch vụ chi phí thấp), các giải pháp lưu trữ file chia sẻ **(EFS cho Linux và FSx cho Windows/Linux)**, và dịch vụ di dời ứng dụng **AWS MGN** để chuyển máy chủ lên AWS hoặc xây dựng **Disaster Recovery**.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập |
|---|---|---|---|---|
| 2 | **Amazon EC2:**<br>- Kiến trúc, Instance Types, AMI, Key Pair.<br>- Lưu trữ: Phân biệt **EBS** và **Instance Store**.<br>- Cấu hình: User Data, Meta Data.<br>- Quản lý: **Auto Scaling** và các tùy chọn giá (Pricing Options). | 22/09/2025 | 22/09/2025 | [Module 03](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module3/note3.md) |
| 3 | **Amazon Lightsail:** VPS chi phí thấp & kết nối VPC Peering.<br>**Amazon EFS/FSx:**<br>- EFS: File storage cho Linux (NFS).<br>- FSx: File storage cho Windows/Linux (SMB) & tính năng deduplication.<br>**AWS MGN:** Di dời máy chủ (Migration) và thiết lập Disaster Recovery (DR). | 23/09/2025 | 23/09/2025 | [Module 03](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module3/note3.md) |
| 4 | **Lab 000004:** Thao tác EC2 cơ bản (Tạo máy, Snapshot, Cài ứng dụng).<br>**Lab 000027:** Quản lý tài nguyên bằng Tag và Resource Group. | 24/09/2025 | 24/09/2025 | [Module 03](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module3/note3.md) |
| 5 | **Lab 000008:** Giám sát tài nguyên với Amazon CloudWatch (Agent, Dashboard).<br>**Lab 000006:** Triển khai Auto Scaling Group (Launch Template, Target Group, Load Balancer). | 25/09/2025 | 25/09/2025 | [Module 03](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module3/note3.md) |
| 6 | **Lab 000045:** Amazon Lightsail (Load Balancer, RDS, Migrating to EC2).<br>**Nghiên cứu thêm:** Microsoft Workloads on AWS, quản trị hệ điều hành Linux/Windows. | 26/09/2025 | 26/09/2025 | [Module 03](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module3/note3.md) <br> [Research Link](https://www.youtube.com/playlist?list=PLhr1KZpdzukdJ%7CIxuIUM7pMB7aJ2_FfTP) |


### Kết quả đạt được tuần 3:


- **Dịch vụ EC2:** Hiểu rõ **EC2** là dịch vụ máy chủ ảo cốt lõi của AWS.
- **Kĩ thuật cấu hình EC2:** Biết cách lựa chọn **Instance Type** (cấu hình CPU, RAM, Network) và sử dụng **AMI** để khởi tạo hệ điều hành cho máy chủ.
- **Kĩ thuật bảo mật EC2:** Nắm được cách dùng **Key Pair** (public/private key) để mã hóa thông tin đăng nhập, thay vì dùng mật khẩu.
- **Dịch vụ lưu trữ (Storage):** Phân biệt rõ ràng 2 loại lưu trữ đĩa chính cho EC2:
    + **EBS (Elastic Block Store):** Là ổ đĩa mạng, hoạt động độc lập, dữ liệu được replicate x3 trong 1 AZ (độ sẵn sàng 99.999%), có thể backup bằng snapshot.
    + **Instance Store:** Là ổ đĩa vật lý (NVME) tốc độ cực cao, nhưng dữ liệu là tạm thời (sẽ bị xóa khi stop EC2), thường dùng cho cache/buffer hoặc swap.
- **Kĩ thuật tự động hóa (Automation):**
    + Biết cách dùng **User Data** để chạy script 1 lần khi máy chủ khởi động (ví dụ: cài đặt web server).
    + Hiểu **Meta Data** là gì và cách dùng nó để lấy thông tin (IP, hostname) của máy chủ từ bên trong chính nó, phục vụ cho các script tự động hóa.
- **Kĩ thuật co giãn (Scaling):** Nắm vững khái niệm **EC2 Auto Scaling** để tự động tăng (scale-out) hoặc giảm (scale-in) số lượng máy chủ theo tải (ví dụ: khi ActiveConnectionCount cao hoặc thấp).
- **Kĩ thuật tối ưu chi phí (Pricing):** Nhận biết 4 mô hình giá EC2: **On-demand** (theo giờ/giây, đắt nhất), **Reserved Instance** (cam kết 1-3 năm), **Saving Plans** (cam kết 1-3 năm, linh hoạt hơn), và **Spot Instance** (giá rẻ, tận dụng tài nguyên dư nhưng có thể bị đòi lại).
- **Dịch vụ Lightsail:** Hiểu **Amazon Lightsail** là dịch vụ VM chi phí thấp, đơn giản hóa, phù hợp cho workload nhẹ, và biết cách peering nó với VPC.
- **Dịch vụ lưu trữ file (File Storage):** Phân biệt 2 dịch vụ lưu trữ file chia sẻ cho nhiều máy chủ:
    + **EFS (Elastic File System):** Dùng cho **Linux** (giao thức NFSv4), tính phí theo dung lượng sử dụng.
    + **FSx:** Dùng cho **Windows/Linux** (giao thức SMB), hỗ trợ tính năng deduplication để giảm chi phí.
- **Dịch vụ di dời (Migration):** Hiểu **AWS MGN** là dịch vụ để di dời máy chủ từ on-premise lên AWS hoặc dùng để xây dựng hệ thống **Disaster Recovery (DR)** với chi phí thấp thông qua staging area.
- **Thực hành:** Nắm được các bước thực hành cơ bản với EC2 (tạo, snapshot), triển khai một cụm Auto Scaling Group hoàn chỉnh (với Load Balancer), và làm quen với Lightsail.
