# Dự án phát hiện và dự báo ngập đô thị

## 1. Vấn đề và mục tiêu

### Dự án giải quyết vấn đề gì?
Dự án giải quyết vấn đề **người dân và chính quyền khó biết chính xác khu vực nào đang ngập, mức độ ngập ra sao và nguy hiểm tới đâu**. Ngoài ra, dự án còn hướng tới việc **dự báo nguy cơ ngập sắp xảy ra** để người dùng tránh đường hoặc chuẩn bị trước.

### Vấn đề này có thật sự đáng giải quyết không?
Có. Ngập đô thị ảnh hưởng trực tiếp đến việc đi lại, an toàn giao thông, sinh hoạt, kinh doanh và hạ tầng. Người dân thường chỉ biết đường ngập qua kinh nghiệm cá nhân, mạng xã hội hoặc khi đã đi tới nơi bị ngập.

### Ai đang gặp vấn đề này?
Người đi xe máy, ô tô, học sinh, sinh viên, người đi làm, tài xế công nghệ, đơn vị giao hàng, người dân sống ở khu vực trũng thấp và cơ quan quản lý đô thị.

### Hiện tại họ đang giải quyết bằng cách nào?
Họ thường xem tin trên Facebook, hỏi người quen, nhìn thời tiết, dựa vào kinh nghiệm tuyến đường quen thuộc hoặc đi đến nơi rồi mới phát hiện bị ngập.

### Cách hiện tại có hạn chế gì?
Thông tin thường không chính xác theo thời gian thực, dễ bị trễ, không có số liệu đo cụ thể, khó biết mức độ nguy hiểm và không có dự báo rõ ràng.

### Mục tiêu cuối cùng của dự án là gì?
Xây dựng một hệ thống có thể **phát hiện ngập theo thời gian thực, hiển thị lên bản đồ, cảnh báo mức độ nguy hiểm và dự báo nguy cơ ngập trong tương lai gần**.

---

## 2. Người dùng và nhu cầu

### Người dùng chính là ai?
Người dân di chuyển trong đô thị, đặc biệt là người đi xe máy, tài xế công nghệ, tài xế giao hàng và người đi làm/học hằng ngày.

### Người dùng cần chức năng gì nhất?
Cần biết **đường nào đang ngập, ngập nặng hay nhẹ, có đi qua được không và nên tránh tuyến nào**.

### Họ sẽ dùng sản phẩm trong tình huống nào?
Khi trời mưa lớn, sau mưa, trước khi đi ra ngoài, khi đang di chuyển hoặc khi cần chọn tuyến đường an toàn hơn.

### Họ dùng thường xuyên hay chỉ khi cần?
Chủ yếu dùng **khi cần**, đặc biệt vào mùa mưa hoặc khi có mưa lớn. Tuy nhiên tài xế công nghệ/giao hàng có thể dùng thường xuyên hơn.

### Họ dùng trên thiết bị nào?
Chủ yếu trên điện thoại thông qua web/app bản đồ. Với chính quyền hoặc nhóm quản lý, có thể dùng dashboard trên máy tính.

### Họ có sẵn sàng thay đổi thói quen để dùng sản phẩm không?
Có, nếu sản phẩm đơn giản, mở lên là thấy ngay khu vực ngập và gợi ý tuyến đường. Người dùng sẽ không muốn nhập nhiều thông tin phức tạp.

---

## 3. Giải pháp đề xuất

### Giải pháp của team là gì?
Team đề xuất hệ thống gồm các **trạm cảm biến đặt tại những điểm dễ ngập**, gửi dữ liệu về server để xử lý, sau đó hiển thị tình trạng ngập lên bản đồ và dùng dữ liệu lịch sử/thời tiết để dự báo.

### Sản phẩm cuối cùng sẽ trông như thế nào?
Sản phẩm sẽ gồm một bản đồ có các điểm/cung đường được đánh dấu màu theo mức độ ngập: bình thường, ngập nhẹ, ngập vừa, ngập nguy hiểm. Người dùng có thể xem vị trí, mức nước, thời gian cập nhật và cảnh báo.

### Nó là app, web, thiết bị, mô hình, hệ thống hay dịch vụ?
Đây là một **hệ thống IoT + phần mềm bản đồ**. Trong đó có thiết bị cảm biến ngoài thực tế, server xử lý dữ liệu và giao diện web/app cho người dùng.

### Input của hệ thống là gì?
Input gồm mực nước đo được tại từng điểm, dữ liệu mưa/thời tiết, vị trí cảm biến, thời gian đo, trạng thái thiết bị và dữ liệu lịch sử ngập.

### Output của hệ thống là gì?
Output gồm trạng thái ngập hiện tại, mức độ nguy hiểm, bản đồ ngập, cảnh báo cho người dùng và dự báo nguy cơ ngập trong thời gian tới.

