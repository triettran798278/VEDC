# AgriSort - Hệ thống Phân loại Nông sản Tự động bằng Edge Computer Vision

## I. Vấn đề và mục tiêu 
- **Dự án giải quyết vấn đề gì?** 
  - Khâu phân loại nông sản (cà phê, cà chua, chanh dây, v.v.) sau thu hoạch tốn quá nhiều nhân công. Việc phân loại thủ công dựa vào cảm tính của mắt người dễ dẫn đến sai sót do mỏi mệt, làm giảm giá trị xuất khẩu hoặc bán buôn của lô hàng.
- **Vấn đề này có thật sự đáng giải quyết không?** 
  - Rất đáng. Nông sản đạt chuẩn có giá cao gấp nhiều lần nông sản xô (trộn lẫn quả hỏng, sâu bệnh). Tuy nhiên, máy phân loại quang học công nghiệp hiện nay có giá từ vài trăm triệu đến cả tỷ đồng, các hợp tác xã, nhà vườn nhỏ không thể đầu tư.
- **Ai đang gặp vấn đề này?** 
  - Các hợp tác xã nông nghiệp, cơ sở thu mua nông sản quy mô vừa và nhỏ, và các nhà vườn tự chủ đóng gói.
- **Hiện tại họ đang giải quyết bằng cách nào?** 
  - Thuê hàng chục nhân công ngồi hai bên băng chuyền để nhặt quả hỏng bằng tay, hoặc chấp nhận bán giá thấp cho thương lái vì chưa được phân loại kỹ.
- **Mục tiêu cuối cùng của dự án là gì?** 
  - Chế tạo một hệ thống băng chuyền phân loại mini, sử dụng công nghệ **Edge AI (Thị giác máy tính tại biên)** được nhúng trên vi điều khiển chi phí cực thấp, có khả năng nhận diện và phân tách nông sản hỏng/sâu bệnh một cách tự động.

## II. Người dùng và nhu cầu 
- **Người dùng chính là ai?** 
  - Chủ cơ sở thu mua nông sản, quản lý hợp tác xã nông nghiệp.
- **Người dùng cần chức năng gì nhất?** 
  - Một cỗ máy "cắm điện là chạy", thả nông sản vào là máy tự động gạt quả hỏng ra rổ riêng. Cần đếm được tổng số lượng quả tốt/quả hỏng để quản lý sản lượng.
- **Họ có sẵn sàng thay đổi thói quen để dùng sản phẩm không?** 
  - Hoàn toàn sẵn sàng nếu chi phí của máy chỉ bằng 1-2 tháng lương của nhân công nhặt tay và thao tác vận hành chỉ qua 1 nút bấm (Start/Stop).

## III. Giải pháp đề xuất 
- **Giải pháp của team là gì?** 
  - Xây dựng một băng chuyền mini. Nông sản di chuyển trên băng chuyền sẽ đi qua một "buồng chụp ảnh". Tại đây, Camera gắn với vi điều khiển ESP32-S3 liên tục chụp ảnh. Mô hình AI phân loại hình ảnh (Image Classification) chạy **trực tiếp trên chip** sẽ quyết định quả đang chạy qua là "Đạt" hay "Lỗi". Nếu là quả "Lỗi", chip ra lệnh cho một động cơ Servo gạt quả đó ra khay phế phẩm.
- **Nó là hệ thống hay dịch vụ?** 
  - Đây là một **Hệ thống Cơ - Điện tử AIoT (Mechatronics + Edge AI + IoT)**.
- **Điểm khác biệt của giải pháp là gì?** 
  - Thay vì gửi ảnh lên Cloud (bị trễ, tốn băng thông) hay dùng máy tính công nghiệp/Raspberry Pi (đắt tiền, tốn điện), hệ thống đưa mô hình Deep Learning xuống chạy hoàn toàn offline trên chip vi điều khiển giá chỉ ~200k VNĐ.
- **Vì sao giải pháp này tốt hơn cách hiện tại?** 
  - Chính xác, không biết mệt mỏi như con người. Chi phí phần cứng rẻ hơn gấp hàng chục lần so với máy móc quang học công nghiệp.

## IV. Phạm vi dự án 
- **Phạm vi giai đoạn thi VEDC:** 
  - Thiết kế và gia công một băng chuyền mini dài khoảng 50-80cm (mica/nhựa in 3D). Huấn luyện AI chuyên biệt cho **một loại nông sản duy nhất** (Ví dụ: Cà chua bi - Phân loại Xanh/Chín/Héo, hoặc Hạt cà phê - Phân loại hạt đen/hạt đỏ). Có Dashboard hiển thị đếm số lượng trực tuyến.
- **Chưa làm trong giai đoạn này:** 
  - Hệ thống đa luồng phân loại tốc độ siêu cao hàng tấn/giờ (do giới hạn về cơ khí).

## V. Chức năng chính 
- **Các chức năng cốt lõi:** 
  - (1) Băng chuyền cuộn tốc độ ổn định. 
  - (2) Thu nhận hình ảnh qua Camera. 
  - (3) Xử lý AI tại biên để ra nhãn phân loại. 
  - (4) Điều khiển cơ cấu gạt (Servo). 
  - (5) Thống kê số lượng đẩy lên Cloud Dashboard.
