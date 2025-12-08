---
title: "Worklog Tuần 2"
date: "2025-09-15"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

- **Hiểu rõ AWS VPC:** Nắm vững khái niệm cơ bản về VPC (Virtual Private Cloud) như một môi trường mạng logic cô lập, bao gồm các thành phần chính như Subnets (Public và Private), Route Tables, và ENI.

- **Kiểm soát lưu lượng và bảo mật:** Học cách cấu hình các lớp bảo mật (Security Groups và NACLs) và kiểm soát đường đi của lưu lượng mạng ra/vào Internet (Internet Gateway và NAT Gateway).

- **Kết nối mạng phức tạp:** Phân biệt và biết cách sử dụng các phương thức kết nối giữa các VPC (VPC Peering) và mô hình kết nối trung tâm (Transit Gateway).

- **Xây dựng môi trường Hybrid Cloud:** Tìm hiểu các giải pháp kết nối mạng tại chỗ (on-premises) với AWS, bao gồm VPN (Site-to-Site) và kết nối riêng tư (AWS Direct Connect).

- **Phân phối tải ứng dụng:** Hiểu chức năng của Elastic Load Balancing (ELB) và phân biệt được các loại bộ cân bằng tải khác nhau (ALB, NLB, CLB, GLB) để đảm bảo tính sẵn sàng cao và khả năng mở rộng cho ứng dụng.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập |
|---|---|---|---|---|
| 2 | - Tìm hiểu kiến trúc **VPC** và các thành phần cốt lõi: Subnets, Route Table, ENI, Endpoints.<br>- Các cổng kết nối: Internet Gateway, NAT Gateway.<br>- Bảo mật: Security Group, NACL, Flow Logs. | 15/09/2025 | 15/09/2025 | [Module 02](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module2/note2.md) |
| 3 | - Tìm hiểu kết nối mạng: **VPC Peering**, **Transit Gateway**.<br>- Các giải pháp kết nối lai (Hybrid): **VPN** (Site-to-Site, Client-to-Site) & **AWS Direct Connect**. | 16/09/2025 | 16/09/2025 | [Module 02](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module2/note2.md) |
| 4 | - Tổng quan về **Elastic Load Balancing (ELB)**.<br>- Phân biệt kiến trúc và ứng dụng của các loại: Application (ALB), Network (NLB), Classic (CLB) và Gateway Load Balancer. | 17/09/2025 | 17/09/2025 | [Module 02](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module2/note2.md) |
| 5 | - **Lab 03:** Khởi tạo VPC, cấu hình Firewall và Site-to-Site VPN.<br>- **Lab 58:** SSM Session Manager (kết nối EC2, quản lý logs, Port Forwarding).<br>- **Lab 19:** Thiết lập VPC Peering (Network ACL, Route tables, DNS). | 18/09/2025 | 18/09/2025 | [Module 02](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module2/note2.md) |
| 6 | - **Lab 20:** Cấu hình **Transit Gateway** (kết nối đa VPC, Route Tables).<br>- **Lab 10:** **Hybrid DNS** (Outbound/Inbound Endpoints, Resolver Rules).<br>- Nghiên cứu thêm: AWS Advanced Networking Specialty. | 19/09/2025 | 19/09/2025 | [Module 02](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module2/note2.md) <br> [Research Link](https://www.amazon.com/Certified-Advanced-Networking-Official-Study/dp/1119439833) |

---

### Kết quả đạt được tuần 2:

- **Giải thích** được VPC là gì, vai trò của nó trong AWS, và các thành phần cốt lõi của nó (Subnet, Route Table, ENI).
- **Phân biệt** rõ ràng giữa Public Subnet (có Internet Gateway) và Private Subnet (sử dụng NAT Gateway để truy cập Internet).
- **So sánh và đối chiếu** hai cơ chế tường lửa chính: Security Group (stateful, áp dụng cho ENI) và NACL (stateless, áp dụng cho Subnet).
- **Trình bày** được cách thức kết nối riêng tư từ VPC đến các dịch vụ AWS (như S3) mà không cần qua Internet bằng VPC Endpoint.
- **Đánh giá** được ưu nhược điểm giữa hai giải pháp kết nối VPC: VPC Peering (kết nối 1:1, không hỗ trợ bắc cầu) và Transit Gateway (mô hình hub-and-spoke, đơn giản hóa quản lý).
- **Mô tả** được các phương thức thiết lập kết nối hybrid cloud, bao gồm VPN Site-to-Site (qua Internet) và AWS Direct Connect (kết nối vật lý riêng).
- **Phân loại** và **lựa chọn** được loại Elastic Load Balancer phù hợp cho từng kịch bản cụ thể:
   + **Application Load Balancer (ALB):** Cho lưu lượng HTTP/HTTPS (Layer 7), hỗ trợ path-based routing.
   + **Network Load Balancer (NLB):** Cho lưu lượng TCP/TLS (Layer 4), cần hiệu suất cực cao và IP tĩnh.
   + **Gateway Load Balancer (GLB):** Dùng để tích hợp các thiết bị mạng ảo (virtual appliances).
- **Xác định** được các bài thực hành (Lab) cần thiết để củng cố kiến thức đã học về VPC, Peering, Transit Gateway và các dịch vụ liên quan.