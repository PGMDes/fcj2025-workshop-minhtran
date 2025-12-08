---
title: "Worklog Tuần 10"
date: "2025-11-10"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

- Cải tiến và tối ưu hóa mô hình OCR cho nhiều loại hóa đơn
- Nâng cao chất lượng xử lý Voice với số tiếng Việt và cụm từ ghép
- Triển khai hệ thống Confidence Scoring cho cả Voice và Bill
- Phát hiện danh mục thông minh và nhận dạng ngữ cảnh
- Xử lý lỗi toàn diện và tối ưu hiệu suất
- Kiểm thử đa chiều với các trường hợp edge cases

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập |
|---|---|---|---|---|
| 2 | **Cloud Mastery Series #2.**<br>**Cải tiến OCR:** Trích xuất chi tiết mục hàng (line items) ra JSON, đếm số lượng.<br>**Cải tiến Voice:** Chuẩn hóa số tiếng Việt (text normalization), xử lý nhiễu và lỗi chính tả. | 10/11/2025 | 10/11/2025 | |
| 3 | **Đánh giá độ tin cậy (Confidence Scoring):**<br>- **OCR:** Tính điểm cho từng trường (giá, ngày), ngưỡng tin cậy thấp.<br>- **Voice:** Điểm tin cậy đa lớp, kiểm tra hiệu suất (<4s).<br>- Kiểm thử hệ thống diện rộng. | 11/11/2025 | 11/11/2025 | |
| 4 | **Tính năng nâng cao & Tích hợp:**<br>- **Voice:** Phát hiện danh mục thông minh & ngữ cảnh.<br>- **OCR:** Mở rộng hỗ trợ các loại hóa đơn (siêu thị, nhà hàng, cafe).<br>- **Backend:** Tích hợp giao dịch, chuẩn hóa JSON output. | 12/11/2025 | 12/11/2025 | |
| 5 | **Xử lý lỗi & Tối ưu hóa (Error Handling):**<br>- Xử lý file hỏng, timeout, logic thử lại (Retry logic).<br>- Quản lý ngoại lệ (Edge cases): Âm thanh tĩnh, sai ngôn ngữ, file quá lớn.<br>- Cơ chế Graceful Degradation (trả về kết quả một phần thay vì lỗi hoàn toàn). | 13/11/2025 | 13/11/2025 | |
| 6 | **Kiểm thử toàn diện & Tài liệu:**<br>- Kiểm tra API Voice/Bill.<br>- Test các trường hợp khó: Voice (nhiễu, tốc độ nói), Bill (ảnh xoay, mờ, phức tạp).<br>- Hoàn thiện tài liệu dự án. | 14/11/2025 | 14/11/2025 | |



### Kết quả đạt được tuần 10:

#### 1. Cải Tiến Mô Hình OCR

- Phát hiện và trích xuất mục hàng đúng định dạng JSON
- Trích xuất đa mục hàng hóa trong một hóa đơn
- Tính toán số lượng các thành phần trong hóa đơn tự động
- Kiểm thử thành công với nhiều loại hóa đơn: siêu thị, nhà hàng, cà phê, quán nước
- Xây dựng quy tắc trích xuất theo từng loại hóa đơn cụ thể
- Cải thiện format JSON response cho endpoint Bill

#### 2. Nâng Cao Chất Lượng Voice Processing

- Xử lý số tiếng Việt (chuyển "hai mươi hai" → "22")
- Nhận dạng các cụm từ ghép tiếng Việt
- Sửa lỗi chính tả và xử lý nhiễu âm thanh
- Cải tiến định dạng phản hồi JSON
- Tối ưu hóa hiệu suất xử lý Voice

#### 3. Hệ Thống Confidence Scoring

**OCR Confidence:**

- Tính toán độ tin cậy cấp trường (Field-level Confidence)
- Độ tin cậy cho Số tiền/Tổng
- Độ tin cậy cho Ngày tháng
- Đánh giá độ rõ nét văn bản và phân tách dòng
- Phát hiện căn chỉnh giá và số lượng
- Xây dựng thuật toán độ tin cậy tổng thể
- Thiết lập Low Confidence Threshold
- Kiểm thử trên hơn 30 hóa đơn thực tế

**Voice Confidence:**

- Triển khai điểm số tin cậy nhiều lớp (Multi-layer Confidence Scoring)
- Thuật toán độ tin cậy tổng thể cho Voice
- Thiết lập Low Confidence Thresholds
- Kiểm tra hiệu suất trên hơn 50 mẫu (thời gian xử lý <4 giây)

#### 4. Phát Hiện Danh Mục Thông Minh

- Phân tích tên người bán/merchant
- Trích xuất keyword dựa vào danh mục
- Xác định ngữ cảnh giao dịch
- Phát hiện danh mục nâng cao (Advanced Category Detection)

#### 5. Error Handling & Resilience

**Xử lý Lỗi Âm Thanh:**

- Xác thực định dạng âm thanh (WAV, MP3, M4A)
- Kiểm tra thời lượng (min: 0.5s, max: 30s)
- Phát hiện tệp bị hỏng/không đầy đủ
- Xử lý timeout STT (max: 30s)
- Logic retry với exponential backoff (3 lần, 1s-2s-4s)

**Xử lý Trường Hợp Ngoại Lệ:**

- Âm thanh trống/im lặng → Error: "Không phát hiện giọng nói"
- Giọng nói không phải tiếng Việt → Cảnh báo độ tin cậy thấp
- Nhiều người nói → Cảnh báo + trích xuất nỗ lực tốt nhất
- Âm thanh quá dài (>30s) → Error: "Âm thanh quá dài"

**Graceful Degradation:**

- Danh mục không phát hiện được → Trả về "Chưa phân loại"
- Số lượng không trích xuất được → Trả về null + cảnh báo
- Ngày không phát hiện → Sử dụng ngày hiện tại + cảnh báo
- Luôn trả về kết quả partial khi có thể

#### 6. Kiểm Thử Toàn Diện

**Voice Testing:**

- Kiểm tra với tiếng ồn xung quanh
- Kiểm tra tốc độ nói (nhanh/chậm)
- Kiểm tra đầu vào không hợp lệ (nói tàm phào)
- Kiểm tra đa giao dịch trong một lần ghi âm
- Kiểm tra đầu vào mơ hồ

**Bill OCR Testing:**

- Kiểm tra ảnh xoay nhiều hướng
- Kiểm tra chất lượng ảnh đa dạng
- Kiểm tra input không đúng định dạng hóa đơn
- Kiểm tra hóa đơn có độ phức tạp cao
- Kiểm tra hóa đơn nhiều mặt hàng

#### 7. Tích Hợp Backend

- Tích hợp các chức năng giao dịch với Backend
- Xử lý lỗi toàn diện
- Trả về giá trị JSON chuẩn hóa

**Tổng kết:** Tuần 10 tập trung vào việc nâng cao chất lượng và độ tin cậy của cả hai mô hình Voice và OCR. Đã triển khai thành công hệ thống confidence scoring, xử lý lỗi toàn diện, và kiểm thử đa chiều với nhiều edge cases. Hệ thống đã sẵn sàng tích hợp với Backend và xử lý các tình huống thực tế phức tạp.
