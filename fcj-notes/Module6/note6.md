# **Module 6: Dịch vụ Cơ sở dữ liệu trên AWS**

## **I. Tổng quan & Các khái niệm CSDL (Database Concepts)**

### **1. Định nghĩa cơ bản**
*   **Database (Cơ sở dữ liệu - CSDL):** Là hệ thống các thông tin có cấu trúc hoặc bán cấu trúc, được lưu trữ trên thiết bị nhằm phục vụ nhu cầu khai thác thông tin đồng thời của nhiều người dùng hoặc ứng dụng.
*   **Session (Phiên làm việc):** Khoảng thời gian tính từ lúc bắt đầu kết nối (time start) đến lúc ngắt kết nối (time end) vào hệ thống CSDL.
*   **Mô hình chia sẻ trách nhiệm (Shared Responsibility):**
    *   **AWS:** Quản lý hạ tầng, phần cứng, hệ điều hành, cập nhật bản vá (patching) cho CSDL.
    *   **Khách hàng:** Chịu trách nhiệm về thiết kế schema (cấu trúc dữ liệu), tối ưu hóa câu lệnh truy vấn (query tuning) và logic ứng dụng.

### **2. Các thành phần trong CSDL Quan hệ (RDBMS)**
*   **Primary Key (Khóa chính):** Một hoặc nhóm cột dùng để xác định **duy nhất** một bản ghi (hàng) trong bảng. Giá trị không được trùng lặp.
*   **Foreign Key (Khóa ngoại):** Cột dùng để tạo liên kết tham chiếu đến Khóa chính của bảng khác. Giúp thiết lập mối quan hệ giữa các bảng.
    *   *Mục đích:* Giúp **chuẩn hóa dữ liệu (Normalization)**, chống trùng lặp dữ liệu và tiết kiệm dung lượng lưu trữ.

### **3. Kỹ thuật tối ưu hiệu năng**
*   **Index (Chỉ mục):**
    *   *Khái niệm:* Cấu trúc dữ liệu giúp tăng tốc độ tìm kiếm (Read).
    *   *Ưu điểm:* Định vị dữ liệu nhanh mà không cần quét toàn bộ bảng (Full scan).
    *   *Nhược điểm:* Làm **tăng chi phí ghi (Write)** và tốn thêm dung lượng lưu trữ (do phải cập nhật cả bảng và Index khi có thay đổi).
*   **Partition (Phân vùng):**
    *   *Khái niệm:* Chia một bảng lớn thành các phần nhỏ hơn.
    *   *Lợi ích:* Truy vấn chỉ cần quét trên phân vùng liên quan, giúp tăng tốc độ xử lý.
*   **Execution Plan (Kế hoạch thực thi):**
    *   *Khái niệm:* Các bước mà CSDL tính toán để thực hiện câu truy vấn (ví dụ: quyết định dùng Index hay quét bảng).
    *   *Tầm quan trọng:* Đọc hiểu Execution Plan là kỹ năng cốt lõi để tối ưu hóa câu lệnh SQL.
*   **Buffer (Bộ nhớ đệm):** Vùng lưu trữ tạm trong RAM. Dữ liệu thường dùng được lưu ở đây để truy xuất nhanh hơn so với đọc từ ổ cứng.
*   **Database Log (Nhật ký):** Ghi lại mọi thay đổi của CSDL. Dùng để khôi phục dữ liệu (Recovery) khi gặp sự cố và đồng bộ hóa giữa CSDL chính/phụ.

### **4. Phân loại Workload: OLTP vs OLAP**

| Đặc điểm | **OLTP (Online Transaction Processing)** | **OLAP (Online Analytical Processing)** |
| :--- | :--- | :--- |
| **Mục đích** | Xử lý giao dịch hàng ngày (Đặt hàng, thanh toán, ngân hàng). | Phân tích dữ liệu, báo cáo, Business Intelligence (BI). |
| **Đặc thù** | Đọc/Ghi/Update liên tục, giao dịch nhỏ, yêu cầu nhanh. | Truy vấn phức tạp trên lượng dữ liệu lịch sử cực lớn. |
| **Hướng lưu trữ** | **Row-based** (Lưu theo hàng). | **Columnar-based** (Lưu theo cột). |
| **Dịch vụ AWS** | Amazon RDS, Aurora. | Amazon Redshift. |

