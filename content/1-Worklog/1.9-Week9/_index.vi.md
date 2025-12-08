---
title: "Worklog Tuần 9"
date: "2025-11-03"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

- Dự án FastAPI với MongoDB
- Thư viện STT tiếng Việt được lựa chọn và tích hợp
- Thư viện OCR tiếng Việt được lựa chọn và thử nghiệm
- Trích xuất NLP: số lượng, danh mục, ngày tháng, phát hiện jar (REQ-027)
- Phát hiện nhiều giao dịch (REQ-027)
- Xuất bản sự kiện lên RabbitMQ

### Các công việc cần triển khai trong tuần này:


| Thứ | Công việc | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập |
|---|---|---|---|---|
| 2 | **Thiết lập dự án:** Cấu trúc FastAPI, Docker, MongoDB (ai_service_db).<br>**Nghiên cứu công nghệ:** Tìm kiếm mô hình OCR (Bill) và STT (Voice) tối ưu cho tiếng Việt. | 03/11/2025 | 03/11/2025 | |
| 3 | **Xây dựng Core API:**<br>- Thiết lập Endpoints, Pydantic models.<br>- Cấu hình Middleware (CORS, Error handling) & Logging (structlog). | 04/11/2025 | 04/11/2025 | |
| 4 | **Triển khai Voice & OCR:**<br>- Voice: Cài đặt thư viện STT, tiền xử lý âm thanh.<br>- OCR: Cài đặt thư viện, nghiên cứu kỹ thuật tiền xử lý ảnh hóa đơn. | 05/11/2025 | 05/11/2025 | |
| 5 | **Tối ưu hóa:**<br>- **Voice:** Ứng dụng mô hình **PhoWhisper** (VinAI), detect giao dịch/thời gian.<br>- **OCR:** Tối ưu hóa chất lượng ảnh đầu vào, thu thập dataset hóa đơn Việt Nam. | 06/11/2025 | 06/11/2025 | |
| 6 | **Tích hợp & Kiểm thử (Integration & Testing):**<br>- Xử lý Background tasks.<br>- Test luồng E2E cho Voice (Ghi âm -> Text).<br>- Đánh giá hiệu quả các model OCR (Tesseract, EasyOCR...). | 07/11/2025 | 07/11/2025 | |



### Kết quả đạt được tuần 9:

#### 1. Thiết lập Dự án và Hạ tầng

- Hoàn thành cấu trúc dự án FastAPI với các thư mục chuẩn (/app, /models, /services, /utils, /routers, /schemas, /ai-models)
- Thiết lập môi trường Python 3.11+ với môi trường ảo
- Cài đặt và cấu hình MongoDB cục bộ sử dụng Docker
- Tạo cơ sở dữ liệu `ai_service_db` và thu thập bộ dữ liệu Bills và Voices
- Thiết lập kết nối MongoDB với MongoEngine và quản lý vòng đời kết nối

#### 2. Cấu trúc API và Middleware

- Thiết lập các API endpoint cho Voice và Bill processing
- Tạo mô hình Pydantic cho request/response validation
- Cấu hình CORS middleware và error handling middleware
- Triển khai health check endpoint (GET /health)
- Tích hợp structlog cho logging system

#### 3. Xử lý Giọng nói (Speech-to-Text)

- Nghiên cứu và lựa chọn mô hình **PhoWhisper của VinAI** cho STT tiếng Việt
- Triển khai tiền xử lý âm thanh và tích hợp Voice-to-Text
- Kiểm tra độ chính xác của mô hình và khả năng detect giọng nói
- Cấu hình endpoint trả về đúng các category đã định nghĩa
- Thử nghiệm xử lý nhiều giao dịch cùng lúc
- Thiết lập phát hiện thời gian giao dịch từ giọng nói
- Tạo đối tượng giao dịch từ dữ liệu voice

#### 4. Xử lý Hóa đơn (OCR)

- Nghiên cứu và lựa chọn thư viện OCR phù hợp (Tesseract, EasyOCR)
- Triển khai tiền xử lý ảnh để tối ưu chất lượng trước khi OCR
- Thu thập bộ dữ liệu hóa đơn Việt Nam đa dạng (điện, siêu thị, quán ăn, cửa hàng tiện lợi, cà phê)
- Thử nghiệm các mô hình OCR với hóa đơn thực tế

#### 5. Trích xuất NLP và Xử lý Dữ liệu

- Triển khai trích xuất thông tin: số lượng, danh mục, ngày tháng (REQ-027)
- Phát hiện jar detection
- Xử lý phát hiện nhiều giao dịch trong một request

#### 6. Tích hợp RabbitMQ

- Thiết lập xuất bản sự kiện lên RabbitMQ
- Xử lý các công việc nền (background tasks) cho Voice và Bill

#### 7. Testing và Quality Assurance

- Kiểm thử end-to-end cho Voice processing pipeline (Ghi âm → Xử lý → Trả Endpoint)
- Đánh giá và cải thiện độ chính xác của xử lý Voice
- Kiểm thử các mô hình OCR với dataset thực tế

**Tổng kết:** Tuần 9 đã hoàn thành đầy đủ các mục tiêu đề ra, bao gồm thiết lập hạ tầng dự án FastAPI-MongoDB, tích hợp mô hình PhoWhisper cho STT tiếng Việt, triển khai OCR cho xử lý hóa đơn, và thiết lập hệ thống event publishing với RabbitMQ. Các chức năng NLP cho trích xuất thông tin giao dịch đã được triển khai và kiểm thử thành công.
