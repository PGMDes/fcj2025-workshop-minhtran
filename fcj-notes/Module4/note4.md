# Module 4: DỊCH VỤ LƯU TRỮ TRÊN AWS (AWS STORAGE SERVICES)

## I. AMAZON SIMPLE STORAGE SERVICE (S3)

### 1. Khái niệm & bản chất
- Định nghĩa: Amazon S3 là kho lưu trữ ở mức đối tượng (Object Storage).
- Đơn vị lưu trữ: Object (khác với block storage).
- Cơ chế ghi (WORM): Write Once Read Many.
- Cập nhật dữ liệu: Không chỉnh sửa một phần của object — phải tải lại toàn bộ object để ghi đè.

### 2. Đặc điểm kỹ thuật
- Tổng dung lượng: Không giới hạn.
- Dung lượng tối đa 1 object: 5 TB.
- Durability: 99.999999999% (11 số 9).
- Availability: 99.99% (4 số 9).
- Sao lưu: Mặc định replicate trên 3 AZ (trừ One Zone-IA).
- Giao thức: REST API (HTTP): PUT để upload, GET để download.

### 3. Cấu trúc lưu trữ (Bucket & Object)
- Bucket: nơi chứa object; tên bucket phải unique toàn cầu.
- Object Key: định danh object; S3 có cấu trúc phẳng — “thư mục” là phần của key.
- Ví dụ URL:
```
// https://mybucket.s3.amazonaws.com/images/logo.png
```
- Multipart Upload: tải lên file lớn theo nhiều phần.

### 4. Các tính năng nâng cao
- Event Trigger (Lambda): trigger khi có event (ví dụ resize ảnh).
- S3 Access Point: endpoint riêng cho từng ứng dụng/quyền.
- Static Website Hosting: host website tĩnh (SPA).
- CORS: cho phép chia sẻ tài nguyên giữa domain.
- S3 VPC Endpoint: truy cập S3 qua mạng nội bộ AWS.

### 5. Quản lý phiên bản (Versioning)
- Lưu nhiều phiên bản của cùng object.
- Xóa: đặt Delete Marker; object vẫn có thể khôi phục.
- Ghi đè: tạo Version ID mới; các phiên bản cũ được giữ.
- Lưu ý: bật Versioning tăng dung lượng lưu trữ; chỉ có thể Suspend, không thể tắt hoàn toàn.

### 6. Hiệu năng (Performance)
- Partitioning tự động theo prefix của object key.
- Best practice: dùng random/hash prefix để tránh "hot spot" (vd: /x8jq/image.jpg).

## II. CÁC LỚP LƯU TRỮ (STORAGE CLASSES) & QUẢN LÝ VÒNG ĐỜI

### 1. Các lớp lưu trữ chính
| Lớp | Đặc điểm | Trường hợp sử dụng |
|---|---|---|
| S3 Standard | Truy cập thường xuyên, độ trễ thấp | Web hosting, Mobile app, Content distribution |
| S3 Standard-IA | Ít truy cập, phí lưu trữ thấp hơn, phí truy xuất cao hơn | Backup, DR |
| S3 Intelligent-Tiering | Tự động di chuyển giữa frequent/infrequent | Dữ liệu có pattern truy cập không rõ |
| S3 One Zone-IA | Lưu 1 AZ, rẻ hơn | Dữ liệu có thể tái tạo |
| S3 Glacier | Lưu trữ dài hạn, chi phí thấp, không truy xuất tức thì | Archiving, logs |
| S3 Deep Archive | Lưu trữ rất dài hạn, chi phí thấp nhất | Lưu trữ lâu dài tuân thủ pháp luật |

### 2. Chi tiết về S3 Glacier
- Retrieval:
  - Expedited: 1–5 phút (đắt nhất)
  - Standard: 3–5 giờ
  - Bulk: 5–12 giờ (rẻ nhất)
- Vault Lock: khóa dữ liệu cho compliance.

### 3. Object Lifecycle Management
- Thiết lập rule tự động chuyển lớp hoặc xóa.
- Ví dụ: Sau 30 ngày → Standard-IA; 90 ngày → Glacier; 365 ngày → xóa.

## III. BẢO MẬT & QUYỀN TRUY CẬP (ACCESS CONTROL)

### 1. Các phương thức kiểm soát
- S3 ACL: cơ chế cũ, gắn quyền trực tiếp lên bucket/object.
- Bucket Policy: JSON policy gắn vào bucket, quản lý tập trung.
- IAM Policy: gắn quyền vào user/role/group.

### 2. Mô hình bảo mật mặc định
- Mặc định: tất cả bucket/object là private; chỉ resource owner có quyền ban đầu.

## IV. SNOW FAMILY (MIGRATE DỮ LIỆU OFFLINE)

- Dùng khi băng thông internet hạn chế.

### 1. Snowball
- Dung lượng ~80 TB.
- Quy trình: AWS ship thiết bị → copy dữ liệu → ship về AWS → import vào S3/Glacier.

### 2. Snowball Edge
- Dung lượng ~100 TB.
- Hỗ trợ compute (EC2, Lambda) tại thiết bị.

### 3. Snowmobile
- Dung lượng đến ~100 PB.
- Hình thức: xe container cho quy mô rất lớn.

## V. AWS STORAGE GATEWAY (HYBRID CLOUD)

### 1. File Gateway
- Giao thức: NFS, SMB.
- File được convert thành object lưu trên S3.

### 2. Volume Gateway
- Giao thức: iSCSI.
- Lưu dưới dạng EBS Snapshots.
- Loại:
  - Stored Volumes: dữ liệu chính ở on‑premise, backup lên AWS.
  - Cached Volumes: dữ liệu chính ở S3, cache hot data on‑premise.

### 3. Tape Gateway
- Giao thức: VTL (iSCSI).
- Thay thế hệ thống băng từ; lưu backup vào S3/Glacier/Deep Archive.

## VI. DISASTER RECOVERY (DR) & BACKUP

### 1. Chỉ số quan trọng
- RTO (Recovery Time Objective): thời gian tối đa để phục hồi.
- RPO (Recovery Point Objective): thời gian tối đa dữ liệu có thể mất.

### 2. Chiến lược DR (từ chi phí thấp đến cao)
- Backup & Restore: rẻ nhất, RTO/RPO cao.
- Pilot Light: core services ở trạng thái tối thiểu.
- Warm Standby: bản sao thu nhỏ luôn chạy, scale up khi cần.
- Multi-site Active-Active: full capacity ở nhiều site, RTO/RPO gần 0 (đắt nhất).

### 3. AWS Backup
- Dịch vụ quản lý sao lưu tập trung.
- Hỗ trợ: EC2, EBS, RDS, DynamoDB, EFS, Storage Gateway.
- Tính năng: scheduling, retention policy.

## VII. LAB & THỰC HÀNH (THAM KHẢO)
- Lab S3: tạo bucket, upload file, bật Versioning, cấu hình Static Website.
- Lab AWS Backup: tạo Backup Plan cho EC2/EBS, thử restore.
- Lab Storage Gateway: cấu hình File Gateway map ổ đĩa S3 về máy local.
- Lab Import/Export: thử nghiệm quy trình Snowball (nếu có điều kiện).