# LAB 1: PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG

## Mục đích
Phân tích kiến trúc và ca sử dụng hệ thống **"Payroll System"** dựa trên tài liệu yêu cầu đính kèm.

---

# Phân tích ca sử dụng "Create Employee" trong Payroll System

## 1. Phân tích các lớp

### 1.1. Các loại lớp
- **Boundary**: Đại diện cho giao diện người dùng và các điểm tương tác với hệ thống.
- **Control**: Điều phối luồng hoạt động của hệ thống, xử lý logic và điều khiển giữa các lớp.
- **Entity**: Lưu trữ thông tin dữ liệu và thể hiện các đối tượng trong hệ thống.

### 1.2. Các lớp trong ca sử dụng "Create Employee"

#### 1.2.1. Boundary
- **EmployeeForm**
  - **Vai trò**: Là giao diện mà **Admin** sử dụng để nhập thông tin của nhân viên mới (tên, địa chỉ, vị trí, mức lương, v.v.).
  - **Nhiệm vụ**:
    - Nhận thông tin đầu vào từ **Admin**.
    - Gửi yêu cầu tạo nhân viên mới đến **EmployeeManager** (Control).
    - Hiển thị kết quả (thành công hoặc thất bại) của quá trình tạo nhân viên cho **Admin**.

#### 1.2.2. Control
- **EmployeeManager**
  - **Vai trò**: Điều phối quá trình tạo nhân viên mới.
  - **Nhiệm vụ**:
    - Nhận yêu cầu từ **EmployeeForm** để tạo một nhân viên mới.
    - Kiểm tra thông tin nhập vào (đảm bảo hợp lệ).
    - Tạo một đối tượng **Employee** (Entity) với thông tin đã cung cấp.
    - Gửi yêu cầu lưu đối tượng **Employee** vào cơ sở dữ liệu thông qua lớp **Database**.
    - Gửi phản hồi (thành công hoặc thất bại) về **EmployeeForm** để hiển thị cho **Admin**.

#### 1.2.3. Entity
- **Employee**
  - **Vai trò**: Đại diện cho thông tin của một nhân viên trong hệ thống.
  - **Thuộc tính**:
    - `employeeID`: Mã định danh duy nhất của nhân viên.
    - `name`: Tên của nhân viên.
    - `address`: Địa chỉ của nhân viên.
    - `position`: Vị trí công việc của nhân viên.
    - `salary`: Mức lương cơ bản của nhân viên.
  - **Nhiệm vụ**:
    - Lưu trữ thông tin cá nhân và chi tiết công việc của nhân viên.

- **Database**
  - **Vai trò**: Cơ sở dữ liệu chứa thông tin của các nhân viên.
  - **Thuộc tính**:
    - `connection`: Kết nối tới cơ sở dữ liệu.
  - **Nhiệm vụ**:
    - Lưu trữ thông tin của nhân viên vào cơ sở dữ liệu.
    - Trả về kết quả (thành công hoặc thất bại) khi yêu cầu lưu thông tin được thực hiện.

---

## 1.3. Biểu đồ lớp với các lớp Boundary, Control, Entity



---


# Phân tích ca sử dụng "Maintain Purchase Order" trong Payroll System

## 1. Phân tích các lớp

### 1.1. Các loại lớp
- **Boundary**: Đại diện cho giao diện người dùng và các điểm tương tác với hệ thống.
- **Control**: Điều phối luồng hoạt động của hệ thống, xử lý logic và điều khiển giữa các lớp.
- **Entity**: Lưu trữ thông tin dữ liệu và thể hiện các đối tượng trong hệ thống.

### 1.2. Các lớp trong ca sử dụng "Maintain Purchase Order"

#### 1.2.1. Boundary
- **PurchaseOrderForm**
  - **Vai trò**: Là giao diện mà **Employee** hoặc **Payroll Administrator** sử dụng để tạo, cập nhật, và xem chi tiết đơn đặt hàng.
  - **Nhiệm vụ**:
    - Nhận thông tin đầu vào từ **Employee** hoặc **Payroll Administrator**.
    - Gửi yêu cầu tạo hoặc cập nhật đơn đặt hàng đến **PurchaseOrderManager** (Control).
    - Hiển thị kết quả (thành công hoặc thất bại) của quá trình tạo hoặc cập nhật đơn đặt hàng cho người dùng.

#### 1.2.2. Control
- **PurchaseOrderManager**
  - **Vai trò**: Điều phối quá trình tạo và duy trì đơn đặt hàng.
  - **Nhiệm vụ**:
    - Nhận yêu cầu từ **PurchaseOrderForm** để tạo mới hoặc cập nhật đơn đặt hàng.
    - Kiểm tra tính hợp lệ của thông tin nhập vào.
    - Tạo hoặc cập nhật đối tượng **PurchaseOrder** (Entity) với thông tin đã cung cấp.
    - Gửi yêu cầu lưu hoặc cập nhật đối tượng **PurchaseOrder** vào cơ sở dữ liệu thông qua lớp **Database**.
    - Gửi phản hồi (thành công hoặc thất bại) về **PurchaseOrderForm** để hiển thị cho người dùng.

#### 1.2.3. Entity
- **PurchaseOrder**
  - **Vai trò**: Đại diện cho thông tin của một đơn đặt hàng trong hệ thống.
  - **Thuộc tính**:
    - `orderID`: Mã định danh duy nhất của đơn đặt hàng.
    - `employeeID`: Mã định danh của nhân viên tạo đơn đặt hàng.
    - `items`: Danh sách các mặt hàng trong đơn đặt hàng.
    - `quantities`: Số lượng của từng mặt hàng.
    - `totalAmount`: Tổng tiền của đơn đặt hàng.
    - `orderDate`: Ngày tạo đơn đặt hàng.
  - **Nhiệm vụ**:
    - Lưu trữ thông tin chi tiết của đơn đặt hàng.
    - Cung cấp các phương thức để tính toán tổng tiền và cập nhật trạng thái đơn đặt hàng.

- **Database**
  - **Vai trò**: Cơ sở dữ liệu chứa thông tin của các đơn đặt hàng.
  - **Thuộc tính**:
    - `connection`: Kết nối tới cơ sở dữ liệu.
  - **Nhiệm vụ**:
    - Lưu hoặc cập nhật thông tin của đơn đặt hàng vào cơ sở dữ liệu.
    - Trả về kết quả (thành công hoặc thất bại) khi yêu cầu lưu hoặc cập nhật thông tin được thực hiện.

---

## 1.3. Biểu đồ lớp với các lớp Boundary, Control, Entity



