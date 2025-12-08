# Module 5: Dịch vụ Bảo Mật trên AWS (Security Services)

Triết lý cốt lõi: "Security is job zero" — Bảo mật là công việc ưu tiên hàng đầu khi sử dụng dịch vụ AWS.

---

## I. Shared Responsibility Model - Mô hình chia sẻ trách nhiệm
Khi sử dụng điện toán đám mây, bảo mật là trách nhiệm chung giữa AWS và khách hàng.

### 1. Phân chia trách nhiệm
- AWS (Security OF the Cloud): chịu trách nhiệm bảo vệ hạ tầng, phần cứng, phần mềm nền tảng, mạng và cơ sở vật chất (data centers). Các dịch vụ hạ tầng: Compute, Storage, Database, Networking.
- Khách hàng (Security IN the Cloud): chịu trách nhiệm bảo mật các nội dung và cấu hình mà họ đưa lên đám mây:
  - Cấu hình hệ thống, áp dụng best practices.
  - Bảo mật OS, firewall, mạng.
  - Quản lý định danh và quyền truy cập.
  - Mã hóa dữ liệu (client-side & server-side).

Lưu ý: AWS cung cấp công cụ hỗ trợ; trách nhiệm của khách hàng không bắt đầu từ con số 0.

### 2. Thay đổi theo loại dịch vụ
- IaaS (Infrastructure as a Service): khách hàng chịu trách nhiệm nhiều nhất (ví dụ: EC2 — quản lý OS, patching).
- PaaS (Platform as a Service): trách nhiệm chia sẻ (ví dụ: RDS — AWS quản lý OS patching, khách hàng quản lý schema/data).
- SaaS (Software as a Service): AWS chịu nhiều trách nhiệm; khách hàng quản lý dữ liệu và quyền truy cập (ví dụ: S3, DynamoDB).

Hình minh họa:  
https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_1_Share_Responsibility_Model.png

---

## II. AWS Identity and Access Management (IAM)
Quản trị định danh và quyền truy cập trong AWS.

### 1. Root Account (Tài khoản gốc)
- Tài khoản tạo đầu tiên khi đăng ký AWS, có toàn quyền (unrestricted access) tới mọi dịch vụ và thông tin thanh toán.
- Best Practices:
  - KHÔNG dùng Root cho tác vụ hàng ngày.
  - Tạo IAM User có quyền Admin cho công việc hằng ngày.
  - Bật MFA cho Root.
  - Khóa hoặc xóa Access Key của Root.
  - Chia sẻ thông tin Root chỉ khi cần, hạn chế số người biết.

### 2. IAM User & IAM Group
- IAM User: đại diện cho người dùng hoặc ứng dụng, không phải một AWS Account riêng. Mặc định không có quyền.
  - Credentials: Console password (Management Console) và Access Key/Secret Key (CLI/SDK).
- IAM Group: tập hợp IAM Users để gán quyền dễ dàng. Group không thể chứa Group khác.
- Các thực thể (principals) có thể thao tác trên AWS:
  - Root user, IAM user, IAM role, federated users, AWS services.

Hình minh họa:  
https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_2_IAM_User.png

### 3. IAM Policy
- Chính sách định nghĩa quyền (JSON).
- Phân loại:
  - Identity-based Policy: gán cho User, Group, Role.
  - Resource-based Policy: gán cho tài nguyên (ví dụ: S3 bucket policy).
- Nguyên tắc đánh giá policy:
  - Mặc định là Deny.
  - Explicit Deny luôn thắng Allow.

Hình minh họa:  
https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_3_IAM_Policy.png

### 4. IAM Role
- Role: thực thể có tập quyền cụ thể, không gắn với user cố định, không có credentials lâu dài.
- Cơ chế: assume role -> AWS STS cấp credentials tạm thời.
- Trust Policy: quy định ai/cái gì được phép assume role.
- Use cases:
  - AWS Services (ví dụ: cho EC2 truy cập S3 không cần Access Key lưu trữ).
  - Cross-account access.
  - Federated users (Google, Facebook, AD).
- Có thể áp dụng điều kiện (time/IP) để tăng bảo mật.

Hình minh họa:  
https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_5_IAM_Role_for_EC2.png

---

