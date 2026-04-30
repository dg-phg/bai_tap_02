# HQTCSDL_DTAP_BT2
## Thông tin sinh viên:
+ **Họ và tên:** Dương Thị Anh Phương 
+ **Mã sinh viên:** K235480106056
+ **Lớp:** K59.KMT.K01
+ **Trường:** Đại học Kỹ thuật Công nghiệp Thái Nguyên

---
## BÀI TẬP SỐ 2
### Phần 1: Thiết kế và khởi tạo Cấu trúc dữ liệu 
#### 1. Chọn chủ đề quản lý: _Quản lý khách sạn_
   
1.1 Khởi tạo Database với tên dự án và Mã Sinh Viên: `QuanLyKhachSan_K235480106056`
   
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6b42166e-1fc8-4757-af0d-2cd10915d173" />

1.2 Tạo bảng Khách hàng 
   
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/79cc4800-92d6-4776-b2c8-3957976ac4b0" />

+ PK: [MaKhachHang]
  
=> Cấu trúc bảng `KhachHang` với các kiểu dữ liệu Unicode và Số thực

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bb34265d-3d78-425a-bea7-2995a7bdf3db" />

1.3 Tạo bảng `Phong`
   
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/22a59b1e-6834-4a71-9a66-63f3cea9ec29" />

+ PK: [MaPhong]
  
+ CK: [GiaTheoNgay]
  
=>Cấu trúc bảng `Phong` với kiểu dữ liệu Tiền tệ và mã phòng kiểu Chuỗi

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9d4b8c29-b7d2-4a9f-847c-a89509eafe8f" />

1.4 Tạo bảng `DatPhong`và thêm các khóa liên kết tới 2 bảng trên
   
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4f00099c-4381-4016-90b4-fe2302e0046a" />

PK: [MaDatPhong]

FK: [MaKhachHang] ; [MaPhong]

CK: [CK_ThoiGian]

=> Cấu trúc bảng [DatPhong] và thiết lập các mối liên kết

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5993ec3f-d46f-4b92-9b7f-e6cdeb97d093" />

#### Giải thích các ràng buộc dữ liệu:

+ Khóa chính (Primary Key - PK):

[MaKhachHang], [MaDatPhong]: Là các số nguyên tự động tăng (IDENTITY), giúp định danh duy nhất mỗi khách hàng và mỗi lượt đặt phòng.

[MaPhong]: Dùng mã định danh dạng chuỗi (ví dụ: 'P101') để quản lý phòng theo sơ đồ thực tế.

+ Khóa ngoại (Foreign Key - FK):

Bảng [DatPhong] chứa hai khóa ngoại là [MaKhachHang] và [MaPhong]. Điều này tạo ra mối quan hệ: "Một khách hàng có thể đặt nhiều phòng" và "Một phòng có thể được đặt bởi nhiều khách hàng tại các thời điểm khác nhau".

+ Ràng buộc kiểm tra (Check Constraint - CK):

[CK_GiaPhong]: Đảm bảo trường [GiaTheoNgay] luôn phải lớn hơn 0, tránh nhập liệu sai về tài chính.

[CK_ThoiGian]: Đảm bảo [NgayTraPhong] không được trước [NgayNhanPhong], logic nghiệp vụ bắt buộc trong quản lý khách sạn.

1.5 Sơ đồ `Database Diagram` của hệ thống _Quản lý Khách sạn_, thể hiện trực quan các `Khóa chính` (PK - Chìa khóa vàng) và các đường liên kết `Khóa ngoại` (FK) giữa 3 bảng.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fb43b616-a0ab-4f44-9fe9-5efa1bbe34cf" />

### Phần 2: Xây dựng FUNCTION (hàm)

2.1 Các loại Function Built-in (Hàm có sẵn) trong _SQL Server_

Trong SQL Server, các hàm có sẵn được thiết kế để thực hiện các tính toán hoặc thao tác dữ liệu nhanh chóng. Chúng được chia thành các nhóm chính sau:

+ Hàm xử lý chuỗi (String Functions): Thao tác với văn bản (Ví dụ: LEN(), UPPER(), SUBSTRING(), LTRIM()).

+ Hàm ngày tháng (Date and Time Functions): Xử lý các giá trị thời gian (Ví dụ: GETDATE(), DATEDIFF(), DATEADD(), DAY(), MONTH()).

+ Hàm toán học (Mathematical Functions): Tính toán số học (Ví dụ: ROUND(), ABS(), POWER()).

+ Hàm tổng hợp (Aggregate Functions): Tính toán trên một tập hợp dữ liệu và trả về một giá trị duy nhất (Ví dụ: SUM(), COUNT(), MAX(), MIN(), AVG()).

+ Hàm chuyển đổi (Conversion Functions): Chuyển đổi giữa các kiểu dữ liệu (Ví dụ: CAST(), CONVERT(), FORMAT()).

2.2 Các hàm Built-in đặc sắc (Góc nhìn cá nhân)
Đối với bài toán Quản lý Khách sạn mà em đang xây dựng, em thấy 3 hàm sau đây là đặc sắc và hữu dụng nhất để giải quyết các logic thực tế:

+ DATEDIFF(datepart, startdate, enddate): Hàm này cực kỳ quan trọng để tính khoảng cách giữa 2 mốc thời gian. Trong quản lý khách sạn, nó giúp em tự động tính ra số ngày khách thuê phòng dựa trên Ngày nhận và Ngày trả, từ đó mới nhân lên được thành tiền.

+ FORMAT(value, format, culture): Hàm này giúp định dạng dữ liệu hiển thị cực kỳ thẩm mỹ. Em dùng nó để định dạng giá tiền thành chuẩn tiền tệ Việt Nam (VNĐ) có dấu chấm phân cách hàng nghìn, và định dạng lại ngày tháng theo chuẩn Việt Nam (dd/MM/yyyy).

+ UPPER(string): Hàm chuyển chuỗi thành CHỮ IN HOA. Rất phù hợp để in chuẩn hóa tên Khách hàng trên các hóa đơn thanh toán.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/28e3c81c-16dc-4097-9e41-d65906c94c69" />




  
