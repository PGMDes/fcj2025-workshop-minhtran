---
title: "Worklog Tuần 5"
date: "2025-10-06"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

- Tìm hiểu kiến thức nền tảng và các dịch vụ cốt lõi về bảo mật trên AWS, xoay quanh triết lý "Security is job zero".
- Bắt đầu với khái niệm cơ bản nhất là **Mô hình chia sẻ trách nhiệm (Share Responsibility Model)**. 
- Tập trung sâu vào việc quản lý định danh và quyền truy cập (**Identify and Access Management - IAM**), bao gồm các thành phần: **User**, **Group**, **Policy**, và **Role**. 
- Mở rộng tìm hiểu thêm các dịch vụ quản lý định danh ở quy mô lớn hơn như **AWS Organizations** (quản lý nhiều tài khoản), **AWS Identity Center (SSO)** (đăng nhập một lần), và **Amazon Cognito** (quản lý người dùng cho ứng dụng web/di động).
- Nắm rõ kiến thức về bảo vệ dữ liệu thông qua mã hóa với **AWS KMS** và giám sát, kiểm tra tuân thủ với **AWS Security Hub**.


### Các công việc cần triển khai trong tuần này:


| Thứ | Công việc | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập |
|---|---|---|---|---|
| 2 | **Shared Responsibility Model:** AWS bảo mật *của* Cloud, Khách hàng bảo mật *trong* Cloud.<br>**IAM:**<br>- Root Account (Best practices).<br>- IAM User, Group, Policy (Identity & Resource-based).<br>- IAM Role, Assume Role (AWS STS). | 06/10/2025 | 06/10/2025 | [Module 05](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module5/note5.md) |
| 3 | **Amazon Cognito:** User Pool (Xác thực người dùng cuối) & Identity Pool (Cấp quyền).<br>**AWS Organizations:** Quản lý đa tài khoản, OU, SCP, Consolidated Billing.<br>**AWS Identity Center (SSO):** Quản lý truy cập tập trung, Permission Sets. | 07/10/2025 | 07/10/2025 | [Module 05](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module5/note5.md) |
| 4 | **AWS KMS:** Quản lý khóa mã hóa (CMK, Data Key).<br>**AWS Security Hub:** Kiểm tra bảo mật tự động theo tiêu chuẩn.<br>**Lab 000002:** IAM cơ bản & Assume Role.<br>**Lab 000044:** IAM Role Condition & Giới hạn quyền (IP, Time). | 08/10/2025 | 08/10/2025 | [Module 05](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module5/note5.md) |
| 5 | **Lab 000048:** IAM Role cho Application (EC2).<br>**Lab 000030:** IAM Permission Boundary.<br>**Lab 000027 & 000028:** Quản lý Tag, Resource Groups và kiểm soát EC2 qua Tag. | 09/10/2025 | 09/10/2025 | [Module 05](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module5/note5.md) |
| 6 | **Lab 000018:** Cấu hình & đánh giá với AWS Security Hub.<br>**Lab 000012:** Thiết lập AWS SSO & Organizations.<br>**Lab 000033:** KMS Workshop (Mã hóa, Key Policy).<br>**Nghiên cứu thêm:** AWS Security Specialty Guide (SCS-C01). | 10/10/2025 | 10/10/2025 | [Module 05](https://github.com/PGMDes/fcj2025-workshop-minhtran/blob/main/fcj-notes/Module5/note5.md) <br> [Research Link](https://www.amazon.com/Certified-Security-Specialty-Guide-SCS-C01/dp/1260461726) |



### Kết quả đạt được tuần 5:

- **Bài học Nền tảng:** Nắm vững **Mô hình chia sẻ trách nhiệm (Share Responsibility Model)**, hiểu rõ đâu là trách nhiệm của AWS và đâu là của khách hàng.
- **Dịch vụ IAM (Cốt lõi):**
  + Phân biệt rõ ràng **Root Account** (toàn quyền, cần khóa lại) và **IAM User** (dùng hàng ngày, mặc định không có quyền).
  + Nắm vững 3 thành phần chính để cấp quyền: **IAM User** (đối tượng), **IAM Policy** (giấy phép - viết bằng JSON), và **IAM Group** (nhóm các đối tượng).
  + Hiểu rõ **IAM Role**: một cơ chế cấp quyền tạm thời (không có credentials vĩnh viễn) cho cả User và Service (như EC2).
- **Kĩ thuật IAM (Quan trọng):**
  + Biết cách một User/Service "nhận" quyền của Role thông qua kĩ thuật **Assume Role** (sử dụng dịch vụ **STS**).
  + Hiểu quy tắc đánh giá quyền: **Explicit Deny** (Deny tường minh) luôn thắng mọi quyền Allow.
- **Dịch vụ Quản lý Định danh (Identity Services):**
  + Phân biệt rõ **IAM** (quản lý người quản trị AWS) và **Amazon Cognito** (quản lý người dùng cuối của ứng dụng web/mobile).
  + Biết **Cognito User Pool** là thư mục người dùng (có thể login bằng Facebook, Google) và **Identity Pool** là nơi cấp quyền cho user đó truy cập tài nguyên AWS.
- **Dịch vụ Quản lý Đa tài khoản (Multi-Account):**
  + Hiểu **AWS Organizations** dùng để quản lý tập trung nhiều tài khoản, cho phép **Consolidated Billing** (thanh toán gộp).
  + Biết dùng **Service Control Policies (SCP)** trong Organization để *giới hạn* quyền tối đa của các tài khoản con.
  + Nắm được **AWS Identity Center (SSO)** là giải pháp đăng nhập một lần, sử dụng **Permission Set** để cấp quyền vào các tài khoản trong Organization.
- **Dịch vụ Mã hóa (Encryption):**
  + Biết **AWS KMS** là dịch vụ để tạo và quản lý khóa mã hóa.
  + Hiểu cơ chế mã hóa **Encryption at rest** và phân biệt được **CMK** (khóa chính trong KMS) với **Data Key** (khóa dùng để mã hóa dữ liệu thực tế).
- **Dịch vụ Giám sát Bảo mật (Monitoring):**
  + Biết **AWS Security Hub** là dịch vụ quét và chấm điểm bảo mật, giúp kiểm tra tuân thủ (compliance) theo các tiêu chuẩn (như **PCIDSS**).
- **Thực hành:**
  + Thực hành tạo và quản lý User, Group, Policy, Role.
  + Thực hành triển khai SSO và KMS.
  + Thực hành sử dụng các tính năng nâng cao của IAM như **Conditions** và **Permission Boundary**.