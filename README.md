# Kho Quản lý Ý tưởng - Cuộc thi Thiết kế Điện tử Việt Nam (VEDC) 2026

Chào mừng đến với không gian làm việc của nhóm. Kho lưu trữ này chứa các ý tưởng dự án, yêu cầu kỹ thuật, khung phát triển, và các tài liệu tham khảo nhằm chuẩn bị tốt nhất cho **Cuộc thi Thiết kế Điện tử Việt Nam 2026 (VEDC 2026)** với chủ đề Hệ thống nhúng và Công nghệ AIoT.

---

## 1. Yêu cầu kỹ thuật cuộc thi VEDC 2026
Chi tiết được nêu trong file: [`yeu_cau_ky_thuat_vedc_2026.md`](./yeu_cau_ky_thuat_vedc_2026.md)
* **Thành phần:** Bắt buộc có thành phần nhúng, IoT (vi điều khiển/FPGA/GPU, cảm biến, kết nối Internet/Cloud).
* **Phần cứng:** Sử dụng các bo mạch phát triển phổ biến (ESP32, STM32, Jetson Nano...) hoặc thiết kế PCB riêng.
* **Phần mềm:** Cần có Firmware, local/cloud server, dashboard quản lý và hiển thị.
* **Tích hợp AI:** Tích hợp các mô hình AI/ML tại thiết bị biên (Edge AI) để tự động hóa, suy luận và ra quyết định nội bộ.
* **Tính hoàn thiện:** Có sản phẩm/thiết bị mẫu (prototype) hoạt động thực tế.

## 2. Khung phát triển dự án
Chi tiết định hướng được nêu trong file: [`khung_phat_trien_du_an.md`](./khung_phat_trien_du_an.md). Khung đánh giá này giúp nhóm bám sát thực tế để hoàn thiện từng ý tưởng, thông qua các bước giải quyết tuần tự:
* Phân tích vấn đề và mục tiêu.
* Đánh giá người dùng và nhu cầu thực tiễn.
* Đề xuất giải pháp và xác định phạm vi dự án.
* Lựa chọn chức năng cốt lõi và công nghệ phù hợp.
* Thu thập dữ liệu và thiết kế kiến trúc hệ thống (Edge tới Cloud).
* Phân tích rủi ro và chuẩn bị các phương án dự phòng.

---

## 3. Các ý tưởng dự án của nhóm
Nhóm đang cân nhắc 5 ý tưởng chính. Từng ý tưởng đã được phân tích theo đúng cấu trúc của Khung phát triển dự án:

### 💡 [Ý tưởng 1] Dự án Tưới tiêu thông minh (Trung)
👉 **Chi tiết:** [`trung.md`](./trung.md)
* **Vấn đề:** Hạn hán, thiếu nước cục bộ tại Tây Nguyên và nguy cơ nấm bệnh, hạ tầng mạng chập chờn.
* **Giải pháp:** Hệ thống tưới tiêu tự động, tích hợp Edge AI (TinyML trên ESP32-S3) và mạng LoRa. Hệ thống có khả năng tự suy luận, điều khiển van tưới offline và dự báo rủi ro vi khí hậu.

### 💡 [Ý tưởng 2] Thiết bị Khung xương ngoài (Exoskeleton) hỗ trợ bệnh nhân Parkinson (Toàn)
👉 **Chi tiết:** [`parkinson.md`](./parkinson.md)
* **Vấn đề:** Người bệnh Parkinson gặp khó khăn trong sinh hoạt do run rẩy, đơ cứng cơ và chậm vận động.
* **Giải pháp:** Găng tay trợ lực cơ học dạng mềm, kết hợp TinyML dự đoán ý đồ vận động và hệ thống truyền động cáp từ xa giúp bệnh nhân cử động dễ dàng, triệt tiêu run vô thức.

### 💡 [Ý tưởng 3] Dự án Phát hiện và Dự báo ngập đô thị (Vĩnh)
👉 **Chi tiết:** [`urban_flood.md`](./urban_flood.md)
* **Vấn đề:** Khó biết khu vực nào đang ngập, rủi ro ngập nặng ra sao, gây ảnh hưởng trực tiếp tới đi lại.
* **Giải pháp:** Hệ thống cảnh báo ngập qua thiết bị IoT, đo mực nước theo thời gian thực tại các trạm, hiển thị cảnh báo lên bản đồ web/app và có AI dự báo trong tương lai gần.

### 💡 [Ý tưởng 4] CareEdge - Giám sát sức khỏe thông minh (Ý)
👉 **Chi tiết:** [`ARCHITECTURE.md`](./ARCHITECTURE.md)
* **Vấn đề:** Rủi ro té ngã, bất động kéo dài hoặc thay đổi nhịp tim bất ngờ ở người cao tuổi, bệnh nhân không được phát hiện kịp thời.
* **Giải pháp:** Hệ thống AIoT theo vùng (Edge Health Node) dùng ESP32-S3 tích hợp cảm biến PPG, IMU để cảnh báo bất thường trực tiếp tại biên, kết nối qua MQTT server theo dõi thời gian thực.

### 💡 [Ý tưởng 5] AgriSort - Hệ thống phân loại nông sản bằng Edge Computer Vision (Triết)
👉 **Chi tiết:** [`phan_loai_nong_san.md`](./phan_loai_nong_san.md)
* **Vấn đề:** Phân loại nông sản sau thu hoạch tốn nhiều thời gian, chi phí nhân công và dễ xảy ra sai sót. Máy quang học công nghiệp thì quá đắt đỏ.
* **Giải pháp:** Băng chuyền phân loại tự động dùng camera và vi điều khiển (XIAO ESP32S3). Xử lý hình ảnh hoàn toàn tại biên (TinyML) để phát hiện quả lỗi và dùng động cơ gạt ra khay phế phẩm, thống kê dữ liệu lên Cloud.

---

## 4. Tài liệu tham khảo và Cảm hứng
* **Kết quả VEDC 2025:** [`kqvaovongbanket-vedc2025.md`](./kqvaovongbanket-vedc2025.md)
Tham khảo danh sách 30 đội lọt vào vòng bán kết VEDC 2025 và các tên đề tài của họ để hiểu rõ xu hướng công nghệ, mức độ hoàn thiện của đối thủ và cách thức đặt tên/chọn chủ đề sao cho hấp dẫn, bám sát AIoT.