- **Mỗi chức năng cần input gì và tạo output gì?** 
  - *Camera & AI:* Input là khung hình pixel -> Output là Nhãn (Ví dụ: 90% Lỗi).
  - *Cơ cấu gạt:* Input là Tín hiệu lỗi từ AI -> Output là Góc quay Servo hất quả ra ngoài.
- **Chức năng nào dễ làm trước để có bản chạy được?** 
  - Huấn luyện mô hình AI phân loại ảnh và test độ chính xác trên máy tính trước, sau đó nhúng xuống chip ESP32 để bật tắt đèn LED báo hiệu (chưa cần ráp vào băng chuyền cơ khí).

## VI. Công nghệ và tài nguyên 
- **Dùng công nghệ gì?** 
  - Vi điều khiển: **XIAO ESP32S3 Sense** (siêu nhỏ gọn, có sẵn camera OV2640 và hỗ trợ AI Vector instructions).
  - Nền tảng huấn luyện AI: **Edge Impulse** (giúp thu thập ảnh, dán nhãn, train và đóng gói thành thư viện C++ một cách nhanh chóng).
  - Cơ khí & Điện tử: Động cơ giảm tốc DC cho băng chuyền, Servo MG996R, mạch cầu H L298N.
  - IoT Dashboard: MQTT kết nối lên Adafruit IO hoặc Node-RED.
- **Có công nghệ nào rủi ro quá cao không?** 
  - Việc nhận diện ảnh đang chạy trên băng chuyền có thể bị nhòe (Motion Blur).
  - *Phương án giảm rủi ro:* Chỉnh tốc độ băng chuyền chậm lại cho phù hợp với số khung hình/giây (FPS) của ESP32-S3 (khoảng 2-4 FPS).

## VII. Dữ liệu 
- **Dữ liệu lấy từ đâu?** 
  - Tuyệt đối **không nên** lấy ảnh có sẵn trên mạng vì môi trường, nền, góc chụp sẽ khác hoàn toàn thực tế. Phải dựng xong khung băng chuyền, đặt quả thật lên và quay video lại, sau đó cắt từng frame (khung hình) để tạo tập dataset (khoảng 300 - 500 ảnh mỗi loại).
- **Dữ liệu có đủ để train AI không?** 
  - Với kỹ thuật **Transfer Learning** (Học chuyển giao) như MobileNetV2 trên Edge Impulse, tập dữ liệu nhỏ vài trăm ảnh kèm với Data Augmentation (xoay, lật, chỉnh màu) là hoàn toàn đủ sức tạo ra độ chính xác >90%.

## VIII. Kiến trúc hệ thống 
```text
[Phễu cấp liệu] ──(Nông sản rơi xuống)──► [Băng chuyền] 
                                            │
           (Hộp đen chắn sáng) ◄────────────┤
                                            ▼
                                  [XIAO ESP32-S3 Sense] (Chụp ảnh)
                                            │ (Chạy TinyML Inference nội bộ)
                                            ▼
[Khay Lỗi] ◄──(Gạt)── [Động cơ Servo] ◄── [Quyết định Đạt/Lỗi] 
                                            │
[Khay Đạt] ◄──(Đi tiếp)─────────────────────┤
                                            │ (MQTT Wi-Fi)
                                            ▼
                              [Cloud Dashboard thống kê sản lượng]
```

## IX. Rủi ro và phương án dự phòng 
- **Phần nào dễ lỗi nhất?** 
  - Ánh sáng môi trường thay đổi (trời nắng/mưa, bật/tắt đèn phòng) sẽ làm độ sáng bức ảnh thay đổi, khiến AI nhận diện sai lệch hoàn toàn.
  - *Biện pháp (Rất quan trọng):* Xây một cái "hộp tối" che kín khu vực đặt Camera trên băng chuyền. Bên trong hộp gắn dải đèn LED trắng chiếu sáng với cường độ cố định. AI sẽ luôn hoạt động trong điều kiện ánh sáng môi trường lý tưởng nhất, loại bỏ hoàn toàn nhiễu từ bên ngoài.

## X. Kịch bản Demo tại Bàn (Dành riêng cho cuộc thi VEDC) - [Mới]
*Khác với các dự án tĩnh, dự án này ăn điểm tuyệt đối ở khâu trình diễn trực tiếp:*
1. Chuẩn bị 2 rổ quả cà chua bi (hoặc quả nhựa đồ chơi xốp tròn), pha trộn giữa quả xanh và quả đỏ.
2. Ban giám khảo tự tay đổ rổ quả lên băng chuyền.
3. Băng chuyền chuyển động, màn hình máy tính (kết nối UART) hiển thị log quá trình suy luận.
4. Mỗi khi quả xanh chạy qua hộp tối, càng gạt tự động bật ra "phầm phập", gạt chính xác quả xanh sang một khay riêng. Quả đỏ đi thẳng.
5. Màn hình Dashboard trên điện thoại nảy số liệu đếm: Tổng số 20 quả, 15 Đạt, 5 Lỗi.
=> **Kết quả:** Thuyết phục tuyệt đối về khả năng "System Integration" (Kết hợp Cơ khí - Nhúng - AI - IoT) của nhóm.
