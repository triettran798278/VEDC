# Kiến Trúc Hệ Thống CareEdge

## 1. Tổng Quan Dự Án

**Tên dự án đề xuất:** CareEdge - Hệ thống giám sát sức khỏe thông minh sử dụng Edge AI và AIoT.

CareEdge là hệ thống giám sát sức khỏe theo vùng, phù hợp cho gia đình, phòng bệnh, khu chăm sóc người cao tuổi hoặc bệnh viện. Hệ thống gồm nhiều node cảm biến sử dụng ESP32-S3, kết hợp cảm biến sinh hiệu và cảm biến chuyển động. Mỗi node có khả năng xử lý dữ liệu trực tiếp tại thiết bị bằng TinyML để phát hiện sớm các dấu hiệu bất thường như té ngã, bất động kéo dài, nhịp tim bất thường hoặc mẫu chuyển động nghi ngờ co giật.

Dữ liệu quan trọng được gửi về server để theo dõi dài hạn, hiển thị dashboard, lưu lịch sử, phân tích xu hướng và quản lý thiết bị. Server cũng hỗ trợ cập nhật firmware hoặc model qua OTA, giúp hệ thống có thể cải thiện thuật toán mà không cần can thiệp thủ công từng node.

> Lưu ý định vị: hệ thống hướng tới hỗ trợ cảnh báo sớm bất thường sức khỏe, không tuyên bố chẩn đoán đột quỵ, động kinh hay các bệnh lý khác khi chưa có kiểm chứng y tế.

## 2. Mục Tiêu Và Bài Toán Thực Tiễn

### 2.1. Vấn Đề Cần Giải Quyết

- Người già, bệnh nhân hậu phẫu, bệnh nhân tim mạch hoặc người sống một mình cần được theo dõi liên tục.
- Các tình huống nguy hiểm như té ngã, bất động, co giật hoặc nhịp tim bất thường cần được phát hiện sớm.
- Hệ thống camera có thể gây lo ngại riêng tư, trong khi thiết bị y tế chuyên dụng thường đắt và khó triển khai rộng.
- Nếu toàn bộ dữ liệu thô được gửi lên server để xử lý, hệ thống sẽ phụ thuộc vào mạng và có độ trễ cao.

### 2.2. Mục Tiêu Kỹ Thuật

- Thiết kế node cảm biến nhỏ gọn, chi phí thấp, có thể đặt tại giường bệnh, phòng chăm sóc hoặc đeo trên người.
- Chạy mô hình TinyML trực tiếp trên ESP32-S3 để cảnh báo nhanh tại edge.
- Xây dựng server theo dõi nhiều node, lưu dữ liệu dài hạn và hiển thị trạng thái theo thời gian thực.
- Hỗ trợ OTA để cập nhật firmware hoặc model từ xa.
- Tạo prototype có thể demo được với phần cứng thật, dashboard thật và benchmark rõ ràng.

## 3. Kiến Trúc Tổng Thể

Kiến trúc hệ thống được chia thành 5 lớp chính:

```text
[Sensor Layer]
    |
    v
[Edge Health Node - ESP32-S3]
    |
    v
[Network / Gateway]
    |
    v
[Server & Dashboard]
    |
    v
[Alert / Monitoring / OTA Management]
```

Trong đó, **Edge Health Node** là thành phần trung tâm của dự án. Node không chỉ thu thập dữ liệu cảm biến mà còn xử lý tín hiệu, chạy TinyML, tạo cảnh báo cục bộ và đồng bộ dữ liệu về server.

## 4. Vai Trò Từng Thành Phần

### 4.1. Sensor Layer

**Vai trò:** thu thập dữ liệu sinh hiệu, vận động và môi trường làm đầu vào cho hệ thống phân tích.

Thành phần dự kiến:

| Cảm biến | Vai trò | Giai đoạn |
|---|---|---|
| PPG sensor module | Đo nhịp tim, SpO2, dạng sóng mạch | MVP |
| Accelerometer / IMU module | Đo gia tốc, tư thế, rung động, té ngã, bất động | MVP |
| ECG module | Đo tín hiệu điện tim, hỗ trợ phân tích nhịp tim nâng cao | Mở rộng |
| EMG module | Đo hoạt động cơ, hỗ trợ phát hiện co cơ bất thường | Mở rộng |
| Nhiệt độ / độ ẩm | Bổ sung ngữ cảnh môi trường | Mở rộng |
| CO2 / VOC / PM2.5 | Theo dõi chất lượng không khí trong phòng | Mở rộng |

