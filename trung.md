# Dự án tưới tiêu thông minh

## I. Vấn đề và mục tiêu 
- **Dự án giải quyết vấn đề gì?**
  - Tình trạng hạn hán, thiếu nước cục bộ vào mùa khô kéo dài tại Tây Nguyên; rủi ro thời tiết cực đoan (mưa bão đột ngột gây lãng phí nước/ngập úng); và nguy cơ bùng phát dịch bệnh, nấm mốc (như nấm Phytophthora trên sầu riêng, tiêu) do không kiểm soát tốt vi khí hậu. Ngoài ra, giải quyết điểm yếu mất kết nối mạng Internet/Wi-Fi thường xuyên tại các vùng rẫy sâu. 

- **Vấn đề này có thật sự đáng giải quyết không?**
  - Cực kỳ đáng giải quyết. Các loại cây công nghiệp và cây ăn trái giá trị cao (sầu riêng, cà phê, tiêu) là nguồn thu nhập chính của Tây Nguyên. Việc tưới sai cách hoặc không phát hiện sớm nấm bệnh có thể làm thiệt hại hàng trăm triệu đồng mỗi héc-ta của nông dân chỉ trong một mùa vụ. 

- **Ai đang gặp vấn đề này?**
  - Các hộ nông dân, chủ trang trại, gia trại canh tác cây công nghiệp và cây ăn quả lâu năm tại khu vực Tây Nguyên (Đắk Lắk, Lâm Đồng, Gia Lai, Đắk Nông, Kon Tum). 

- **Hiện tại họ đang giải quyết bằng cách nào?**
  - Họ dùng các hệ thống tưới nhỏ giọt hoặc béc phun bán tự động bằng cách hẹn giờ cố định, bật/tắt thủ công bằng tay hoặc qua các bộ điều khiển GSM/Wi-Fi cơ bản. Việc phun thuốc ngừa bệnh thường làm theo định kỳ hoặc khi thấy lá cây chớm hỏng thì mới phun. 

- **Cách hiện tại có hạn chế gì?**
  - Tưới theo định kỳ gây lãng phí nước và phân bón nếu đất còn ẩm, hoặc khiến cây bị héo nếu trời nắng gắt hơn dự kiến. Quan trọng nhất, các bộ điều khiển thông thường sẽ "tê liệt" hoặc hoạt động sai lệch khi mất mạng Internet. Việc trị bệnh cho cây khi đã phát bệnh thường tốn kém và hiệu quả thấp. 

- **Mục tiêu cuối cùng của dự án là gì?**
  - Tạo ra một hệ thống tự động hóa tưới tiêu thông minh tích hợp trí tuệ nhân tạo tại biên (Edge AI), có khả năng tự suy luận tối ưu lượng nước, cảnh báo nguy cơ nấm bệnh bùng phát và hoạt động bền bỉ 24/7 ngay cả khi hoàn toàn mất kết nối Internet. 

## II. Người dùng và nhu cầu 
- **Người dùng chính là ai?**
  - Người nông dân trực tiếp quản lý rẫy và các chủ trang trại tại Tây Nguyên. 

- **Người dùng cần chức năng gì nhất?**
  - Hệ thống tự động tưới đúng, tưới đủ, tiết kiệm điện nước; tự ngắt khi trời mưa; và phát cảnh báo sớm về độ mặn (EC) hoặc nguy cơ bệnh hại trực tiếp về điện thoại một cách đơn giản, dễ hiểu nhất. 

- **Họ sẽ dùng sản phẩm trong tình huống nào?**
  - Hằng ngày trong suốt mùa khô và đầu mùa mưa để quản lý tưới tiêu; giám sát từ xa khi không có mặt tại rẫy; hoặc theo dõi các khuyến nghị của AI khi thời tiết thay đổi đột ngột. 

- **Họ dùng thường xuyên hay chỉ khi cần?**
  - Hệ thống phần cứng hoạt động **thường xuyên liên tục (24/7)** ngoài thực địa, còn nông dân sẽ tương tác với dashboard/app **hằng ngày** (1-2 lần/ngày) để kiểm tra trạng thái rẫy. 

- **Họ dùng trên thiết bị nào?**
  - Điện thoại thông minh (smartphone) phân khúc phổ thông chạy hệ điều hành Android. 

- **Họ có sẵn sàng thay đổi thói quen để dùng sản phẩm không?**
  - Có, nếu sản phẩm chứng minh được khả năng **tiết kiệm chi phí** (phân bón, nước, tiền điện) và **giao diện cực kỳ tối giản**, không đòi hỏi họ phải hiểu biết sâu về công nghệ hay AI. 

