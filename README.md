# Assignment4_Embedded_System
Lập trình GPIO và Ngắt ngoài (EXTI) trên STM32F1
Dự án này là một ví dụ minh họa cách kết hợp hoạt động của GPIO và Ngắt ngoài (External Interrupt - EXTI) trên vi điều khiển STM32F103, sử dụng thư viện Standard Peripheral Library (SPL).

Chương trình thực hiện hai tác vụ chạy song song:

Một đèn LED nhấp nháy liên tục theo một chu kỳ định sẵn trong vòng lặp chính.

Một đèn LED khác được điều khiển bật/tắt mỗi khi người dùng nhấn nút, sử dụng cơ chế ngắt.

## Tính năng
Đa nhiệm đơn giản: Minh họa cách xử lý hai tác vụ khác nhau: một tác vụ lặp đi lặp lại (nháy LED) và một tác vụ dựa trên sự kiện (nhấn nút).

Điều khiển GPIO: Cấu hình các chân GPIO ở cả chế độ xuất (Output) để điều khiển LED và chế độ nhập (Input) để đọc nút nhấn.

Sử dụng Ngắt ngoài (EXTI): Cấu hình ngắt ngoài để chương trình có thể phản ứng ngay lập tức với sự kiện nhấn nút mà không cần kiểm tra liên tục trong vòng lặp chính.

Chống dội phím: Áp dụng một kỹ thuật chống dội phím đơn giản bên trong trình phục vụ ngắt để đảm bảo mỗi lần nhấn nút chỉ được ghi nhận một lần.

## Cấu hình phần cứng
Vi điều khiển: STM32F103C8T6 (Board Blue Pill hoặc tương tự).

LED 1 (Nhấp nháy tự động):

Nối với chân PC13.

LED 2 (Điều khiển bằng nút nhấn):

Nối với chân PC14.

Nút nhấn:

Nối một chân của nút nhấn vào chân PA0.

Nối chân còn lại của nút nhấn vào GND.

Lưu ý: Chân PA0 được cấu hình là Input Pull-Up, do đó không cần điện trở kéo ngoài.

## Cách hoạt động của code
Hàm GPIO_Config():

Kích hoạt xung clock cho GPIOA (dùng cho nút nhấn) và GPIOC (dùng cho 2 LED).

Cấu hình PC13 và PC14 là Output Push-Pull để điều khiển hai đèn LED.

Cấu hình PA0 là Input Pull-Up để đọc tín hiệu từ nút nhấn.

Hàm EXTI0_Config():

Cấu hình ngắt ngoài trên đường EXTI_Line0 được kết nối với chân PA0.

Ngắt được thiết lập để kích hoạt bởi cạnh xuống (Falling Edge), tức là khi nút được nhấn và chân PA0 được kéo từ mức CAO xuống THẤP.

Kích hoạt và cài đặt độ ưu tiên cho trình phục vụ ngắt EXTI0_IRQn trong NVIC.

Hàm main():

Gọi các hàm cấu hình GPIO_Config() và EXTI0_Config().

Vào một vòng lặp while(1) vô tận.

Bên trong vòng lặp, trạng thái của LED 1 (PC13) được đảo liên tục sau mỗi 500ms, tạo ra hiệu ứng nhấp nháy với tần số 1Hz. Vòng lặp này chạy độc lập và không quan tâm đến nút nhấn.

Hàm EXTI0_IRQHandler() (Trình phục vụ ngắt):

Hàm này sẽ tự động được gọi mỗi khi nút nhấn ở chân PA0 được nhấn.

Đầu tiên, nó kiểm tra và xóa cờ ngắt để sẵn sàng cho lần ngắt tiếp theo.

Thực hiện một delay ngắn (~50ms) để chống dội phím.

Kiểm tra lại để chắc chắn rằng nút nhấn vẫn đang được giữ.

Nếu đúng, trạng thái của LED 2 (PC14) sẽ được đảo (^=).