Cảm biến ở giai đoạn MVP nên ưu tiên **PPG + IMU**, vì đây là cặp cảm biến có thể demo rõ ràng các kịch bản: nhịp tim bất thường, té ngã, bất động và vận động bất thường.

Trong MVP, các cảm biến PPG và IMU nên được dùng dưới dạng **module rời gắn lên PCB carrier** thay vì thiết kế lại toàn bộ mạch cảm biến từ đầu. Cách này giảm rủi ro phần cứng, rút ngắn thời gian debug và vẫn cho phép đội thể hiện năng lực thiết kế mạch thông qua PCB tích hợp nguồn, giao tiếp, connector, cảnh báo cục bộ và bố trí cơ khí.

### 4.2. Edge Health Node

**Vai trò:** xử lý dữ liệu trực tiếp tại thiết bị biên và đưa ra cảnh báo nhanh mà không phụ thuộc hoàn toàn vào server.

Thành phần chính:

- ESP32-S3 làm vi điều khiển trung tâm.
- Firmware đọc dữ liệu cảm biến.
- PCB carrier board để gắn module PPG, module IMU, nguồn, nút bấm, LED/buzzer và các header mở rộng.
- Bộ tiền xử lý tín hiệu.
- Module trích xuất đặc trưng.
- TinyML inference engine.
- Bộ quản lý kết nối Wi-Fi hoặc BLE.
- Bộ quản lý OTA.
- LED, buzzer hoặc màn hình nhỏ để cảnh báo cục bộ.

Nhiệm vụ chi tiết:

1. Đọc dữ liệu từ module PPG, module IMU và các cảm biến mở rộng.
2. Lọc nhiễu và chuẩn hóa tín hiệu.
3. Trích xuất đặc trưng như nhịp tim, biến thiên nhịp tim đơn giản, mức vận động, tư thế và biên độ chuyển động.
4. Chạy model TinyML hoặc thuật toán phát hiện bất thường.
5. Phân loại trạng thái người dùng: bình thường, cần chú ý, cảnh báo.
6. Gửi sự kiện và chỉ số tóm tắt về server.
7. Nhận firmware hoặc model mới qua OTA.

Trạng thái có thể phát hiện trong MVP:

- Té ngã.
- Bất động kéo dài.
- Chuyển động bất thường dạng co giật giả lập.
- Nhịp tim vượt ngưỡng.
- Mất tín hiệu cảm biến hoặc đeo sai vị trí.

### 4.3. Network / Gateway

**Vai trò:** kết nối các node với server và đảm bảo dữ liệu được truyền ổn định.

Phương án MVP:

- Mỗi node ESP32-S3 kết nối Wi-Fi và gửi dữ liệu trực tiếp về server.
- Sử dụng MQTT cho dữ liệu thời gian thực.
- Sử dụng HTTP cho cấu hình, truy vấn và OTA.
- Sử dụng WebSocket để dashboard cập nhật realtime nếu cần.

Phương án mở rộng:

- Thêm gateway nội bộ như Raspberry Pi hoặc mini PC.
- Gateway nhận dữ liệu từ nhiều node qua BLE/Wi-Fi, sau đó đồng bộ lên server.
- Gateway có thể cache dữ liệu khi mất mạng.

Dữ liệu node gửi lên server:

| Trường dữ liệu | Mô tả |
|---|---|
| `node_id` | Mã định danh node |
| `user_id` / `room_id` | Người dùng hoặc phòng gắn với node |
| `timestamp` | Thời điểm ghi nhận |
| `heart_rate` | Nhịp tim hiện tại |
| `motion_state` | Trạng thái vận động |
| `risk_level` | Mức cảnh báo |
| `event_type` | Loại sự kiện nếu có |
| `battery_level` | Mức pin |
| `firmware_version` | Phiên bản firmware đang chạy |
| `model_version` | Phiên bản model TinyML đang chạy |

### 4.4. Server

**Vai trò:** quản lý toàn bộ hệ thống, lưu dữ liệu dài hạn, hiển thị dashboard, phân tích xu hướng và cập nhật thiết bị.

Module chính:

| Module | Vai trò |
|---|---|
| API Server | Nhận dữ liệu, cung cấp API cấu hình và quản lý |
| MQTT Broker | Nhận dữ liệu realtime từ các node |
| Database | Lưu dữ liệu sinh hiệu, sự kiện, node và người dùng |
| Dashboard | Hiển thị trạng thái theo phòng, người dùng và node |
| Alert Engine | Xử lý và phát cảnh báo |
| OTA Manager | Quản lý firmware/model version và quá trình cập nhật |
| Analytics Module | Phân tích xu hướng sức khỏe dài hạn |

