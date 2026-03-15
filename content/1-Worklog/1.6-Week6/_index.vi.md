---
title: "Worklog Tuần 6"
date: "2025-10-13"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

- Ôn tập các khái niệm cơ sở dữ liệu (CSDL) nền tảng, bao gồm RDBMS (khóa chính, khóa ngoại), các kỹ thuật tối ưu (Index, Partition), và các khái niệm về vận hành (Database Log, Buffer).
- Phân biệt rõ hai loại hệ thống CSDL chính: **OLTP** (Online Transaction Processing - xử lý giao dịch) và **OLAP** (Online Analytical Processing - xử lý phân tích hay Kho dữ liệu).
- Hiểu rõ dịch vụ CSDL quan hệ được quản lý **Amazon RDS**, bao gồm các tính năng cốt lõi như **Multi-AZ** (cho tính sẵn sàng cao) và **Read Replicas** (cho hiệu năng đọc).
- Tìm hiểu về **Amazon Aurora**, dịch vụ CSDL cloud-native của AWS, với kiến trúc lưu trữ chia sẻ độc đáo, hiệu năng cao và các tính năng vượt trội như **Zero Replication Lag**.
- Tìm hiểu về **Amazon Redshift**, dịch vụ kho dữ liệu (Data Warehouse) quy mô petabyte, được thiết kế cho OLAP, và hiểu rõ kiến trúc **MPP** cùng kỹ thuật **Columnar Storage**.
- Hiểu về vai trò của **Amazon ElastiCache** (Redis, Memcached) như một lớp bộ nhớ đệm (caching) tốc độ cao để giảm tải cho CSDL chính.


### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập |
|---|---|---|---|---|
| 2 | **Database Concepts:**<br>- Kiến trúc RDBMS (PK, FK, Normalization) & Tối ưu hóa (Index, Partition, Execution Plan).<br>- Phân biệt **RDBMS (ACID)** vs **NoSQL (BASE)**.<br>- Phân loại hệ thống: **OLTP** (Giao dịch) vs **OLAP** (Phân tích). | 13/10/2025 | 13/10/2025 | [Module 06](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module6/note6.md) |
| 3 | **Amazon RDS:**<br>- Dịch vụ quản lý, Automated Backups (Point-in-Time Recovery).<br>- **Multi-AZ:** Đồng bộ, High Availability, Auto Failover.<br>- **Read Replicas:** Bất đồng bộ, Tối ưu hiệu năng đọc. | 14/10/2025 | 14/10/2025 | [Module 06](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module6/note6.md) |
| 4 | **Amazon Aurora:**<br>- Kiến trúc lưu trữ: Shared Volume, 6 bản sao/3 AZ, Zero Replication Lag.<br>- Cấu trúc Cluster: 1 Writer + tối đa 15 Readers.<br>- Tính năng nâng cao: Backtrack, Global Database. | 15/10/2025 | 15/10/2025 | [Module 06](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module6/note6.md) |
| 5 | **Amazon Redshift:** Data Warehouse, kiến trúc MPP, lưu trữ dạng Cột (Columnar) tối ưu cho OLAP, Redshift Spectrum.<br>**Amazon ElastiCache:** Caching in-memory (Redis/Memcached), giảm tải cho DB chính. | 16/10/2025 | 16/10/2025 | [Module 06](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module6/note6.md) |
| 6 | **Lab 000005:** Amazon RDS cơ bản (Tạo DB, Kết nối, Backup/Restore).<br>**Lab 000043:** Migration CSDL dùng DMS và SCT (Oracle sang Aurora).<br>**Nghiên cứu thêm:** Sách *Database Internals* & *The Data Warehouse Toolkit*. | 17/10/2025 | 17/10/2025 | [Module 06](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module6/note6.md) |



### Kết quả đạt được tuần 6:

- **Bài học (Nền tảng):**
  + Phân biệt rõ ràng hai mô hình hệ thống: **OLTP** (Online Transaction Processing - xử lý giao dịch) và **OLAP** (Online Analytical Processing - xử lý phân tích, kho dữ liệu).
  + Nắm vững các kỹ thuật tối ưu CSDL cơ bản: **Index** (tăng tốc độ đọc) và **Partition** (chia nhỏ bảng).
  + Hiểu vai trò của **Database Log** (để khôi phục/đồng bộ) và **Buffer** (dùng RAM để tăng tốc).
- **Dịch vụ (RDS):**
  + Biết **Amazon RDS** là dịch vụ CSDL quan hệ (OLTP) được quản lý.
  + Phân biệt rõ 2 tính năng chính của RDS: **Multi-AZ** (dùng cho tính Sẵn sàng cao - HA) và **Read Replicas** (dùng để tăng hiệu năng đọc).
- **Kĩ thuật (Replication):**
  + Phân biệt **Synchronous Replication** (Sao chép đồng bộ - dùng cho RDS Multi-AZ) và **Asynchronous Replication** (Sao chép bất đồng bộ - dùng cho RDS Read Replicas, có thể bị trễ).
- **Dịch vụ (Aurora):**
  + Biết **Amazon Aurora** là CSDL hiệu năng cao, cloud-native.
  + Hiểu kiến trúc **lưu trữ chia sẻ (Cluster Volume)** của Aurora và lợi ích vượt trội là **Zero Replication Lag** (không có độ trễ).
  + Nắm được các tính năng cao cấp như **Backtrack** và **Global Database**.
- **Dịch vụ (Redshift):**
  + Biết **Amazon Redshift** là dịch vụ kho dữ liệu (OLAP).
  + Hiểu kiến trúc **MPP (Massively Parallel Processing)** (gồm Leader Node và Compute Nodes).
  + Nắm vững kỹ thuật cốt lõi của OLAP: **Columnar Storage (Lưu trữ dạng Cột)**, giúp tăng tốc các truy vấn phân tích.
- **Dịch vụ (ElastiCache):**
  + Biết **Amazon ElastiCache** (Redis/Memcached) là dịch vụ caching trong RAM.
  + Hiểu vai trò của caching là giảm tải cho CSDL chính.
  + Nhận thức được trách nhiệm phải tự viết **Caching Logic** trong ứng dụng.
- **Thực hành:**
  + Biết cách tạo và vận hành (backup/restore) một CSDL **RDS**.
  + Biết cách sử dụng dịch vụ DMS và SCT để **dịch chuyển (migrate)** CSDL từ Oracle sang Aurora.