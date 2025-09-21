# Assignment4_Embedded_System
Chắc chắn rồi! Dưới đây là nội dung được viết lại theo đúng cấu trúc và văn phong mà bạn đã cung cấp.

Lập trình GPIO và Giao tiếp UART (với Ngắt) trên STM32F1
Dự án này là một ví dụ minh họa cách kết hợp hoạt động của GPIO và giao tiếp UART sử dụng ngắt trên vi điều khiển STM32F103, dùng thư viện Standard Peripheral Library (SPL).

Chương trình cho phép vi điều khiển nhận lệnh văn bản (text command) từ một máy tính thông qua cổng nối tiếp để điều khiển trạng thái của một đèn LED. Toàn bộ quá trình nhận dữ liệu được xử lý bằng ngắt để tối ưu hóa hiệu năng.

Tính năng 📜
Điều khiển GPIO: Cấu hình một chân GPIO ở chế độ xuất (Output Push-Pull) để điều khiển một đèn LED duy nhất.

Giao tiếp UART: Cấu hình và sử dụng USART1 để gửi và nhận dữ liệu nối tiếp với máy tính, hoạt động như một giao diện điều khiển.

Sử dụng Ngắt UART: Cấu hình ngắt USART_IT_RXNE (Receive Not Empty) để chương trình có thể phản ứng ngay lập tức mỗi khi có byte dữ liệu mới đến mà không cần phải kiểm tra liên tục trong vòng lặp chính (polling).

Xử lý Lệnh Văn bản: Xây dựng một bộ đệm (buffer) để lưu trữ các ký tự nhận được và xử lý chuỗi lệnh hoàn chỉnh (ví dụ: "ON", "OFF") khi nhận được ký tự xuống dòng.

Cấu hình phần cứng 🛠️
Vi điều khiển: STM32F103C8T6 (Board Blue Pill hoặc tương tự).

Đèn LED:

Nối với chân PA4.

Giao tiếp Nối tiếp (với máy tính):

Nối chân PA9 (TX) của STM32 với chân RX của mạch chuyển USB-to-TTL.

Nối chân PA10 (RX) của STM32 với chân TX của mạch chuyển USB-to-TTL.

Nối chân GND của hai board với nhau.

Lưu ý: Cần một phần mềm terminal trên máy tính (như PuTTY, Tera Term) được cấu hình ở 9600 baud, 8 data bits, 1 stop bit, no parity.