Chức năng server:

- Hiển thị danh sách node theo phòng hoặc khu vực.
- Theo dõi trạng thái từng người dùng.
- Xem biểu đồ nhịp tim, vận động và cảnh báo.
- Lưu lịch sử sự kiện bất thường.
- Cấu hình ngưỡng cảnh báo.
- Upload firmware hoặc model mới.
- Theo dõi version firmware/model của từng node.
- Phát hiện node mất kết nối hoặc pin yếu.

### 4.5. Alert System

**Vai trò:** đưa cảnh báo đến người chăm sóc, người nhà hoặc nhân viên y tế.

Kênh cảnh báo:

- Cảnh báo tại node bằng buzzer hoặc LED.
- Cảnh báo trên dashboard bằng màu trạng thái và popup.
- Cảnh báo qua Telegram, email, SMS hoặc Zalo nếu có thời gian tích hợp.

Mức cảnh báo:

| Mức | Ý nghĩa | Ví dụ |
|---|---|---|
| Normal | Trạng thái bình thường | Tín hiệu ổn định |
| Warning | Cần theo dõi | Nhịp tim vượt ngưỡng, pin yếu |
| Critical | Cần phản ứng nhanh | Té ngã, bất động kéo dài, chuyển động bất thường nghiêm trọng |

### 4.6. OTA Firmware / Model Update

**Vai trò:** cập nhật firmware hoặc model TinyML cho node từ xa.

Lợi ích:

- Không cần nạp code thủ công từng thiết bị.
- Có thể cải thiện model sau khi thu thêm dữ liệu.
- Có thể sửa lỗi firmware sau khi triển khai.
- Phù hợp với hệ thống nhiều node trong bệnh viện hoặc khu chăm sóc.

Luồng OTA:

1. Nhóm phát triển huấn luyện hoặc tối ưu model.
2. Đóng gói firmware hoặc model mới.
3. Upload bản cập nhật lên server.
4. Server thông báo node có bản cập nhật.
5. Node tải firmware/model mới.
6. Node kiểm tra version và checksum.
7. Node reboot và chạy bản mới.
8. Server ghi nhận trạng thái cập nhật.

## 5. Luồng Dữ Liệu Hoạt Động

### 5.1. Luồng Giám Sát Bình Thường

```text
Sensor -> ESP32-S3 -> Preprocessing -> Feature Extraction -> TinyML Inference
       -> Summary Data -> MQTT/API -> Server -> Dashboard
```

Trong chế độ bình thường, node chỉ gửi dữ liệu tóm tắt theo chu kỳ để giảm băng thông và tiết kiệm năng lượng.

### 5.2. Luồng Khi Có Sự Kiện Bất Thường

```text
Sensor -> ESP32-S3 -> TinyML detects anomaly
       -> Local Alert
       -> Event Packet + Short Data Window
       -> Server
       -> Alert Engine
       -> Dashboard / Notification
```

Khi có sự kiện bất thường, node ưu tiên cảnh báo cục bộ và gửi gói dữ liệu sự kiện về server. Gói sự kiện có thể kèm một đoạn dữ liệu ngắn trước và sau thời điểm bất thường để phục vụ phân tích sau.

### 5.3. Luồng Cập Nhật OTA

```text
Developer -> Server OTA Manager -> Version Check -> Node Download
          -> Checksum Verification -> Reboot -> Report Status
```

## 6. Công Nghệ Và Linh Kiện Đề Xuất

### 6.1. Phần Cứng

| Thành phần | Lựa chọn đề xuất | Mục đích |
|---|---|---|
| MCU | ESP32-S3 module hoặc ESP32-S3 DevKit trong giai đoạn đầu | Xử lý edge, Wi-Fi, TinyML |
| PPG module | MAX30102, MAX30105, MAX86141 | Nhịp tim, SpO2, sóng mạch |
| IMU module | MPU6050, MPU9250, ICM-20948 | Té ngã, tư thế, vận động |
| ECG | AD8232, ADS1292R | Điện tim, mở rộng |
| EMG | Module EMG analog | Co cơ, mở rộng |
| Môi trường | BME280, SHT31, SGP30, PMS5003 | Nhiệt độ, độ ẩm, chất lượng không khí |
| Cảnh báo | Buzzer, LED, OLED | Cảnh báo cục bộ |
| Nguồn | Pin Li-ion/Li-Po, mạch sạc | Prototype đeo được |

