
## Thiết kế lớp 
#### 1. BankSystem
##### Xác định các operations 
  - deposit(Paycheck, BankInformation): Gửi yêu cầu nạp tiền vào tài khoản.
  - getAmount(): Lấy số tiền từ paycheck.
  - create(Deposit, paycheckAmount, BankInformation.routingNumber): Tạo giao dịch mới.
  - submit(BankTransaction): Gửi giao dịch tới giao diện hệ thống ngân hàng.
  - submit(BankTransaction): Xác nhận và thực thi giao dịch trong hệ thống ngân hàng.

![Operations](https://www.planttext.com/api/plantuml/png/V98zJiGm48NxESKeLP0M3f02BJzD6a222tYziy7QU1pPasA5E1a5H-8AE752WXVHnPxtlVV6ojV7vpQ8yjBR5iH8I_ZOaLTY70SqZFMjukFpAGZPgjfJvu8H0AN5URnh3R6W2cZJ9tZIehY9BWk6Ru2u38edTTAlf8_50Cw7tv81Vl6AGyo9HKPbTdSEfBIQXVn1QVg1idju1vZgukNrkcU5qtxbt6epZci-E6_79xc0bJxIip2o3ScDTJrBcOkovb6hFIcXyZx5RR2RR9B1MUgLTxqORXvwkoF_btssOum8_Sx6JRBiDRkeeyduWfW6nJyuR8dtmx_o3G00__y30000)

##### Xác định các trạng thái
  - Paycheck:
    - Initialized: Được khởi tạo với số tiền cụ thể.
    - Processed: Đã được sử dụng để tạo giao dịch nạp tiền.
  - BankTransaction:
    - Created: Giao dịch được khởi tạo.
    - Submitted: Giao dịch được gửi tới hệ thống ngân hàng.
    - Completed: Giao dịch hoàn thành thành công.
    - Failed: Giao dịch thất bại.
   
![Status](https://www.planttext.com/api/plantuml/png/T991JiCm44NtESMiaNg1B515fKfTKIb8B10BrvxGeR4TnXEgWZWP2ux45R2TL7L0xEoPzyV_Z_pz-RKCebW6srL2qY4qeWG3-1OsDyeTcbCGj72xUqOjeQf2QiDMdVGUzG7UAu27gqTOBAvXuqX8TVI61cgWudOasOEoVd0I-P9BkYrxZI5arGW1ep3XAvhgu_naCdF7oWMbXRoRlRnYZ8Y9bUcKgysmioIIvqgX39XjNDfvXBTzXoCS1fqC_M7MYheC8BFdkRLfJxDzcBZE6eugndLFq7gEkLu63996vsuHFo4rz9UBmTu7IauB8Wdknu5hpollMcAhSgnV8S_Ee_uVGU5HbtL6ZJJjVedEfB_n0m00__y30000)

##### Xác định các thuộc tính
- Paycheck: Chứa số tiền và thông tin nhân viên.
- BankInformation: Gồm tên ngân hàng và mã định tuyến.
- BankTransaction: Chứa số tiền giao dịch, loại giao dịch, và mã định tuyến.

![Attributes](https://www.planttext.com/api/plantuml/png/T95BJWCn38RtEOKlC1UeK5KGcv4GK9KBvE6MqCIfOdinGfoC1KVY2cHAWNPQTeaVts___dp_MB3OAfgJaIW9uLgaHgU236KD_OsbxMfWmGmFxWMzi34-MMPuj8D_Hh-5LmFGWSr5IM06eQXBk8y5AzWpAuOMlsqVy_RJFN9xMfUQhSH21qWjAf4szveTrjQpQhFGvfll_IWmJPq0dwebjlu8A7-HFfm2PTZXHEB22iqTKVv7xs3CcTHIKKVsNMIvcWmstnVx597aUAG6_dMqw-Pd-yn0kVde1ZErxd9rm1rIQ4SaOnRjDLxu2m00__y30000)

##### Xác định các phụ thuộc

![Dependencies](https://www.planttext.com/api/plantuml/png/T55BRi8m4Dtx5AEiO94Bi42eOfDTLRZ0u4oBXMCZpnW98Kx6WYFr2hNJ88VGBltylfhlstt5Wa5YPvKOiGGVP56CTxmtHmRZe7b3TzYSMQXJIbjaXeB0HG7KS0nU4_Cse6FKMJwRznydjAP5eNSywptfGuAl3vS7DdXWvwCJM43huyvIZsLfmnofJVWwFOewTnZb3IPIa2PhDXAC--g_qaw9NB3hwvh62OLFr3IuSTnrHfvN9TbeVbqlouu5L969gobXMZNnTA2qvc_gj4kY_nPX45-DumlddvZXBZb8hSYr-Sm_0000__y30000)

#### 2. BankSystem
##### Xác định các operations
- PrintService:
  - print(Paycheck, String): Nhận yêu cầu in từ Client
  - create(Paycheck): Tạo đối tượng hình ảnh cần in từ thông tin Paycheck
- PaycheckPrinterImage:
  - buildPrintImage(): Tạo hình ảnh in từ Paycheck
  - getEmployee(), getEmployeeName(), getEmployeeID(): Lấy thông tin nhân viên từ Paycheck
  - getAmount(): Lấy số tiền cần in từ Paycheck
- PrinterInterface:
  - print(theImage): Gửi hình ảnh tới máy in.
  - submit(): Yêu cầu máy in thực hiện in.
 
![Operations](https://www.planttext.com/api/plantuml/png/b991Ri8m44NtSueHAv3e1RAegA2BRA0I9nYvqs0HEv4pL49LJzP5ZzGhr0aus60gTMF9y__xcXdxv-jxqGavEPWQH4lDk6dPaUZ6TgWjbYzEMzcoUzUAYwBjRm2af76uh3LRGUemDfsgu5W9sSe7nY9-0E95cWmQkx8_taZnP4oBYbS87TMErJwu35LdB2EawBDfw-R89tkuvDEJHFW4k1qH7nxJsGeSrZCDs1otuWlLB847BDEgnvLZ4Xvvp-Ly4U-PYYLCChqF14iAhCdy7ofNVo1fOq-cEVXzPEQ_Uk5nTRBZ8UkCn9OBDhfd00ksh_tV_GK00F__0m00)

##### Xác định các trạng thái
- PaycheckPrinterImage:
  - Initialized: Đối tượng được khởi tạo.
  - Built: Hình ảnh in được tạo xong.
  - Ready: Hình ảnh sẵn sàng để in.
- Printer:
  - Idle: Máy in ở trạng thái chờ.
  - Printing: Máy in đang xử lý lệnh in.
  - Completed: Lệnh in hoàn thành.
 
![States](https://www.planttext.com/api/plantuml/png/L90nJWGn34NxdC8rqbvW2xIYcueHMoAAa7Xt39bav7XOBOYJKN0ahe2TGQEXYYA___ESdw_lGnNFCe_92Kb2E8eNh51EqFLCMOx8RnGGxfzVC4XrhXe0lR-60SDhOv2xqPyHFXp0uyqJx7Qtq6KIyedUCS8U0gEc8bn8XZMhz9QorDrCIPIdrXTAhi9pqAIooyoe1_JngXItyrGO9jEWV7QVg-0Yzjyfwe9xk7WojWL36KUVhRuDZUh_kfISk0IirIuouFBA9hAIctATJWdDM5KEcADzxIy0003__mC0)

##### Xác định các thuộc tính
- Paycheck:
  - amount: Số tiền cần in (kiểu double).
  - issuedTo: Nhân viên nhận lương (đối tượng Employee).
- Employee:
  - employeeId: Mã nhân viên (kiểu String).
  - employeeName: Tên nhân viên (kiểu String).
- PaycheckPrinterImage:
  - image: Dữ liệu hình ảnh cần in (kiểu byte[]).
  - status: Trạng thái của hình ảnh (kiểu String).
- Printer:
  - printerId: Mã định danh máy in.
  - printerStatus: Trạng thái của máy in.

![Atributes](https://www.planttext.com/api/plantuml/png/R94nRiCm34LtdO8Ny0Ky1EdGmKiJmDsA3hByawgLh42a2XX5JfOXH-eLeZXoWgRPo2V-Zq_gzt1SikWeoJibLXpeIIJQBWcOmeQQTRI3j8ZVre1MtIUCi5B6QMPQwz5ym7pHZoAgIFkG1g6Q-f0wXubPveJ-DMJwx7SkZ83Qp_gP53rAs_HvkiqfXkqV_g8zRY_x-nHJKiJ6w-tiQAUwfcuKlBrFA6yhYH_PNEH5kIjcTr4ARl-RN6zHLOlROZL5R12P9AY7ES_JLsbDYP6lkyJGdp_a1000__y30000)

##### Xác định các phụ thuộc

![Dependecies](https://www.planttext.com/api/plantuml/png/R94nRiCm34LtdO8Ny0Ky1EdGmKiJmDsA3hByawgLh42a2XX5JfOXH-eLeZXoWgRPo2V-Zq_gzt1SikWeoJibLXpeIIJQBWcOmeQQTRI3j8ZVre1MtIUCi5B6QMPQwz5ym7pHZoAgIFkG1g6Q-f0wXubPveJ-DMJwx7SkZ83Qp_gP53rAs_HvkiqfXkqV_g8zRY_x-nHJKiJ6w-tiQAUwfcuKlBrFA6yhYH_PNEH5kIjcTr4ARl-RN6zHLOlROZL5R12P9AY7ES_JLsbDYP6lkyJGdp_a1000__y30000)

#### 3. ProjectManagementDatabase
##### Xác định các operations
- ProjectManagementDatabase:
  - Phương thức getChargeNumbers(String): Bắt đầu quy trình bằng cách nhận một tham số dạng chuỗi (string), có thể là tên dự án hoặc mã liên quan.
- DBChargeNumber:
  - getChargeNums(String): Lấy thông tin charge numbers từ cơ sở dữ liệu.
  - createStatement() và executeQuery(String): Hai phương thức quan trọng cho việc truy vấn cơ sở dữ liệu.
  - add(ChargeNum): Thêm một charge number vào danh sách.

![operations](https://www.planttext.com/api/plantuml/png/X59BJiCm4Dtx56RdIlG2LHKLw18gIaumSHuXA76GFIuWnCbOS2IkG4ARRntXXMLvtiVpnZzVtnl7PDcNXRX8yPWRoAl4iINDShscqp6AXD05EIVlRVKCpNTaA4C9mrjYIiX1VWZPh0nyyqGsmywN2QnJCTlSP0lnsKfihqU04B5d_PMq1J5YhhV6KfskyGRj6NiF-pucK9ggJcnWtTtTvevRut_1BT3WLRqS-zzHYKjveC9Zm7Y0ymN7u45FntUf0Qhhe_MfZAabyye8CH_lSXcT9RUQJtiARUYTSKqyZxIlXgs2QOTi-XGcf8NeIxFjT7c5fCVpMqr7DowF23LuRdmRcBJv_xy0003__mC0)

##### Xác định các trạng thái
- DBChargeNumbers:
  - Khi nhận được chuỗi đầu vào từ ProjectManagementDatabase.
  - Sau khi thực hiện createStatement() hoặc executeQuery().
- ResultSet:
  - Khi gọi getString() để lấy kết quả truy vấn.
- ChargeNumList:
  - Trước và sau khi thêm dữ liệu bằng add(ChargeNum).

![States](https://www.planttext.com/api/plantuml/png/N95D2W8n38NtFKMObGfUm8KCg3iHdLcAYp8JL9W_sXJqR2uyabUmwJI3TLEIB--55_fvlNDBsf1h6-KBGiXAxZFG5a8b-EJGFE5eSD06wp0FI4YgspsmSlIh4oAwhIRjr_KLMXjrZ2OYkWAjQmWA96UwA1oP8ANEYmiib-iOEBoXJmB22Yg3VcV9YrliQ3PNgMBoI5ZlmR4CM0pJc0r9Qc-8TGnP8gbKmPxq03RrWslutirDcoiUNBk_Mr9_EhRwMrMENSq_zWK00F__0m00)

##### Xác định các thuộc tính
- ProjectManagementDatabase: Không thấy trực tiếp các thuộc tính, nhưng có thể có thuộc tính như thông tin kết nối database.
- DBChargeNumbers:
  - projectName: tên dự án hiện tại đang xử lý.
  - value: dữ liệu liên quan đến charge numbers.
- ChargeNum: Có thể bao gồm các thuộc tính như id, amount hoặc description của charge numbers.
- ChargeNumList: Là một danh sách (collection) lưu nhiều ChargeNum.

![Attributes](https://www.planttext.com/api/plantuml/png/V51B2i8m4Dtd5Bb0Bo1IHBlK8dY2QJhKI38foSIDU38N7iahc51RR46po_lDl7azdfl0u3bQ8vI14EJHkmigFW11XnQ9As1e8A2y2PbUeHnH4cX7uYu-fcgxEuFli8wsGHz6QJzarM1HhkI9lQPkOAvWuXSs1KqnOuHkaqeJ3p-mBX8df7MnCJY0BGRbTPyt-fUuru6d3YCOaYCJwqbMPkll8nH5kMmhbkspPZPMp9UOyMA3rERplm400F__0m00)

##### Xác định các phụ thuộc

![Dependencies](https://www.planttext.com/api/plantuml/png/V95D3e8m44RtFKMNkl02BWmHbcgCd620iTP0QsO6DyQJkV18Ni524F_Gxjg-xvlNz7QvHYn0KbUboajWrcloUynb2GuCLkWa0O4C6FL9wMOPb7W7P71LLnaIZr8XwynOdLLNaSpVWA7WG2eLa7PWju-zSq74UjSTR93hKbBiWKVPmh8ezLjyCfbzEKrrWGTq1UlG_tdP17gTWDQCF0Wz7VzHlNY027EqHsHT13kz9LyD5x--BSHOF8KGjKsihLDHa6z-xGu00F__0m00)
