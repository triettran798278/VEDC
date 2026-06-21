# SmartAgri
## Hệ sinh thái Edge AI đa tác vụ cho nông nghiệp thông minh

## 1. Tầm nhìn dự án
SmartAgri là hệ thống AIoT nông nghiệp thế hệ mới, kết hợp Edge AI, Computer Vision, LoRa và Cloud Dashboard nhằm tự động giám sát, dự báo và điều khiển canh tác trong điều kiện thực tế tại Tây Nguyên.

Khác với các hệ thống tưới thông minh truyền thống chỉ dựa trên ngưỡng cảm biến, SmartAgri có khả năng:
- Dự báo nhu cầu tưới trước nhiều giờ.
- Phát hiện sớm bệnh lá bằng AI thị giác máy tính.
- Phát hiện bất thường của hệ thống tưới.
- Tự động điều khiển van, bơm và quạt.
- Hoạt động hoàn toàn offline khi mất Internet.

---

## 2. Bài toán giải quyết

### Thách thức hiện nay
- Hạn hán và thiếu nước cục bộ.
- Lãng phí nước do tưới theo lịch cố định.
- Không phát hiện sớm sâu bệnh.
- Mất kết nối Internet tại vùng sâu vùng xa.
- Thiếu công cụ giám sát tập trung.

### Mục tiêu
Xây dựng hệ thống AI nhúng có khả năng tự suy luận và ra quyết định tại thiết bị biên, giảm phụ thuộc vào Cloud và nâng cao hiệu quả sản xuất nông nghiệp.

---

## 3. Đối tượng sử dụng

- Nông hộ trồng cà phê, hồ tiêu, sầu riêng.
- Hợp tác xã nông nghiệp.
- Trang trại quy mô vừa và nhỏ.
- Trung tâm nghiên cứu nông nghiệp thông minh.

---

## 4. Chức năng cốt lõi

### 4.1 AI dự báo tưới (Predictive Irrigation)

Input:
- Độ ẩm đất
- Nhiệt độ
- Độ ẩm không khí
- Lượng mưa

Output:
- Dự báo độ ẩm tương lai
- Khuyến nghị tưới
- Điều khiển van tự động

### 4.2 AI nhận diện bệnh lá (Leaf Disease Detection)

Sử dụng camera XIAO ESP32-S3 Sense.

Phân loại:
- Healthy
- Nutrient Deficiency
- Leaf Spot
- Fungal Disease
- Critical

### 4.3 AI phát hiện bất thường (Anomaly Detection)

Phát hiện:
- Tắc đường ống
- Rò rỉ nước
- Van hỏng
- Cảm biến lỗi

### 4.4 Điều khiển tự động

Điều khiển:
- Van điện từ
- Máy bơm
- Quạt thông gió
- Hệ thống bón phân

### 4.5 Dashboard & Digital Twin

Hiển thị:
- Bản đồ khu vực canh tác
- Trạng thái từng node
- Dữ liệu thời gian thực
- Cảnh báo bệnh và lỗi hệ thống

---

## 5. Kiến trúc hệ thống

```text
                 [Camera ESP32-S3 Sense]
                           │
                           ▼
              [AI Vision - Leaf Health]
                           │
                           ▼

[Cảm biến đất] ---> [ESP32-S3 TinyML Node] <--- [Cảm biến môi trường]
                           │
                           ├── AI Dự báo tưới
                           ├── AI Dự báo bệnh
                           ├── AI Phát hiện lỗi
                           ▼

                 [Van / Bơm / Quạt]

                           │
                      (LoRa Mesh)

                           ▼

                     [Gateway]

                           ▼

                    [Cloud Dashboard]
```

---

## 6. Công nghệ sử dụng

### Phần cứng

- XIAO ESP32-S3 Sense
- ESP32-S3
- LoRa SX1276
- Cảm biến độ ẩm đất
- Cảm biến nhiệt độ độ ẩm
- Cảm biến EC
- Cảm biến lưu lượng nước
- Van điện từ
- Relay
- Máy bơm DC
- Pin năng lượng mặt trời

### AI & Embedded

- Edge Impulse
- TensorFlow Lite Micro
- TinyML
- MobileNetV2
- Quantization Int8

### IoT & Cloud

- MQTT
- Node-RED
- Adafruit IO
- InfluxDB
- Grafana

---

## 7. Điểm khác biệt

### Edge AI thực sự

Mọi quyết định quan trọng đều được xử lý trên ESP32-S3.

### Computer Vision tại biên

Nhận diện bệnh lá trực tiếp trên camera nhúng.

### Hoạt động khi mất Internet

Hệ thống vẫn tưới và cảnh báo bình thường.

### Digital Twin nông trại

Mô phỏng trạng thái toàn bộ khu vực canh tác theo thời gian thực.

### Chi phí thấp

Chi phí prototype dự kiến dưới 2 triệu VNĐ.

---

## 8. Kịch bản demo VEDC 2026

### Demo 1: Tưới tự động

Làm khô đất.

AI nhận biết độ ẩm thấp.

Van tự động mở.

### Demo 2: Phát hiện bệnh lá

Đưa lá bệnh trước camera.

AI nhận diện và gửi cảnh báo.

### Demo 3: Mất Internet

Ngắt kết nối mạng.

Hệ thống vẫn hoạt động nhờ TinyML tại biên.

### Demo 4: Phát hiện lỗi

Mô phỏng tắc đường ống.

AI phát hiện bất thường và gửi cảnh báo.

---

## 9. Giá trị mang lại

- Tiết kiệm nước.
- Giảm chi phí vận hành.
- Giảm rủi ro dịch bệnh.
- Hỗ trợ quản lý từ xa.
- Phù hợp với điều kiện Tây Nguyên.
- Dễ thương mại hóa.

---