### 6.2. Định Hướng PCB Cho MVP

PCB trong MVP nên được thiết kế theo hướng **carrier board gắn module**, không thiết kế lại mạch PPG/IMU ở mức linh kiện rời.

Vai trò của PCB carrier:

- Gắn ESP32-S3 module hoặc cắm ESP32-S3 DevKit.
- Gắn module PPG qua header I2C.
- Gắn module IMU qua header I2C/SPI.
- Tích hợp nguồn pin, sạc pin, công tắc nguồn và mạch bảo vệ cơ bản.
- Tích hợp LED, buzzer, nút bấm reset/config.
- Bố trí connector mở rộng cho ECG/EMG hoặc cảm biến môi trường ở giai đoạn sau.
- Chuẩn hóa kích thước cơ khí để dễ làm vỏ và demo.

Lý do chọn hướng carrier board:

- Giảm rủi ro thiết kế analog, đặc biệt với PPG/ECG/EMG.
- Dễ thay module nếu cảm biến lỗi hoặc cần nâng cấp.
- Phù hợp tiến độ 2 tháng của nhóm 5 người.
- Vẫn thể hiện được năng lực thiết kế điện tử qua sơ đồ nguồn, giao tiếp, layout, connector và tích hợp hệ thống.

### 6.3. Firmware Và Embedded AI

- ESP-IDF hoặc Arduino framework.
- PlatformIO để quản lý build.
- C/C++ cho firmware.
- TensorFlow Lite Micro hoặc inference C/C++ tối ưu thủ công.
- MQTT client.
- OTA support.

### 6.4. Server Và Dashboard

- FastAPI hoặc Node.js cho API server.
- Mosquitto cho MQTT broker.
- PostgreSQL, SQLite hoặc InfluxDB cho database.
- React, Vue hoặc Grafana cho dashboard.
- Docker nếu cần đóng gói hệ thống.

### 6.5. EDA Và Thiết Kế Mạch

- KiCad hoặc Altium Designer cho PCB.
- EasyEDA nếu cần làm nhanh prototype.
- LTspice nếu cần mô phỏng mạch nguồn hoặc các khối analog mở rộng.

## 7. MVP Đề Xuất Cho Vòng Bán Kết

MVP nên tập trung vào phần có thể demo rõ và đo được benchmark:

- 1-2 node ESP32-S3 hoạt động thật.
- PCB carrier gắn module PPG và module IMU.
- Đọc dữ liệu PPG và IMU ổn định.
- Chạy thuật toán/TinyML phát hiện ít nhất 2 trạng thái bất thường.
- Gửi dữ liệu realtime về server.
- Dashboard hiển thị trạng thái node.
- Lưu lịch sử cảnh báo.
- Demo OTA firmware cơ bản.

Tính năng nên hoàn thiện trước:

1. Đọc nhịp tim từ PPG.
2. Đọc gia tốc 3 trục từ IMU.
3. Phát hiện té ngã.
4. Phát hiện bất động kéo dài.
5. Gửi dữ liệu qua Wi-Fi.
6. Dashboard hiển thị realtime.
7. Lưu lịch sử sự kiện.
8. OTA firmware thử nghiệm.

## 8. Benchmark Cần Đo

| Chỉ số | Mục tiêu MVP |
|---|---|
| Inference latency | Dưới 100 ms |
| Cảnh báo lên dashboard | Dưới 2 giây trong Wi-Fi nội bộ |
| Model size | Dưới 200 KB |
| Accuracy fall detection nội bộ | Trên 85% với tập test demo |
| False alarm rate | Ghi nhận và tối ưu qua test |
| Thời lượng pin prototype | 4-8 giờ tùy dung lượng pin |
| Thời gian OTA | Ghi nhận theo kích thước firmware |
| RAM/Flash usage | Báo cáo theo build firmware |

Benchmark không chỉ để chứng minh hệ thống chạy được, mà còn giúp dự án có tính kỹ thuật rõ ràng khi thuyết trình.

## 9. Roadmap Hoàn Thiện

### Giai Đoạn 1: Node Và Cảm Biến

- Kết nối ESP32-S3 với PPG và IMU.
- Đọc dữ liệu ổn định.
- Xây dựng bộ tiền xử lý cơ bản.
- Gửi dữ liệu mẫu về máy tính hoặc server.