## III. Giải pháp đề xuất 
- **Giải pháp của team là gì?**
  - Xây dựng hệ thống mạng cảm biến không dây diện rộng công suất thấp (LoRa) kết hợp vi xử lý tầm trung tích hợp TinyML (Edge AI) xử lý tại chỗ, liên kết đồng bộ dữ liệu lên nền tảng Cloud. 

- **Sản phẩm cuối cùng sẽ trông như thế nào?**
  - Gồm các **Hộp thiết bị biên (Edge Nodes)** bọc kín chống nước kèm tấm pin mặt trời cắm ngoài rẫy, một **Bộ trung tâm (Gateway)** đặt tại nhà rẫy, và một **Ứng dụng giao diện Web/App** trực quan trên điện thoại. 

- **Nó là app, web, thiết bị, mô hình, hệ thống hay dịch vụ?**
  - Đây là một **Hệ thống phần cứng và phần mềm toàn diện (End-to-End IoT System)** tích hợp mô hình nhúng AI. 

- **Input của hệ thống là gì?**
  - Dữ liệu thời gian thực từ cảm biến: Nhiệt độ, độ ẩm, độ dẫn điện EC của đất; nhiệt độ, độ ẩm không khí; lưu lượng nước trong đường ống; trạng thái lượng mưa mặt đất và API dự báo thời tiết trực tuyến. 

- **Output của hệ thống là gì?**
  - Lệnh đóng/mở van điện từ điều khiển tưới; tín hiệu cảnh báo rủi ro bỡ ống/nghẹt béc; cảnh báo nguy cơ nấm bệnh (Xanh/Vàng/Đỏ) hiển thị trên màn hình dashboard của nông dân. 

- **Điểm khác biệt của giải pháp là gì?**
  - Tự động ra quyết định thông minh hoàn toàn ngoại tuyến (Offline) nhờ TinyML chạy trực tiếp trên chip ESP32-S3 mà không cần máy chủ (Server) AI đắt tiền. Tích hợp đo chỉ số EC đất để kiểm soát phân bón/độ mặn — điều mà các bộ tưới thông thường bỏ qua. 

- **Vì sao giải pháp này tốt hơn cách hiện tại?**
  - Tiết kiệm chi phí vận hành mạng (nhờ sóng LoRa miễn phí thay vì sim 4G cho từng node), tăng tính chịu lỗi của hệ thống trước hạ tầng mạng không ổn định tại vùng sâu vùng xa, và chuyển dịch từ "chữa bệnh cây" sang "phòng bệnh cây" nhờ mô hình AI dự báo sớm vi khí hậu. 

## IV. Phạm vi dự án 
- Dự án tập trung phát triển một mô hình mẫu (Prototype) hoàn chỉnh gồm 1-2 Edge Nodes kết nối đến 1 Gateway, thử nghiệm đo đạc các thông số đất, không khí và chạy mô hình TinyML mô phỏng dự báo ngay tại phòng thí nghiệm/vườn thực nghiệm nhỏ trong thời gian từ nay đến tháng 10/2026. Dự án không bao gồm việc sản xuất thương mại hàng loạt hoặc bao phủ toàn bộ một nông trường lớn trong giai đoạn thi đấu. 

## V. Chức năng chính 
- **Các chức năng cốt lõi là gì?**
  - a. Thu thập dữ liệu cảm biến đa tầng. 
  - b. Suy luận AI tại biên để điều khiển tưới và nhận diện bất thường. 
  - c. Truyền thông diện rộng không dây tầm xa (LoRa). 
  - d. Hiển thị thông tin trực quan và đồng bộ đám mây (Cloud Dashboard). 

- **Chức năng nào phục vụ trực tiếp mục tiêu dự án?**
  - Chức năng **Suy luận AI tại biên ra quyết định đóng/cắt van ngoại tuyến và Dự báo nguy cơ nấm bệnh vi khí hậu** là cốt lõi để hiện thực hóa chủ đề "AI nhúng cho IoT thông minh". 

- **Mỗi chức năng cần input gì và tạo output gì?**
  - *Đọc cảm biến & Chạy AI*: Input là mảng dữ liệu (Time-series) các thông số vật lý -> Output là Trạng thái rủi ro bệnh (Phần trăm %) và Lệnh điều khiển Relay (On/Off). 
  - *Truyền thông LoRa*: Input là chuỗi Byte dữ liệu nén -> Output là dữ liệu nhận được tại Gateway nguyên vẹn. 
  - *Cloud Dashboard*: Input là dữ liệu từ Gateway đẩy lên qua MQTT/HTTP -> Output là các widget đồ thị biểu diễn trực quan và thông báo (Notification) tới điện thoại. 

