# Lab 4 - Thiết kế ca sử dụng cho hệ thống "Payroll System" dựa vào kết quả phân tích ca sử dụng và các phần tử thiết kế
## 1. Login:
### 1.1. Mô tả tương tác giữa các đối tượng thiết kế:
- Đối tượng:
  + `LoginForm`: Giao diện nhập thông tin người dùng.
  + `AuthenticationService`: Xác thực thông tin đăng nhập.
  + `Employee`: Đối tượng đại diện cho người dùng sau khi đăng nhập.
- Tương tác:
  + Người dùng nhập thông tin vào `LoginForm`.
  + `LoginForm` gửi yêu cầu đến `AuthenticationService` để xác thực.
  + Nếu thông tin hợp lệ, `AuthenticationService` tạo phiên làm việc với đối tượng `Employee`.
### 1.2. Đơn giản hóa sơ đồ tuần tự bằng hệ thống con:
- Hệ thống con liên quan:
  + `Authentication Subsystem`: Bao gồm `LoginForm` và `AuthenticationService`.
- Quy trình: Thay vì xử lý trực tiếp tất cả các logic trong giao diện, logic xác thực được chuyển cho `AuthenticationService`.
  
![](https://www.planttext.com/api/plantuml/png/T9B1IWCn48RlUOevjeU-m1waWgW7yM9zW6msx8Pk9pMR57kK7ZnuyW44br84eQ0WYCcXXos-Hvx0Lp3RLhk5zZQJcN_-RuRyk4Mtq5HfCyX9qHS8IXQSKAQbWkk2An9BWmbLOxYGgS1JgGQ4ITHAvd1iTCPH2qQra7Z5rKWmJXAgQKmBlfAVR192wWmwHzin4Lnctiw7eBFg0rFGmNpvk9o445S5yjzQw_QQHN3ctLp0k7ermBnzCN1RbIoCzEwTaRsQUbWJBOAUCcCOUJl39Wkcts_UFGb8gYzCILC2dSD0FUNjD4npTz3tTg7XnjGFhK0q7KBktJraqjjF1lsrrxRGFWIyUxQ6WmvXMVDcLIbsLc_SRhDl1EV2kmckEXx-DeshKa8h9C-O0Li3hV52cvrfY8E3Q9CknwJ-8xy0003__mC0)

### 1.3. Mô tả hành vi liên quan đến lưu trữ:
- Dữ liệu:
  + Tên người dùng và mật khẩu được truy xuất từ cơ sở dữ liệu `UserDatabase`.
  + Phiên làm việc được lưu tạm thời trong bộ nhớ ứng dụng.
### 1.4. Tinh chỉnh mô tả luồng sự kiện:
1. Người dùng mở `LoginForm`.
2. Nhập tên người dùng và mật khẩu.
3. `LoginForm` gửi thông tin đến `AuthenticationService`.
4. `AuthenticationService` truy vấn `UserDatabase` để kiểm tra thông tin.
5. Nếu hợp lệ:
    - Tạo đối tượng `Employee`.
    - Hiển thị thông báo đăng nhập thành công.
6. Nếu không hợp lệ, hiển thị thông báo lỗi.
### 1.5. Hợp nhất các lớp và hệ thống con:
- Các lớp liên quan:
  + `LoginForm`: Quản lý giao diện nhập liệu.
  + `AuthenticationService`: Xử lý xác thực.
  + `Employee`: Đại diện người dùng đã đăng nhập.
### 1.6. Lý do thiết kế:
#### a. Mục tiêu:
- Xác thực người dùng trước khi cho phép truy cập hệ thống.
- Bảo vệ dữ liệu hệ thống khỏi truy cập trái phép.
#### b. Lý do:
- **Tách biệt giao diện và logic nghiệp vụ:**
  + `LoginForm` đại diện cho giao diện người dùng, giúp người dùng nhập thông tin (username, password). Tách biệt với logic nghiệp vụ xác thực trong `AuthenticationService`.
  + Thiết kế này giúp dễ dàng thay đổi hoặc nâng cấp giao diện mà không ảnh hưởng đến phần xác thực.
- **Đóng gói hệ thống con:**
  + `AuthenticationService` được thiết kế như một hệ thống con (subsystem) chịu trách nhiệm xử lý xác thực.
- **Tính mở rộng:**
  + Dễ dàng thêm các phương thức xác thực khác (như OTP, xác thực qua email) vào `AuthenticationService` mà không làm gián đoạn logic hiện tại.
- **Tuân thủ bảo mật:**
  + Thiết kế không cho phép giao diện (`LoginForm`) trực tiếp truy cập vào UserDatabase, đảm bảo rằng mọi truy vấn phải thông qua `AuthenticationService`, nơi có thể kiểm soát và ghi lại hoạt động.
## 2. Maintain Timecard:
### 2.1. Mô tả tương tác giữa các đối tượng thiết kế:
- Đối tượng:
  + `TimecardForm`: Giao diện nhập thẻ chấm công.
  + `TimecardController`: Xử lý logic nghiệp vụ liên quan đến thẻ chấm công.
  + `Timecard`: Đối tượng lưu thông tin về giờ làm việc.
- Tương tác:
  + Nhân viên nhập thông tin thẻ chấm công vào `TimecardForm`.
  + Dữ liệu được chuyển đến `TimecardController` để xử lý và lưu vào cơ sở dữ liệu qua `DatabaseService`.
### 2.2. Đơn giản hóa sơ đồ tuần tự bằng hệ thống con:
- Hệ thống con liên quan:
  + `Timecard Management Subsystem`: Bao gồm `TimecardForm`, `TimecardController` và `DatabaseService`.
- Quy trình: Tách riêng giao diện nhập liệu (`TimecardForm`) và xử lý logic nghiệp vụ (`TimecardController`).

![](https://www.planttext.com/api/plantuml/png/V98_JiCm58Ttd-Adxhr01bI9lmFg0WEhurZ4mh4hsudKcO61Gz0WiI1LC33XWS5Ixv4JS0KS4jfGH1RBVjBxtlT-ygV_c5b7ZIiBIUoDK33QSaAPqmR7nKBg9UUW5fDv7XuLAX6UrOIakbGPDKjSYe8pQh8JRGh2j796ostni7jBRaX67KsfvJZgBnVSL89nGhP3fWU_Q0dcUVE-Ni3buKrTmqKt5oiUB9vF1LXR9iEM8M8tEy5fuzS2MUDV84NZxyenqAwnnUtf9ZZVl9P3fIgiDDYcXctymt06sMl5z1-xgr0pg7PN1TdJLoeVqVgJLBTWRvM6Me-0kg0YuYVu16TH-FOxNNy_f90PLrdxCRu0003__mC0)

### 2.3. Mô tả hành vi liên quan đến lưu trữ:
Dữ liệu: Thông tin thẻ chấm công (ngày làm việc, số giờ) được lưu vào bảng `Timecards` trong cơ sở dữ liệu.
### 2.4. Tinh chỉnh mô tả luồng sự kiện:
1. Nhân viên mở `TimecardForm`.
2. Nhập thông tin thẻ chấm công:
    - Ngày làm việc.
    - Số giờ làm.
3. Nhấn "Lưu" để gửi yêu cầu đến `TimecardController`.
4. `TimecardController` xác thực dữ liệu và lưu vào `DatabaseService`.
5. Hiển thị thông báo lưu thành công.
### 2.5. Hợp nhất các lớp và hệ thống con:
- Các lớp liên quan:
  + `TimecardForm`: Quản lý giao diện nhập liệu.
  + `TimecardController`: Xử lý nghiệp vụ liên quan đến thẻ chấm công.
  + `Timecard`: Lưu trữ thông tin giờ làm việc.
### 2.6. Lý do thiết kế:
#### a. Mục tiêu:
- Cho phép nhân viên nhập, chỉnh sửa và lưu trữ thông tin chấm công.
- Đảm bảo thông tin được lưu trữ chính xác và có thể truy xuất khi cần.
#### b. Lý do:
- **Phân chia trách nhiệm rõ ràng:**
  + `TimecardForm` chỉ chịu trách nhiệm thu thập dữ liệu từ người dùng và chuyển tiếp dữ liệu đến hệ thống xử lý.
  + `TimecardController` (được thiết kế như một hệ thống con) đảm bảo rằng logic nghiệp vụ, như xác thực dữ liệu và xử lý định dạng, được xử lý trước khi lưu vào `DatabaseService`.
- **Tăng tính trừu tượng hóa:**
  + Thay vì cho phép `TimecardForm` giao tiếp trực tiếp với `DatabaseService`, `TimecardController` được sử dụng như một lớp trung gian giúp dễ dàng thay đổi logic nghiệp vụ mà không ảnh hưởng đến giao diện người dùng hoặc cơ sở dữ liệu.
- **Hỗ trợ phát triển song song:**
  + Cho phép các nhà phát triển giao diện làm việc song song với đội ngũ phát triển cơ sở dữ liệu mà không cần biết chi tiết hoạt động bên trong.
- **Dễ bảo trì:**
  + Việc tách biệt giao diện người dùng, logic nghiệp vụ, và lưu trữ dữ liệu giúp giảm thiểu rủi ro lỗi khi cập nhật một thành phần.
## 3. Run Payroll:
### 3.1. Mô tả tương tác giữa các đối tượng thiết kế:
- Đối tượng:
  + `PayrollController`: Quản lý quá trình tính lương.
  + `BankSystem`: Thực hiện giao dịch ngân hàng.
  + `PrintService`: In phiếu lương.
  + `Paycheck`: Đối tượng lưu thông tin lương.
- Tương tác:
  + `PayrollController` lấy thông tin từ thẻ chấm công và tính lương.
  + Kết quả được gửi đến `BankSystem` hoặc `PrintService`.
### 3.2. Đơn giản hóa sơ đồ tuần tự bằng hệ thống con:
- Hệ thống con liên quan:
  + `Payroll Processing Subsystem`: Bao gồm `PayrollController`, `BankSystem` và `PrintService`.
- Quy trình: Phân chia các chức năng thành hai phần chính:
  + Thanh toán qua ngân hàng (`BankSystem`).
  + In phiếu lương (`PrintService`).

![](https://www.planttext.com/api/plantuml/png/Z9EzJiCm58NtFCLLzxv01bH-940mWDg1rQHHRTMv0SUfoCZCnCX42wgGAYenCCL27LprFVm4l08tBQIbJGKPdDYvv_CvlicdcJGIpPHE8-abNO6WuYJqMA1Z1RljY1PO0hNprENF25evSmSzOKTOyu8OjOebdB6CRd9_CPMXyjfCiqkMX73m_T0CLKy4OIdPOzXjPeaEeoL52TG_TTvYv_hE9jo74-xCeu3flJCFs87hD2DVzXKvQ3kcKSxUPWFiU1lIWhVco8TJbmy9mEqxiJHjghdB3GGq3YC8YcLlJGJrQcCjHOS4FMTk_-1LEgi2_ih3f8OMPqNEs0wGWZF0Zdr2uBPFxu6kIlBoj7quT6Oi8BEZ50ANlwHahoJE2SlYRJ4lx200f3nZN5KNcViqMKGC9RN_6E6A2vTFqZB4LfEh_Q-mARQWLbJ_yIlMRMAxgXi4cd-1FXp5L0sQcgVXXao1j1-bWmR9Y__c2m00__y30000)

### 3.3. Mô tả hành vi liên quan đến lưu trữ:
- Dữ liệu:
  + Lương sau khi tính toán được lưu trong bảng `Paychecks`.
  + Thông tin giao dịch ngân hàng được ghi nhận vào `TransactionLog`.
### 3.4. Tinh chỉnh mô tả luồng sự kiện:
1. `PayrollController` khởi động quy trình tính lương.
2. Lấy thông tin thẻ chấm công từ bảng `Timecards`.
3. Tính lương cho từng nhân viên:
    - Lương theo giờ, cố định, hoặc hoa hồng.
4. Tạo đối tượng `Paycheck` cho mỗi nhân viên.
5. Gửi thông tin:
    - Đến `BankSystem` để chuyển khoản.
    - Hoặc đến `PrintService` để in phiếu lương.
### 3.5. Hợp nhất các lớp và hệ thống con:
- Các lớp liên quan:
  + `PayrollController`: Điều phối quy trình tính lương.
  + `BankSystem`: Xử lý giao dịch ngân hàng.
  + `PrintService`: Xử lý in phiếu lương.
  + `Paycheck`: Lưu thông tin chi tiết về lương.
### 3.6. Lý do thiết kế:
#### a. Mục tiêu:
- Tính toán và xử lý thanh toán lương cho nhân viên.
- Đảm bảo tùy chọn linh hoạt giữa chuyển khoản ngân hàng và in phiếu lương.
#### b. Lý do:
- **Phân nhánh xử lý linh hoạt:**
  + Biểu đồ tuần tự sử dụng cấu trúc điều kiện (alt/else) để thể hiện hai kịch bản: xử lý thanh toán qua `BankSystem` và in phiếu lương qua `PrintService`.
  + Đảm bảo quy trình tính lương có thể mở rộng hoặc thay đổi dễ dàng.
- **Tích hợp hệ thống con:**
  `PayrollController` được thiết kế như một hệ thống con, chịu trách nhiệm:
    + Tương tác với cơ sở dữ liệu thông qua `DatabaseService` để lấy thông tin chấm công.
    + Thực hiện logic tính lương.
    + Gửi yêu cầu đến các hệ thống phụ như `BankSystem` hoặc `PrintService`.
- **Hỗ trợ tích hợp dễ dàng:**
  + Hệ thống tương tác với `BankSystem` và `PrintService` thông qua giao diện, giúp tích hợp dễ dàng với các hệ thống bên ngoài hoặc thay thế chúng nếu cần.
