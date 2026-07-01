# BÀI 1: PHÂN TÍCH & LỰA CHỌN PHƯƠNG ÁN TẠO MÃ NGUỒN

## 1. Phương án lựa chọn tối ưu
*   **Đáp án chọn:** **Phương án B**

## 2. Phân tích lý do chọn Phương án B (Dựa trên cấu trúc 5 thành phần của Prompt)
Phương án B là một ví dụ điển hình của việc thiết kế Prompt chuẩn cấu trúc, giúp AI hiểu sâu sắc và chính xác yêu cầu của lập trình viên nhờ 5 thành phần:
*   **Vai trò (Role):** *"Đóng vai Senior Java Developer."* -> Thiết lập mức độ chuyên môn, giúp AI định hình phong cách viết code chuẩn công nghiệp, tối ưu hiệu năng và tuân thủ các best practices.
*   **Mục tiêu (Task):** *"Viết class PaymentValidator kiểm tra tính hợp lệ của thẻ tín dụng."* -> Nêu rõ hành động cần thực hiện và đối tượng đích của hành động.
*   **Ngữ cảnh (Context):** *"Hệ thống E-commerce, cần validate trước khi gửi API thanh toán."* -> Giúp AI hiểu vị trí của module này trong hệ thống, từ đó thiết kế logic phù hợp với luồng nghiệp vụ thực tế của một hệ thống thương mại điện tử (cần tính an toàn và tin cậy cao).
*   **Ràng buộc (Constraint):** *"Dùng Java 17, triển khai thuật toán Luhn, ném ra ngoại lệ IllegalArgumentException nếu thẻ rỗng hoặc chứa chữ cái."* -> Đây là phần cực kỳ quan trọng. Ràng buộc cụ thể về phiên bản ngôn ngữ (Java 17), thuật toán nghiệp vụ (Luhn) và cách xử lý lỗi cụ thể (ném ngoại lệ có tên rõ ràng khi gặp input sai) giúp loại bỏ hoàn toàn mã nguồn lỗi thời hoặc các logic xử lý ngoại lệ tùy tiện của AI.
*   **Định dạng đầu ra (Format):** *"Chỉ trả về mã nguồn Java trong một code block, không giải thích."* -> Tiết kiệm tối đa thời gian đọc và parse output của lập trình viên hoặc các công cụ tự động hóa.

## 3. Phân tích lỗ hổng và rủi ro ảo tưởng (Hallucination) của Phương án A và C
*   **Phương án A:**
    *   *Lỗ hổng thiếu ngữ cảnh & ràng buộc:* Prompt quá sơ sài, không chỉ định phiên bản Java, không mô tả các trường hợp đặc biệt (như thẻ rỗng, chứa ký tự đặc biệt hay chữ cái).
    *   *Rủi ro ảo tưởng/Sai lệch nghiệp vụ:* AI có thể chọn cách xử lý lỗi tùy tiện (ví dụ: chỉ trả về `false` thay vì ném exception, hoặc ghi log lỗi mà không chặn luồng). Yêu cầu *"Code ngắn gọn thôi nhé"* có thể khiến AI lược bỏ các bước kiểm tra biên quan trọng (edge cases), dẫn đến mã nguồn không an toàn khi chạy trên Production.
*   **Phương án C:**
    *   *Lỗ hổng vi phạm nguyên lý đơn nhiệm (Single Responsibility Principle):* Yêu cầu AI sinh cả code Java, database SQL, hướng dẫn cài đặt và JDBC kết nối trong cùng một prompt. Điều này làm loãng sự tập trung của AI.
    *   *Rủi ro ảo tưởng:* Khi phạm vi yêu cầu quá rộng, AI rất dễ sinh ra các thông tin cấu hình database giả định, lỗi kết nối JDBC lỗi thời, hoặc thiết kế bảng SQL không tối ưu. Hơn nữa, việc này tạo ra sự thừa thãi thông tin cho một lập trình viên vốn chỉ cần class kiểm tra logic thẻ.
