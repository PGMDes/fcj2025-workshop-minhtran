---
title: "Worklog Tuần 11"
date: "2025-11-17"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

- Phát hiện và xử lý nhiều giao dịch phức tạp
- Tích hợp hỗ trợ file PDF cho Bill OCR
- Triển khai hệ thống feedback và fine-tuning models
- Nâng cao chất lượng xử lý hình ảnh và âm thanh
- Tích hợp Backend và lưu trữ MongoDB
- Automated testing và deployment Docker
- Làm quen với AWS và các công cụ quản lý

### Các công việc cần triển khai trong tuần này:


| Thứ | Công việc | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập |
|---|---|---|---|---|
| 2 | **Nâng cao tính năng:**<br>- Phát hiện **đa giao dịch** (Multi-transaction) & phân loại hũ (jar) thông minh.<br>- Hỗ trợ xử lý và kiểm thử file **PDF** cho hóa đơn. | 17/11/2025 | 17/11/2025 | |
| 3 | **Cơ chế học tập (Feedback Loop):**<br>- Xây dựng hệ thống thu thập phản hồi người dùng cho Voice/OCR.<br>- **Fine-tune** lại mô hình dựa trên dữ liệu feedback để cải thiện độ chính xác. | 18/11/2025 | 18/11/2025 | |
| 4 | **Xử lý nâng cao (Advanced Processing):**<br>- **Bill:** Tự động xoay, khử nghiêng, phát hiện vùng quan tâm (ROI), nâng cao chất lượng ảnh.<br>- **Voice:** Giảm nhiễu nền, phát hiện giọng nói (VAD), cắt khoảng lặng. | 19/11/2025 | 19/11/2025 | |
| 5 | **Tích hợp hệ thống:**<br>- Kết nối Backend API, kiểm thử luồng tạo giao dịch tự động.<br>- Thiết lập lưu trữ MongoDB và chuẩn bị tích hợp **AWS S3**. | 20/11/2025 | 20/11/2025 | |
| 6 | **Kiểm thử & Triển khai:**<br>- Thiết lập **Automated Testing** và kiểm thử hồi quy (Regression test).<br>- Đóng gói và triển khai ứng dụng lên **Docker**. | 21/11/2025 | 21/11/2025 | |




### Kết quả đạt được tuần 11:

#### 1. Phát Hiện Nhiều Giao Dịch và Hỗ Trợ PDF
- Phân tích cú pháp đa giao dịch phức tạp
- Tinh chỉnh thuật toán phát hiện đa giao dịch
- Phát hiện phân công jar trong cụm từ
- Xử lý các loại giao dịch hỗn hợp

**Kiểm Tra Cụm Từ Phức Tạp:**
- Kiểm tra 1 giao dịch với 1 hủ
- Kiểm tra nhiều giao dịch
- Kiểm thử chuyển đổi giữa các hủ
- Kiểm thử các ngữ cảnh hỗn hợp

**Hỗ Trợ PDF:**
- Cài đặt các thư viện xử lý PDF
- Kiểm thử giao dịch với file PDF
- Tích hợp PDF vào OCR Pipeline

#### 2. Hệ Thống Phản Hồi và Học Tập
- Xử lý hệ thống feedback từ user của phần Voice
- Xử lý hệ thống feedback từ user của phần Bill
- Fine-tuning các model dựa trên feedback
- Cải thiện xử lý các cú pháp nhập vào sai
- Kiểm tra độ cải thiện của 2 mô hình Voice và Bill

#### 3. Xử Lý Hình Ảnh/Âm Thanh Nâng Cao
**Nâng Cao Chất Lượng Bill:**
- Phát hiện và đánh giá chất lượng ảnh
- Tự động xoay và nghiêng ảnh
- Phát hiện ROI (Region of Interest/Vùng quan tâm)
- Tích hợp với OCR Pipeline
- Kiểm thử với nhiều điều kiện ảnh khác nhau

**Xử Lý Tiếng Ồn Nền Voice:**
- Triển khai giảm noise (Noise Reduction)
- Phát hiện hoạt động giọng nói (Voice Activity Detection)
- Cắt phần im lặng (Silence Trimming)
- Giảm thời gian xử lý
- Tích hợp với Voice Pipeline
- Kiểm thử với nhiều môi trường âm thanh

#### 4. Tích Hợp Backend & Lưu Trữ
**Tích Hợp Backend:**
- Review Backend API endpoints
- Test AI và Backend workflow
- Xác minh mức tiêu thụ sự kiện (Event Consumption)
- Kiểm tra việc tạo giao dịch tự động
- Khắc phục sự cố tích hợp

**Tích Hợp MongoDB:**
- Thiết lập Database cho Voice và Bill
- Chuẩn bị schema cho tích hợp với S3 của Amazon
- Triển khai storage strategy

#### 5. Testing Tự Động và Deployment
- Tạo automated tests cho Voice và Bill
- Nghiệm thu và kiểm tra tất cả test cases
- Sửa lỗi phát hiện từ testing
- Kiểm tra hồi quy đầy đủ (Full Regression Testing)
- Setup Docker environment
- Deploy lên Docker container

#### 6. AWS Learning
- Hiểu AWS và các nhóm dịch vụ cơ bản (Compute, Storage, Networking, Database)
- Tạo và cấu hình AWS Free Tier account
- Làm quen với AWS Management Console
- Cài đặt và cấu hình AWS CLI (Access Key, Secret Key, Region)
- Thực hiện các thao tác cơ bản với AWS CLI
- Kết nối và làm quen với cộng đồng First Cloud Journey

**Tổng kết:** Tuần 11 đã hoàn thành việc nâng cao khả năng xử lý đa giao dịch, tích hợp hỗ trợ PDF, triển khai hệ thống feedback và fine-tuning models. Đã cải thiện đáng kể chất lượng xử lý ảnh/âm thanh với các kỹ thuật nâng cao (ROI detection, noise reduction, VAD), tích hợp thành công với Backend và MongoDB, đồng thời hoàn tất automated testing và deployment lên Docker. Bên cạnh đó, đã làm quen với AWS ecosystem và các công cụ quản lý cơ bản, chuẩn bị cho việc triển khai cloud infrastructure.