### **5. So sánh SQL (RDBMS) và NoSQL**

| Đặc điểm | **RDBMS (SQL)** | **NoSQL** |
| :--- | :--- | :--- |
| **Cấu trúc** | Bảng (Table), Schema cố định. | Document, Key-Value, Graph... Schema linh hoạt. |
| **Mở rộng** | Vertical Scaling (Tăng sức mạnh phần cứng). | Horizontal Scaling (Thêm máy chủ). |
| **Nguyên tắc** | **ACID** (Tính nhất quán cao). | **BASE** (Tính sẵn sàng và hiệu năng cao). |

---

## **II. Amazon RDS (Relational Database Service)**

### **1. Tổng quan**
*   Là dịch vụ CSDL quan hệ được **quản lý hoàn toàn (Managed Service)** bởi AWS.
*   **Mục tiêu:** Giúp người dùng tập trung vào tối ưu ứng dụng thay vì lo quản lý hạ tầng (OS, Patching, Backup).
*   **Các Engine hỗ trợ:** MySQL, PostgreSQL, MariaDB, Oracle, Microsoft SQL Server.

### **2. Các tính năng cốt lõi**
1.  **Automated Backups:** Tự động sao lưu dữ liệu và log. Hỗ trợ **Point-in-Time Recovery** (khôi phục tại bất kỳ thời điểm nào) trong vòng tối đa **35 ngày**.
2.  **Multi-AZ (Tính sẵn sàng cao - HA):**
    *   Tự động tạo một bản sao dự phòng (Standby) ở Availability Zone (AZ) khác.
    *   Cơ chế sao chép: **Đồng bộ (Synchronous)**.
    *   Tác dụng: Tự động **Failover** sang Standby khi Primary gặp sự cố. Dành cho môi trường Production.
3.  **Read Replicas (Tối ưu hiệu năng đọc):**
    *   Tạo ra các bản sao chỉ đọc để giảm tải cho CSDL chính.
    *   Cơ chế sao chép: **Bất đồng bộ (Asynchronous)**.
    *   Tác dụng: Phục vụ cho các tác vụ báo cáo (Reporting). Có thể thăng cấp (Promote) thành Primary DB.
4.  **Bảo mật:** Mã hóa (At rest & In transit), quản lý truy cập bằng IAM, bảo vệ bằng Security Group (giống EC2).
5.  **Scaling:** Hỗ trợ Storage Auto Scaling (tự động tăng dung lượng đĩa) và thay đổi Instance type.

---

## **III. Amazon Aurora**

### **1. Tổng quan**
*   Là CSDL quan hệ do AWS tự phát triển, tương thích hoàn toàn với **MySQL** và **PostgreSQL**.
*   **Điểm khác biệt:** Tái cấu trúc lại tầng lưu trữ (Storage layer) để tối ưu hóa cho Cloud.
*   **Hiệu năng:** Nhanh gấp 5 lần MySQL và 3 lần PostgreSQL tiêu chuẩn.

### **2. Kiến trúc đặc biệt**
*   **Shared Storage Volume:** Dữ liệu được chia sẻ chung giữa bản ghi (Writer) và bản đọc (Reader).
*   **Độ bền dữ liệu:** Dữ liệu được tự động nhân bản **6 copy trên 3 AZs**.
*   **Zero Replication Lag:** Do dùng chung storage, các bản Read Replica gần như không có độ trễ so với Writer.