- **Chức năng nào phụ thuộc vào chức năng nào?**
  - Chức năng chạy AI và chức năng truyền thông phụ thuộc hoàn toàn vào chức năng Thu thập dữ liệu cảm biến. Dashboard trên Cloud phụ thuộc vào chức năng Truyền thông từ Gateway lên mạng Internet. 

- **Chức năng nào dễ làm trước để có bản chạy được?**
  - Chức năng đọc cảm biến, kích hoạt relay bằng code logic cơ bản (if-else) và truyền dữ liệu qua LoRa lên Dashboard là dễ làm trước để có bộ khung phần cứng chạy thử (Bare-metal prototype). 

## VI. Công nghệ và tài nguyên 
- **Dùng công nghệ gì?**
  - Chip vi điều khiển ESP32-S3 (N16R8), chip RF LoRa SX1276, cảm biến công nghiệp RS485 (Modbus RTU), thư viện TinyML (TensorFlow Lite cho Microcontrollers hoặc Edge Impulse SDK), nền tảng Node-RED hoặc Adafruit IO cho Cloud Dashboard. 

- **Vì sao chọn công nghệ đó?**
  - ESP32-S3 có hiệu năng vượt trội với giá thành rất sinh viên (~120k), hỗ trợ tăng tốc AI. LoRa giúp truyền xa tới vài kilomet mà không tốn chi phí cước viễn thông hàng tháng. Cảm biến chuẩn RS485 bọc khoáng chịu được môi trường khắc nghiệt ngoài rẫy thực tế. 

- **Chi phí dự kiến bao nhiêu?**
  - Khoảng **1.800.000 VNĐ** cho một bộ Prototype đầy đủ (bao gồm cả mạch in PCB và tấm pin năng lượng mặt trời). 

- **Có công nghệ nào rủi ro quá cao không?**
  - Việc nhúng mô hình mạng nơ-ron học sâu (Deep Learning) quá lớn vào ESP32-S3 có nguy cơ gây tràn bộ nhớ RAM hoặc làm chip bị treo liên tục. 

- **Có phương án đơn giản hơn không?**
  - Có. Thay vì dùng mạng nơ-ron phức tạp, ta sử dụng các thuật toán học máy cổ điển được tối ưu hóa như **Cây quyết định (Decision Tree)** hoặc **SVM rút gọn**. Chúng tiêu tốn cực ít tài nguyên nhưng vẫn đảm bảo tính toán AI cục bộ hiệu quả. 

## VII. Dữ liệu 
- **Dự án có cần dữ liệu không?**
  - Rất cần. Dữ liệu là "thức ăn" để huấn luyện mô hình AI nhận biết rủi ro dịch bệnh và bất thường dòng chảy. 

- **Dữ liệu lấy từ đâu?**
  - Giai đoạn đầu lấy từ các bộ dữ liệu nông nghiệp công khai (Public Datasets) trên Kaggle về mối liên hệ giữa nhiệt-ẩm và nấm bệnh Phytophthora. Giai đoạn sau thu thập trực tiếp bằng cách đo đạc thực tế từ các cảm biến của nhóm. 

- **Có dữ liệu thật không?**
  - Có. Quá trình test thực địa tại các chậu cây trồng hoặc vườn nhỏ của nhóm sẽ sinh ra dữ liệu thật (Real dữ liệu). 

- **Dữ liệu có đủ để train AI không?**
  - Đủ nếu áp dụng phương pháp **Data Augmentation** (tăng cường dữ liệu bằng cách tạo nhiễu toán học) hoặc sử dụng tính năng giả lập môi trường từ các công cụ chuyên dụng như Edge Impulse. 

- **Cần lưu dữ liệu gì?**
  - Cần lưu: Chuỗi dữ liệu lịch sử nhiệt/ẩm/EC theo mốc thời gian (để vẽ đồ thị xu hướng) và lịch sử các lần bật/tắt van tưới, các cảnh báo lỗi hệ thống. 

## VIII. Kiến trúc hệ thống 
```text
[Các Cảm biến: Đất/Không khí] 
 │ (RS485 / I2C) 
 ▼ 
[Edge Node: ESP32-S3 + TinyML] ──(Điều khiển)──► [Van điện từ / Bơm] 
 │ 
 │ (Sóng không dây LoRa 433/915 MHz) 
 ▼ 
[Gateway: ESP32 / Raspberry Pi tại nhà rẫy] 
 │ 
 │ (Wi-Fi / 4G) 
 ▼ 
[Cloud Server / MQTT Broker] ◄──► [User Smartphone Dashboard]
```

