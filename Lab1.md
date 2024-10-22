# LAB1: PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG
## Mục đích: Phân tích kiến trúc và ca sử dụng hệ thống "Payroll System" trong file tài liệu yêu cầu đính kèm.

### 1. Phân tích kiến trúc
#### 1.1. Đề xuất kiến trúc:
##### Kiến trúc phù hợp cho hệ thống "Payroll System" là Kiến trúc Layer. Kiến trúc này phân tách hệ thống thành ba tầng độc lập: 
#### a. **Tầng Giao diện (Presentation Layer)**:
   - Đây là tầng giao tiếp trực tiếp với người dùng. Các nhân viên, quản trị viên tiền lương và nhân viên theo hợp đồng sẽ thực hiện các thao tác thông qua giao diện này như đăng nhập, quản lý bảng chấm công, chọn phương thức thanh toán, tạo báo cáo hành chính, và chạy bảng lương.
#### b. **Tầng Ứng dụng (Business Logic Layer)**:
   - Tầng này chứa các quy tắc và logic nghiệp vụ của hệ thống, đảm bảo rằng các thao tác của người dùng như tính toán lương, quản lý bảng chấm công, duy trì thông tin nhân viên, và quản lý đơn hàng mua được xử lý một cách chính xác.
#### c. **Tầng Dữ liệu (Database Layer)**:
   - Đây là tầng lưu trữ và quản lý dữ liệu, nơi hệ thống lưu trữ thông tin về nhân viên, bảng chấm công, lương, và các đơn mua hàng. Tầng này cũng có nhiệm vụ cung cấp các dữ liệu cần thiết cho tầng nghiệp vụ để thực hiện các thao tác tính toán và báo cáo.