## III. Amazon Cognito
Dịch vụ định danh cho ứng dụng Web/Mobile, giúp quản lý user signup/signin mà không cần tự xây dựng backend xác thực.

- User Pool (Authentication):
  - Thư mục người dùng, xử lý đăng ký/đăng nhập/khôi phục mật khẩu.
  - Hỗ trợ social sign-in (Facebook, Google, Amazon) và SAML.
  - Trả về JWT (ID Token) để xác thực danh tính trong ứng dụng.
- Identity Pool (Authorization):
  - Trao đổi token từ User Pool hoặc social provider để lấy AWS temporary credentials.
  - Cho phép user truy cập trực tiếp dịch vụ AWS (ví dụ: upload lên S3) dựa trên IAM Role được cấu hình.

Hình minh họa:  
https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_9_Amazon_Cognito_User_Pool_and_Identity_Pool.png

---

## IV. AWS Organizations
Quản lý đa tài khoản tập trung.

- Chức năng: quản lý, điều hành và consolidated billing cho nhiều AWS Account.
- Organization Unit (OU): nhóm tài khoản theo phòng ban/môi trường (Dev/Prod).
- Service Control Policies (SCP):
  - Áp dụng lên OU hoặc Account.
  - Thiết lập “guardrails” — giới hạn mức quyền tối đa (deny-based policies) trên quy mô lớn.

---

## V. AWS Identity Center (trước đây AWS SSO)
Quản lý truy cập tập trung (Single Sign-On).

- Quản lý quyền truy cập vào nhiều AWS Account và ứng dụng bên ngoài với một lần đăng nhập.
- Identity Source: dùng user trong Identity Center hoặc kết nối Microsoft AD on-premise.
- Permission Set: bộ quy tắc quyền được triển khai dưới dạng IAM Roles đến tài khoản con.
- Quy trình:
  - Tạo/đồng bộ Users & Groups.
  - Tạo Permission Sets (ví dụ: Admin, ViewOnly).
  - Gán User + Permission Set cho tài khoản đích.

---

## VI. AWS Key Management Service (KMS)
Dịch vụ quản lý khóa mã hóa.

- Chức năng: tạo và quản lý encryption keys để mã hóa dữ liệu (encryption at rest).
- Tuân thủ tiêu chuẩn bảo mật FIPS 140-2.
- Các loại key:
  - CMK (Customer Master Key): key chính trong KMS, không rời khỏi KMS; dùng để mã hóa Data Key.
  - Data Key: được sinh bởi CMK, dùng để mã hóa dữ liệu lớn bên ngoài KMS.

---

## VII. AWS Security Hub
Trung tâm kiểm soát an ninh cho tài khoản AWS.

- Giám sát liên tục trạng thái bảo mật.
- Tự động kiểm tra cấu hình so với các tiêu chuẩn ngành (PCI DSS, CIS AWS Foundations Benchmark,...).
- Tổng hợp cảnh báo bảo mật từ GuardDuty, Inspector, Macie, v.v.
- Cung cấp Security Score để đánh giá tổng quan.

Hình minh họa:  
https://github.com/DazielNguyen/aws-fcj-report/blob/main/TAKE_NOTES_%26_LABS/Module_05/Image_module_05/Module_05_13_AWS_Security_Hub.png

---

## VIII. Tài liệu tham khảo & Lab thực hành

Danh sách Lab khuyến nghị:
- Lab 000002: Bắt đầu với IAM (User, Group, Role, Assume Role).
- Lab 000044: IAM Role và Condition (Switch role, giới hạn IP/Thời gian).
- Lab 000048: IAM Role cho Application (EC2 Access S3).
- Lab 000030: IAM Permission Boundary (Giới hạn quyền user).
- Lab 000027 & 000028: Quản lý tài nguyên qua Tag & Resource Groups.
- Lab 000018: Sử dụng AWS Security Hub (Kiểm tra tiêu chuẩn bảo mật).
- Lab 000012: Thiết lập AWS SSO (Identity Center) với Organization.
- Lab 000033: AWS KMS Workshop (Mã hóa dữ liệu, Key Policy).

Tài liệu nghiên cứu thêm:
- AWS Certified Security Specialty Guide (Exam SCS-C01).
- Storage Learning Plan: Block Storage & Object Storage (nâng cao về bảo mật lưu trữ).