### Điểm khác biệt của giải pháp là gì?
Khác biệt là hệ thống không chỉ dựa vào báo cáo thủ công mà có **dữ liệu đo trực tiếp từ cảm biến**, cập nhật theo thời gian thực và có khả năng dự báo.

### Vì sao giải pháp này tốt hơn cách hiện tại?
Vì thông tin nhanh hơn, có số liệu cụ thể hơn, ít phụ thuộc vào tin đồn/mạng xã hội và có thể hỗ trợ người dùng ra quyết định trước khi đi vào khu vực ngập.

---

## 4. Phạm vi dự án

### Phạm vi ban đầu của dự án là gì?
Giai đoạn đầu chỉ triển khai ở một khu vực nhỏ, ví dụ một vài tuyến đường hay điểm thường ngập trong thành phố. Mục tiêu là demo được phát hiện ngập, gửi dữ liệu, hiển thị bản đồ và cảnh báo.

### Những gì chưa làm ở giai đoạn đầu?
Chưa cần phủ toàn thành phố, chưa cần dự báo AI quá phức tạp, chưa cần điều hướng giao thông hoàn chỉnh và chưa cần tích hợp trực tiếp với hệ thống chính quyền.

### Phạm vi mở rộng sau này là gì?
Sau khi demo ổn định, có thể mở rộng thêm nhiều node cảm biến, thêm dữ liệu thời tiết, dự báo bằng AI, đề xuất tuyến đường tránh ngập và dashboard cho cơ quan quản lý.

---

## 5. Chức năng chính

### Các chức năng cốt lõi là gì?
Các chức năng cốt lõi gồm:

- Đo mực nước.
- Xác định mức độ ngập.
- Gửi dữ liệu về server.
- Hiển thị lên bản đồ.
- Cảnh báo nguy hiểm.
- Lưu dữ liệu lịch sử.

### Chức năng nào phục vụ trực tiếp mục tiêu dự án?
Đo mực nước, phân loại mức độ ngập và hiển thị trên bản đồ là các chức năng phục vụ trực tiếp nhất.

### Mỗi chức năng cần input gì?
Đo mực nước cần dữ liệu từ cảm biến. Phân loại ngập cần mực nước và ngưỡng nguy hiểm. Bản đồ cần tọa độ node và trạng thái ngập. Dự báo cần dữ liệu lịch sử, mưa và thời gian.

### Mỗi chức năng tạo output gì?
Đo mực nước tạo ra giá trị mực nước. Phân loại tạo ra trạng thái bình thường/ngập nhẹ/ngập nặng. Bản đồ tạo ra giao diện trực quan. Dự báo tạo ra cảnh báo nguy cơ ngập.

### Chức năng nào phụ thuộc vào chức năng nào?
Bản đồ phụ thuộc vào dữ liệu từ cảm biến và server. Cảnh báo phụ thuộc vào kết quả phân loại ngập. Dự báo phụ thuộc vào dữ liệu lịch sử và dữ liệu thời tiết.

### Chức năng nào dễ làm trước để có bản chạy được?
Nên làm trước phần **đo mực nước bằng một node cảm biến**, gửi dữ liệu lên server và hiển thị trạng thái trên web/map đơn giản.

---

## 6. Công nghệ và tài nguyên

### Dùng công nghệ gì?
Có thể dùng ESP32 cho node cảm biến, cảm biến siêu âm chống nước hoặc cảm biến áp suất nước, giao tiếp Wi-Fi/LoRa/4G tùy phạm vi, server dùng Node.js/Python, database như Firebase/PostgreSQL, giao diện web dùng React hoặc bản đồ Leaflet/Google Maps.

### Vì sao chọn công nghệ đó?
ESP32 rẻ, dễ lập trình, có Wi-Fi/Bluetooth, phù hợp làm prototype IoT. Web map dễ demo, dễ truy cập trên điện thoại. Database giúp lưu dữ liệu lịch sử để phân tích và dự báo.

### Chi phí dự kiến bao nhiêu?
Một node demo đơn giản có thể khoảng vài trăm nghìn đến hơn một triệu đồng, tùy cảm biến, hộp chống nước, nguồn và module truyền dữ liệu. Nếu triển khai nhiều node thật ngoài đường thì chi phí sẽ tăng do yêu cầu độ bền, chống nước, nguồn điện và bảo trì.

### Có công nghệ nào rủi ro quá cao không?
Phần dự báo AI là rủi ro nếu chưa có đủ dữ liệu thật. Triển khai phần cứng ngoài trời cũng rủi ro vì nước, bụi, mất nguồn, hỏng cảm biến hoặc mất kết nối.