### Giai Đoạn 2: PCB Carrier Và Tích Hợp Phần Cứng

- Thiết kế schematic PCB carrier cho ESP32-S3, module PPG, module IMU, nguồn, LED/buzzer và nút bấm.
- Thiết kế layout ưu tiên dễ hàn, dễ debug và dễ thay module.
- Đặt header mở rộng cho ECG/EMG hoặc cảm biến môi trường, nhưng chưa bắt buộc tích hợp trong MVP.
- Kiểm tra nguồn, giao tiếp I2C/SPI và độ ổn định khi chạy bằng pin.

### Giai Đoạn 3: TinyML Và Thuật Toán Cảnh Báo

- Thu dữ liệu mẫu cho té ngã, bất động, vận động bình thường và vận động bất thường giả lập.
- Huấn luyện model nhỏ hoặc xây baseline bằng rule-based + ML.
- Chuyển model sang ESP32-S3.
- Đo latency, RAM, Flash và độ chính xác demo.

### Giai Đoạn 4: Server Và Dashboard

- Xây API server và MQTT broker.
- Lưu dữ liệu vào database.
- Xây dashboard realtime.
- Hiển thị node theo người dùng, phòng hoặc khu vực.

### Giai Đoạn 5: OTA Và Quản Lý Thiết Bị

- Hoàn thiện OTA firmware.
- Thêm firmware/model version.
- Thêm trạng thái cập nhật trên dashboard.
- Ghi log thành công/thất bại của mỗi lần cập nhật.

### Giai Đoạn 6: Prototype Sản Phẩm

- Lắp PCB carrier với module PPG và module IMU.
- Làm vỏ thiết bị.
- Tối ưu năng lượng.
- Hoàn thiện video demo, slide và báo cáo.

## 10. Điểm Mạnh, Hạn Chế Và Ranh Giới Kỹ Thuật

### 10.1. Điểm Mạnh

- Đúng định hướng VEDC2026: Embedded AI, AIoT, Smart Healthcare, Edge AI Device.
- Có ứng dụng thực tế trong gia đình, bệnh viện và khu chăm sóc.
- Xử lý tại edge giúp giảm độ trễ và giảm phụ thuộc vào server.
- Server hỗ trợ theo dõi dài hạn và quản lý nhiều node.
- OTA giúp hệ thống có khả năng nâng cấp sau triển khai.
- Có thể demo rõ bằng phần cứng thật.

### 10.2. Hạn Chế Và Thách Thức

- Tín hiệu PPG dễ nhiễu khi người dùng chuyển động hoặc đeo sai vị trí.
- Dữ liệu IMU cần được thu và gán nhãn cẩn thận để giảm cảnh báo sai.
- ESP32-S3 có giới hạn RAM/Flash nên model phải nhỏ.
- Dữ liệu y sinh khó thu thập và gán nhãn chính xác.
- False alarm là vấn đề lớn trong hệ thống cảnh báo sức khỏe.
- Thiết kế đeo được cần tối ưu pin, kích thước và độ ổn định cơ khí.
- Hệ thống chỉ nên được trình bày là hỗ trợ cảnh báo sớm, không phải thiết bị chẩn đoán y tế.

### 10.3. Phạm Vi Không Làm Trong MVP

- Không chẩn đoán đột quỵ, động kinh hoặc bệnh lý chuyên sâu.
- Không tích hợp ECG/EMG trong MVP; chỉ để connector mở rộng trên PCB nếu còn thời gian.
- Không tích hợp cảm biến môi trường trong MVP; chỉ giữ ở mức mở rộng.
- Không làm định vị indoor phức tạp trong MVP; nếu cần chỉ dùng `room_id` cấu hình sẵn cho từng node.
- Không triển khai federated learning trong MVP.
- Không thay thế thiết bị y tế chuyên dụng.
- Không tối ưu sản phẩm thương mại ngay từ vòng đầu.

## 11. Thông Điệp Thuyết Trình

CareEdge là hệ thống giám sát sức khỏe theo vùng sử dụng ESP32-S3 và TinyML để xử lý dữ liệu sinh hiệu ngay tại thiết bị biên. Hệ thống có thể cảnh báo nhanh các bất thường như té ngã, bất động hoặc nhịp tim bất thường, đồng thời gửi dữ liệu về server để theo dõi dài hạn, quản lý nhiều node và cập nhật firmware/model qua OTA.