### **3. Tính năng nâng cao**
*   **Aurora Serverless:** Tự động bật/tắt và co giãn theo nhu cầu thực tế.
*   **Global Database:** Một Master, nhiều Reader ở các Region khác nhau trên toàn cầu (độ trễ thấp).
*   **Backtrack:** Tua ngược dữ liệu về quá khứ cực nhanh mà không cần restore backup.
*   **Multi-Master:** Cho phép ghi dữ liệu trên nhiều node cùng lúc.

### **So sánh nhanh: RDS Multi-AZ vs Aurora**
| Tính năng | RDS Multi-AZ | Amazon Aurora |
| :--- | :--- | :--- |
| **Replica** | 1 Standby (không truy cập được). | Tối đa 15 Readers (truy cập được). |
| **Failover** | Tự động chuyển sang Standby. | Tự động thăng cấp Reader thành Writer (nhanh hơn). |
| **Chi phí** | Thấp hơn Aurora. | Cao hơn (~20%). |

---

## **IV. Amazon Redshift (Data Warehouse)**

### **1. Tổng quan**
*   Dịch vụ Kho dữ liệu (Data Warehouse) quy mô Petabyte, chuyên dùng cho **OLAP** (Phân tích, Big Data).
*   Dựa trên lõi PostgreSQL nhưng được tối ưu hóa mạnh mẽ.

### **2. Kiến trúc và Công nghệ**
*   **MPP (Massively Parallel Processing):** Xử lý song song hàng loạt.
    *   **Leader Node:** Nhận query, lên kế hoạch và tổng hợp kết quả.
    *   **Compute Nodes:** Lưu trữ dữ liệu và thực hiện tính toán song song.
*   **Columnar Storage (Lưu trữ dạng cột):**
    *   Thay vì lưu theo hàng (Row) như RDS, Redshift lưu dữ liệu theo Cột.
    *   *Lợi ích:* Cực kỳ nhanh cho các truy vấn tổng hợp (SUM, AVG, COUNT) trên lượng dữ liệu lớn vì chỉ cần đọc các cột cần thiết.

### **3. Tính năng tối ưu chi phí**
*   **Redshift Spectrum:** Cho phép chạy câu lệnh SQL truy vấn trực tiếp dữ liệu đang nằm trên **S3** mà không cần load vào Redshift.
*   **Transient Cluster:** Tạo cluster tạm thời để xử lý, sau đó xóa đi để tiết kiệm tiền.

---

## **V. Amazon ElastiCache (Caching)**

### **1. Tổng quan**
*   Dịch vụ bộ nhớ đệm (Cache) trong RAM (In-memory data store).
*   **Mục đích:** Đặt trước CSDL (như RDS) để lưu các dữ liệu thường xuyên truy cập -> Giảm tải cho DB, tăng tốc độ phản hồi lên mức micro-seconds.

### **2. Các Engines hỗ trợ**
1.  **Redis:**
    *   Đa tính năng, hỗ trợ cấu trúc dữ liệu phức tạp (Sorted sets, Lists).
    *   Có tính bền vững (Persistence), hỗ trợ Cluster mode.
    *   *Khuyên dùng* cho hầu hết các trường hợp mới.
2.  **Memcached:**
    *   Đơn giản, thuần túy lưu trữ Key-Value.
    *   Dùng cho các nhu cầu cache đơn giản, đa luồng (multi-threaded).

### **3. Lưu ý quan trọng**
*   **Trách nhiệm người dùng:** AWS quản lý hạ tầng ElastiCache, nhưng **Logic Caching** là do lập trình viên chịu trách nhiệm:
    *   Quyết định cái gì cần cache?
    *   Khi nào thì dữ liệu trong cache hết hạn (TTL)?
    *   Làm sao để đồng bộ dữ liệu giữa Cache và DB? (Cache Invalidation).

---

## **VI. Tài liệu tham khảo & Bài Lab**

### **Danh sách bài Lab thực hành**
*   **Lab 000005:** Tạo RDS, kết nối ứng dụng, thực hiện Backup & Restore.
*   **Lab 000043:** Di chuyển CSDL (Migration) dùng AWS DMS và SCT (Schema Conversion Tool).