### Có phương án đơn giản hơn không?
Có. Giai đoạn đầu chỉ cần làm mô hình demo với một vài node giả lập/cảm biến thật, hiển thị mực nước lên dashboard và dùng ngưỡng cố định để phân loại ngập, chưa cần AI phức tạp.

---

## 7. Dữ liệu

### Dự án có cần dữ liệu không?
Có. Dự án cần dữ liệu thời gian thực từ cảm biến và dữ liệu lịch sử để phân tích/dự báo.

### Dữ liệu lấy từ đâu?
Dữ liệu lấy từ cảm biến mực nước, dữ liệu mưa/thời tiết, dữ liệu vị trí các điểm ngập và có thể thêm dữ liệu do người dùng báo cáo.

### Có dữ liệu thật không?
Giai đoạn đầu có thể chưa có nhiều dữ liệu thật. Team có thể thu thập dữ liệu demo từ mô hình, cảm biến đặt thử nghiệm hoặc dùng dữ liệu giả lập để kiểm tra hệ thống.

### Dữ liệu có đủ để train AI không?
Ban đầu có thể chưa đủ. Vì vậy không nên đặt mục tiêu AI quá lớn ngay từ đầu. Có thể dùng rule-based trước, sau đó khi có dữ liệu lịch sử đủ lớn mới train mô hình dự báo.

### Cần lưu dữ liệu gì?
Cần lưu ID node, vị trí node, thời gian đo, mực nước, mức độ ngập, trạng thái thiết bị, dữ liệu mưa/thời tiết và lịch sử cảnh báo.

---

## 8. Kiến trúc hệ thống

### Hệ thống gồm những module nào?
Hệ thống gồm:

- Node cảm biến.
- Module truyền dữ liệu.
- Server/API.
- Database.
- Module xử lý/phân loại ngập.
- Module dự báo.
- Giao diện bản đồ.
- Module cảnh báo.

### Các module giao tiếp với nhau ra sao?
Node cảm biến gửi dữ liệu lên server qua Wi-Fi/LoRa/4G. Server lưu dữ liệu vào database, xử lý trạng thái ngập, sau đó giao diện web/app lấy dữ liệu từ server để hiển thị.

### Dữ liệu đi từ đâu đến đâu?
Dữ liệu đi theo luồng:

```text
Cảm biến → ESP32/node → mạng truyền thông → server/API → database → web/app bản đồ → người dùng
```

### Module nào xử lý chính?
Server là module xử lý chính. Nó nhận dữ liệu, kiểm tra lỗi, phân loại mức độ ngập, lưu dữ liệu và cung cấp API cho giao diện.

### Module nào hiển thị?
Web/app bản đồ là module hiển thị. Nó cho người dùng xem vị trí ngập, mức độ nguy hiểm và cảnh báo.

### Module nào lưu dữ liệu?
Database là module lưu dữ liệu. Nó lưu dữ liệu cảm biến hiện tại, dữ liệu lịch sử, thông tin node và trạng thái cảnh báo.

### Nếu một module lỗi thì ảnh hưởng thế nào?
Nếu cảm biến lỗi thì điểm đó không có dữ liệu chính xác. Nếu mạng lỗi thì dữ liệu không gửi được. Nếu server lỗi thì toàn hệ thống không cập nhật. Nếu database lỗi thì mất lịch sử. Nếu giao diện lỗi thì người dùng không xem được thông tin.

---

## 9. Rủi ro và phương án dự phòng

### Phần nào dễ lỗi nhất?
Phần cứng ngoài trời dễ lỗi nhất, đặc biệt là cảm biến, nguồn điện, hộp bảo vệ và kết nối mạng.

### Phần nào team chưa biết làm?
Có thể team chưa mạnh ở phần triển khai phần cứng ngoài thực tế, chống nước, hiệu chuẩn cảm biến và dự báo AI bằng dữ liệu thật.

### Nếu thiếu dữ liệu thì sao?
Dùng rule-based trước, ví dụ:

- Dưới 5 cm: bình thường.
- Từ 5–15 cm: ngập nhẹ.
- Từ 15–30 cm: ngập vừa.
- Trên 30 cm: nguy hiểm.

Sau đó thu thập dữ liệu dần để cải thiện mô hình.

### Nếu phần cứng lỗi thì sao?
Thiết kế hộp chống nước, kiểm tra định kỳ, gửi trạng thái pin/kết nối về server, dùng nhiều cảm biến để đối chiếu hoặc cho phép người dùng báo cáo bổ sung.

### Nếu mô hình không tốt thì sao?
Không phụ thuộc hoàn toàn vào AI. Có thể dùng mô hình đơn giản trước, kết hợp ngưỡng cảm biến, lượng mưa và dữ liệu lịch sử. AI chỉ là phần nâng cấp sau khi có đủ dữ liệu.
