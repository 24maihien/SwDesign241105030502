# LAB 1: PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG
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
#### 1.2. Lý do lựa chọn kiến trúc:
 Kiến trúc Layer được lựa chọn cho hệ thống “Payroll System” vì các lý do sau:
- Tính phân tách rõ ràng: Kiến trúc Layer giúp phân chia hệ thống thành các tầng riêng biệt (Giao diện, Business Logic, và Dữ liệu), giúp giảm độ phụ thuộc giữa các tầng và tăng khả năng bảo trì cũng như khả năng mở rộng hệ thống. Mỗi tầng có nhiệm vụ riêng biệt, từ giao tiếp người dùng đến xử lý logic và quản lý dữ liệu.
- Dễ dàng bảo trì và mở rộng: Với kiến trúc phân tầng, các thành phần có thể dễ dàng thay đổi hoặc mở rộng độc lập mà không ảnh hưởng đến toàn bộ hệ thống. Ví dụ, có thể thay đổi tầng giao diện (UI) hoặc tầng cơ sở dữ liệu mà không cần thay đổi tầng logic nghiệp vụ.
- Khả năng tái sử dụng mã nguồn: Tầng Business Logic chứa các quy tắc nghiệp vụ của hệ thống, có thể tái sử dụng cho nhiều giao diện hoặc ứng dụng khác mà không cần phải viết lại logic.
- Bảo mật và kiểm soát: Tầng Data Access Layer đảm bảo tính bảo mật, giúp kiểm soát và bảo vệ truy cập đến dữ liệu nhân viên, bảng chấm công, và thông tin thanh toán, hỗ trợ các biện pháp bảo vệ dữ liệu, đặc biệt là trong các hệ thống đòi hỏi tính bảo mật cao như Payroll System.
- Dễ dàng tích hợp với hệ thống cũ: Do Payroll System phải kết nối với hệ thống DB2 của Project Management Database, kiến trúc Layer cho phép thực hiện tích hợp với hệ thống cũ mà không ảnh hưởng đến các tầng còn lại, đảm bảo hệ thống hoạt động ổn định.
#### 1.3. Lý do lựa chọn kiến trúc:
Biểu đồ Package mô tả kiến trúc
![Diagram](https://www.planttext.com/api/plantuml/png/Z5HBJiCm4Dtt55PMiEY60w2cQeKgKRLguG23CnHJnud63Y92d8m5H-8AsFaOsxI8ICbYvisRDsyq-Vhud6a3P9fIJchWHpWWoxQ46fK18oh5Rg55ojZRX34kGMksB6jPjOZtgoxedZrAv6OBRMdBBYw7w58Pf3jH8WSgkkYxVJsFXLCbPLwKGWLSQn2sjL1ZcvLwh3pbhb53cG_Te482WpkiAp936_i9P4wdronhDEgCZNBsI2-2urdSCCiFB54RGrtcFz1UuuYqChtbULrBmSyudeZsLfMWRF6V3WT3-BAQAevQX-lg78lMaXPnaBoHrkVKVufN4Wc8vlLKXs5Ze_Ffvj9ndO5ZR95lUeV3mHnW9FE0S8ZVW5XPcWytim03BEVEiVEtq9F6smfZsuRu4sZSK84K9QXwjgUpxZRfPkgJReGJcKxeOdxbD3rOkaZeyjMUcmB9zgqsMEfGvnpKiGy7dOMxpo5gYKvu5fIToCOCCrI5-ujy0m00__y30000).
### 2. Cơ chế phân tích
Các cơ chế cần thiết để đáp ứng yêu cầu của hệ thống bao gồm:
- Phân quyền truy cập: Chỉ những người có quyền mới truy cập được các thông tin nhạy cảm về lương và chấm công.
- Tính toán lương tự động: Tự động tính toán lương vào thứ Sáu và cuối tháng cho nhân viên.
- Tích hợp cơ sở dữ liệu kế thừa DB2: Đảm bảo khả năng truy xuất và lưu trữ thông tin từ cơ sở dữ liệu DB2 mà không cần thay đổi cơ sở dữ liệu hiện có.
- Lưu trữ và bảo mật thông tin: Đảm bảo dữ liệu chấm công và lương được lưu trữ an toàn và đáp ứng tiêu chuẩn bảo mật thông tin cá nhân.
### 3. Phân tích ca sử dụng "Select Payment"
#### 3.1. Các lớp phân tích
- Employee: Đại diện cho nhân viên, chứa thông tin cá nhân và lựa chọn phương thức thanh toán.
- PaymentProcessor: Chịu trách nhiệm tính toán và xử lý yêu cầu thanh toán từ nhân viên.
- PaymentMethod: Đại diện cho các phương thức thanh toán (chuyển khoản, nhận trực tiếp, và qua bưu điện).
#### 3.2.Biểu đồ Sequence cho "Select Payment"
![Diagram](https://www.planttext.com/api/plantuml/png/R9112i8m44NtESNGbIvwWIwaeYww40Nf0OPqj84sYUbKwDbSU2IlO59IjEfgXl__F3xpl3_oZj5ntpO29Hi7kzOsPY0IrijAAekQ8PdKiaW0EoYBkNt4eIND9t8t9McCnFq_Phi-Z24_XPX4I5SUdFdBXYH3P8go24R4PU3esbF7cnhrXM9cJroRQh4KCHKEF3g3tbR8FoblGVh9b4QVbMkHbT5lHgmpCqCPhq-LlzoST1K--G800F__0m00).
#### 3.3. Thuộc tính và nhiệm vụ của các lớp
- Employee:
      + Thuộc tính: employeeID, paymentMethod.
      + Nhiệm vụ: Cung cấp lựa chọn phương thức thanh toán.
- PaymentProcessor:
      + Thuộc tính: amount, transactionID.
      + Nhiệm vụ: Kiểm tra tính hợp lệ và thực hiện giao dịch.
- PaymentMethod:
      + Thuộc tính: methodType, details.
      + Nhiệm vụ: Thực hiện giao dịch cụ thể tùy theo loại thanh toán.
### 4. Phân tích ca sử dụng "Maintain Timecard"
#### 4.1. Các lớp phân tích
- Employee: Cung cấp thông tin về nhân viên.
- Timecard: Đại diện cho bản ghi chấm công với các thông tin về giờ làm việc và ngày làm.
- TimecardManager: Chịu trách nhiệm thêm, sửa và lưu trữ dữ liệu chấm công.
#### 4.2.  Biểu đồ Sequence cho "Maintain Timecard"
![Diagram](https://www.planttext.com/api/plantuml/png/R9112i8m44NtESNGbIvwWIwaeYww40Nf0OPqj84sYUbKwDbSU2IlO59IjEfgXl__F3xpl3_oZj5ntpO29Hi7kzOsPY0IrijAAekQ8PdKiaW0EoYBkNt4eIND9t8t9McCnFq_Phi-Z24_XPX4I5SUdFdBXYH3P8go24R4PU3esbF7cnhrXM9cJroRQh4KCHKEF3g3tbR8FoblGVh9b4QVbMkHbT5lHgmpCqCPhq-LlzoST1K--G800F__0m00).
#### 4.3. Thuộc tính và nhiệm vụ của các lớp
- Employee:
      + Thuộc tính: employeeID, name.
      + Nhiệm vụ: Cung cấp thông tin cá nhân và dữ liệu chấm công.
- Timecard:
      + Thuộc tính: date, hoursWorked.
      + Nhiệm vụ: Lưu trữ dữ liệu chấm công cụ thể cho từng ngày.
- TimecardManager:
      + Thuộc tính: timecardList.
      + Nhiệm vụ: Quản lý và cập nhật thông tin chấm công.
### 5. Hợp nhất kết quả phân tích
Các kết quả phân tích cho hai ca sử dụng Payment và Maintain Timecard được hợp nhất để tạo thành tài liệu phân tích hệ thống hoàn chỉnh: 
- Tích hợp các biểu đồ lớp: Các lớp Employee, PaymentProcessor, PaymentMethod, Timecard, và TimecardManager kết hợp với nhau, thể hiện một hệ thống đầy đủ cho Payroll System.
- Tích hợp biểu đồ sequence: Các biểu đồ sequence mô tả chi tiết các tương tác cho quy trình thanh toán và chấm công, đảm bảo tính nhất quán trong việc xử lý nghiệp vụ.