- **Hệ thống gồm những module nào?**
  - Module Cảm biến, Module Xử lý & AI Biên (Edge Node), Module Chấp hành (Relay/Van), Module Thu phát tầm xa (LoRa), Module Cổng kết nối (Gateway), Module Đám mây (Cloud) và Trực quan hóa (Dashboard). 

- **Các module giao tiếp với nhau ra sao?**
  - Cảm biến giao tiếp với Node qua chuẩn RS485 (Modbus RTU) hoặc I2C. Node giao tiếp với Gateway qua tần số sóng vô tuyến LoRa. Gateway giao tiếp với Cloud qua giao thức MQTT bảo mật trên nền Wi-Fi/4G. 

- **Dữ liệu đi từ đâu đến đâu?**
  - Dữ liệu thô đi từ Đất/Môi trường -> Cảm biến -> Edge Node (Tại đây AI xử lý ra kết quả) -> Kết quả + Data thô đóng gói gửi qua LoRa đến Gateway -> Đẩy lên Cloud -> Hiển thị trên màn hình điện thoại người dùng. 

- **Module nào xử lý chính?**
  - **Edge Node (ESP32-S3)** chịu trách nhiệm xử lý chính bao gồm lọc nhiễu tín hiệu và chạy mô hình AI đưa ra quyết định đóng ngắt tức thời. 

- **Module nào hiển thị?**
  - Giao diện Web-app (Dashboard) chạy trên trình duyệt điện thoại di động của người nông dân. 

- **Module nào lưu dữ liệu?**
  - Cơ sở dữ liệu đám mây (Cloud Database) lưu trữ dữ liệu dài hạn; bộ nhớ Flash nội bộ của ESP32-S3 lưu trữ tạm thời khi mất mạng. 

- **Nếu một module lỗi thì ảnh hưởng thế nào?**
  - Nếu *Cloud/Internet lỗi*: Hệ thống vẫn tưới tiêu bình thường nhờ AI tại biên (Tính năng chịu lỗi cao). 
  - Nếu *Cảm biến đất lỗi*: Mô hình AI phát hiện bất thường (Anomaly Detection) sẽ lập tức cô lập cảm biến đó, chuyển sang chế độ tưới an toàn theo khung giờ cố định và phát cảnh báo "Lỗi thiết bị" về Gateway. 

## IX. Rủi ro và phương án dự phòng 
- **Phần nào dễ lỗi nhất?**
  - Phần cảm biến cắm dưới đất dễ bị hỏng hoặc sai số do phân bón và độ ẩm cao ăn mòn cơ học. 
  - *Biện pháp*: Dùng cảm biến chuẩn công nghiệp có bọc lớp nhựa epoxy bảo vệ và vỏ thép không gỉ. 

- **Phần nào team chưa biết làm?**
  - Thường là phần tối ưu hóa mô hình AI (nhúng code C++ vào vi điều khiển sao cho không bị tràn RAM). 
  - *Biện pháp*: Sử dụng nền tảng **Edge Impulse** để tự động cấu hình, lượng tử hóa (Quantization) mô hình từ dạng Float32 sang Int8 giúp giảm dung lượng mô hình đi 4 lần. 

- **Nếu thiếu dữ liệu thì sao?**
  - Sử dụng các thư viện tạo dữ liệu nhân tạo hoặc thu thập dữ liệu thô với tần suất cao (Oversampling) trong thời gian ngắn để bù đắp, kết hợp mượn cấu trúc mô hình đã được huấn luyện sẵn (Transfer Learning). 

- **Nếu phần cứng lỗi thì sao?**
  - Thiết kế mạch phần cứng luôn có sự tham gia của chip Watchdog Timer (WDT) tích hợp. Nếu vi điều khiển bị treo cứng quá 5 giây, WDT sẽ tự động khởi động lại (Reset) hệ thống ngay lập tức. 

- **Nếu model chạy không tốt thì sao?**
  - Thiết kế một đường truyền dự phòng (Fallback logic) bằng các lệnh if-else cơ bản trong code. Nếu mô hình AI trả về kết quả với độ tin cậy quá thấp (Confidence < 60%), hệ thống sẽ tự động bỏ qua AI và kích hoạt chạy theo bộ quy tắc an toàn định sẵn để bảo vệ cây trồng.
