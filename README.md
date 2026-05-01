# HQTCSDL_DTAP_BT2
## Thông tin sinh viên:
+ **Họ và tên:** Dương Thị Anh Phương 
+ **Mã sinh viên:** K235480106056
+ **Lớp:** K59.KMT.K01
+ **Trường:** Đại học Kỹ thuật Công nghiệp Thái Nguyên

---
## BÀI TẬP SỐ 2
### Phần 1: Thiết kế và khởi tạo Cấu trúc dữ liệu 

**Chủ đề:** Quản lý Khách sạn

---

#### 1.1. Khởi tạo Database
Tạo cơ sở dữ liệu với tên dự án và gắn kèm Mã Sinh Viên: `QuanLyKhachSan_K235480106056`

*Ảnh: Khởi tạo Database*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6b42166e-1fc8-4757-af0d-2cd10915d173" />

---

#### 1.2. Tạo bảng Khách Hàng (`KhachHang`)
* **Khóa chính (PK):** `[MaKhachHang]`
* **Mô tả:** Cấu trúc bảng `KhachHang` được thiết lập với các kiểu dữ liệu Unicode (để lưu họ tên tiếng Việt) và kiểu Số.

*Ảnh: Lệnh tạo bảng Khách Hàng*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/79cc4800-92d6-4776-b2c8-3957976ac4b0" />

*Ảnh: Cấu trúc bảng Khách Hàng*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/bb34265d-3d78-425a-bea7-2995a7bdf3db" />

---

#### 1.3. Tạo bảng Phòng (`Phong`)
* **Khóa chính (PK):** `[MaPhong]`
* **Ràng buộc kiểm tra (CK):** `[GiaTheoNgay]`
* **Mô tả:** Cấu trúc bảng `Phong` sử dụng kiểu dữ liệu Tiền tệ cho giá phòng và mã phòng lưu ở dạng Chuỗi.

*Ảnh: Lệnh tạo bảng Phòng*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/22a59b1e-6834-4a71-9a66-63f3cea9ec29" />

*Ảnh: Cấu trúc bảng Phòng*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9d4b8c29-b7d2-4a9f-847c-a89509eafe8f" />

---

#### 1.4. Tạo bảng Đặt Phòng (`DatPhong`) và thiết lập liên kết
* **Khóa chính (PK):** `[MaDatPhong]`
* **Khóa ngoại (FK):** `[MaKhachHang]`, `[MaPhong]`
* **Ràng buộc kiểm tra (CK):** `[CK_ThoiGian]`

*Ảnh: Lệnh tạo bảng Đặt Phòng và thêm khóa liên kết*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/4f00099c-4381-4016-90b4-fe2302e0046a" />

*Ảnh: Cấu trúc bảng Đặt Phòng*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5993ec3f-d46f-4b92-9b7f-e6cdeb97d093" />

**Giải thích chi tiết các ràng buộc dữ liệu (Constraints):**
* **Khóa chính (Primary Key - PK):** Cột `[MaKhachHang]` và `[MaDatPhong]` được thiết lập là các số nguyên tự động tăng (`IDENTITY`), giúp định danh duy nhất mỗi khách hàng và mỗi lượt đặt phòng. Riêng cột `[MaPhong]` dùng mã định danh dạng chuỗi (ví dụ: 'P101') để quản lý phòng trực quan theo sơ đồ thực tế.
* **Khóa ngoại (Foreign Key - FK):** Bảng `DatPhong` chứa hai khóa ngoại là `[MaKhachHang]` và `[MaPhong]`. Cấu trúc này tạo ra mối quan hệ nhiều-nhiều: "Một khách hàng có thể đặt nhiều phòng" và "Một phòng có thể được đặt bởi nhiều khách hàng tại các mốc thời điểm khác nhau".
* **Ràng buộc kiểm tra (Check Constraint - CK):**
    * `[CK_GiaPhong]`: Đảm bảo trường `[GiaTheoNgay]` luôn phải có giá trị lớn hơn 0, tránh việc nhập liệu sai sót về mặt tài chính.
    * `[CK_ThoiGian]`: Đảm bảo `[NgayTraPhong]` không được diễn ra trước `[NgayNhanPhong]`, đây là logic nghiệp vụ bắt buộc phải có trong quản lý khách sạn.

---

#### 1.5. Sơ đồ cơ sở dữ liệu (Database Diagram)
Sơ đồ hệ thống Quản lý Khách sạn thể hiện trực quan các Khóa chính (PK - Biểu tượng chìa khóa vàng) và các đường liên kết Khóa ngoại (FK) giữa 3 bảng dữ liệu.

*Ảnh: Database Diagram*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fb43b616-a0ab-4f44-9fe9-5efa1bbe34cf" />

### Phần 2: Xây dựng FUNCTION (hàm)

#### 2.1. Các loại Function Built-in (Hàm có sẵn) trong SQL Server
Trong SQL Server, các hàm có sẵn được thiết kế để thực hiện các tính toán hoặc thao tác dữ liệu nhanh chóng. Chúng được chia thành các nhóm chính sau:
* **Hàm xử lý chuỗi (String Functions):** Thao tác với văn bản (Ví dụ: `LEN()`, `UPPER()`, `SUBSTRING()`, `LTRIM()`).
* **Hàm ngày tháng (Date and Time Functions):** Xử lý các giá trị thời gian (Ví dụ: `GETDATE()`, `DATEDIFF()`, `DATEADD()`, `DAY()`, `MONTH()`).
* **Hàm toán học (Mathematical Functions):** Tính toán số học (Ví dụ: `ROUND()`, `ABS()`, `POWER()`).
* **Hàm tổng hợp (Aggregate Functions):** Tính toán trên một tập hợp dữ liệu và trả về một giá trị duy nhất (Ví dụ: `SUM()`, `COUNT()`, `MAX()`, `MIN()`, `AVG()`).
* **Hàm chuyển đổi (Conversion Functions):** Chuyển đổi giữa các kiểu dữ liệu (Ví dụ: `CAST()`, `CONVERT()`, `FORMAT()`).

**Các hàm Built-in đặc sắc (Góc nhìn cá nhân):**
Đối với bài toán Quản lý Khách sạn mà em đang xây dựng, em thấy 3 hàm sau đây là đặc sắc và hữu dụng nhất để giải quyết các logic thực tế:
* **`DATEDIFF(datepart, startdate, enddate)`**: Hàm này cực kỳ quan trọng để tính khoảng cách giữa 2 mốc thời gian. Trong quản lý khách sạn, nó giúp em tự động tính ra số ngày khách thuê phòng dựa trên Ngày nhận và Ngày trả, từ đó mới nhân lên được thành tiền.
* **`FORMAT(value, format, culture)`**: Hàm này giúp định dạng dữ liệu hiển thị cực kỳ thẩm mỹ. Em dùng nó để định dạng giá tiền thành chuẩn tiền tệ Việt Nam (VNĐ) có dấu chấm phân cách hàng nghìn, và định dạng lại ngày tháng theo chuẩn Việt Nam (dd/MM/yyyy).
* **`UPPER(string)`**: Hàm chuyển chuỗi thành CHỮ IN HOA. Rất phù hợp để in chuẩn hóa tên Khách hàng trên các hóa đơn thanh toán.

**Code SQL khai thác các hàm Built-in:**
```sql
USE [QuanLyKhachSan_K235480106056];
GO

SELECT 
    dp.[MaDatPhong],
    UPPER(kh.[HoVaTen]) AS [TenKhachHang_VietHoa],
    FORMAT(dp.[NgayNhanPhong], 'dd/MM/yyyy') AS [NgayNhan_VN],
    FORMAT(dp.[NgayTraPhong], 'dd/MM/yyyy') AS [NgayTra_VN],
    DATEDIFF(DAY, dp.[NgayNhanPhong], dp.[NgayTraPhong]) AS [SoNgayThue],
    FORMAT(dp.[TongTien], 'C0', 'vi-VN') AS [TongTien_VND]
FROM [DatPhong] dp
JOIN [KhachHang] kh ON dp.[MaKhachHang] = kh.[MaKhachHang];
```

*Ảnh 1: Nhập dữ liệu*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/28e3c81c-16dc-4097-9e41-d65906c94c69" />

*Ảnh 2: Khai thác các hàm Built-in định dạng dữ liệu khách sạn*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/171cb8c0-a031-49fe-9fe4-404593be590e" />

---

#### 2.2. Hàm do người dùng tự viết (User-Defined Functions - UDFs)
* **Mục đích:** Đóng gói các đoạn logic tính toán, xử lý nghiệp vụ đặc thù của ứng dụng để tái sử dụng nhiều lần, giúp code gọn gàng, tránh lặp lại và dễ bảo trì.
  
* **Tại sao có Built-in rồi vẫn cần tự viết hàm riêng?** Các hàm hệ thống chỉ giải quyết các tác vụ tính toán chung chung. Mỗi doanh nghiệp lại có những "luật" và nghiệp vụ riêng biệt. Ví dụ: Khách sạn quy định "Nhận và trả phòng trong cùng 1 ngày vẫn tính là 1 ngày". Nếu dùng hàm hệ thống `DATEDIFF` thì sẽ ra `0` ngày, dẫn đến sai tiền. Ta bắt buộc phải tự viết hàm để xử lý logic này.
  
* **Phân loại UDF:**
    1. **Scalar Function (Hàm vô hướng):** Trả về 1 giá trị duy nhất. Dùng cho công thức tính toán đơn lẻ.
    2. **Inline Table-Valued Function (ITVF):** Trả về 1 bảng từ 1 câu `SELECT`. Dùng để lọc dữ liệu nhanh.
    3. **Multi-statement Table-Valued Function (MSTVF):** Trả về 1 bảng nhưng cho phép dùng biến bảng và viết nhiều lệnh xử lý phức tạp (`IF`, `WHILE`...) ở bên trong.

---

#### 2.3. Viết 01 Scalar Function (Hàm vô hướng)
* **Yêu cầu nghiệp vụ của hàm (Tự nghĩ):** Viết hàm tính số ngày thuê thực tế của một lượt đặt phòng. Nếu khách nhận và trả phòng trong cùng 1 ngày, hệ thống tự động làm tròn thành 1 ngày để tính tiền.
* **Mã nguồn tạo hàm:**
```sql
USE [QuanLyKhachSan_K235480106056];
GO

CREATE FUNCTION [fn_TinhSoNgayThue] (@NgayNhan DATE, @NgayTra DATE)
RETURNS INT
AS
BEGIN
    DECLARE @SoNgay INT;
    SET @SoNgay = DATEDIFF(DAY, @NgayNhan, @NgayTra);
    IF @SoNgay = 0 
        SET @SoNgay = 1; -- Cùng ngày thì làm tròn tính là 1 ngày
    RETURN @SoNgay;
END;
GO
```
* **Câu lệnh khai thác hàm:**
```sql
SELECT 
    [MaDatPhong], 
    [NgayNhanPhong], 
    [NgayTraPhong],
    dbo.fn_TinhSoNgayThue([NgayNhanPhong], [NgayTraPhong]) AS [SoNgayThueThucTe]
FROM [DatPhong];
```

*Ảnh 3: Khởi tạo và truy vấn hàm vô hướng (Scalar Function) tính số ngày thuê thực tế.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a2748517-07c0-4dc8-a6cd-18aeb8523228" />

#### 2.4. Viết 01 Inline Table-Valued Function (Hàm trả về bảng nội tuyến)

* **Yêu cầu nghiệp vụ của hàm:** Xây dựng một hàm nhận tham số đầu vào là Mã Khách Hàng (`@MaKH`), từ đó tự động liên kết dữ liệu giữa bảng `DatPhong` và `Phong` để lọc ra toàn bộ danh sách lịch sử đặt phòng của riêng vị khách đó. Hàm này trả về một bảng (Table) giúp nhân viên dễ dàng tra cứu thông tin nhanh chóng.
  
* **Mã nguồn tạo hàm:**

```sql
USE [QuanLyKhachSan_K235480106056];
GO

CREATE FUNCTION [fn_LichSuDatPhongCuaKhach] (@MaKH INT)
RETURNS TABLE
AS
RETURN (
    SELECT 
        dp.[MaDatPhong], 
        p.[MaPhong], 
        p.[LoaiPhong], 
        dp.[NgayNhanPhong], 
        dp.[NgayTraPhong], 
        dp.[TongTien]
    FROM [DatPhong] dp
    JOIN [Phong] p ON dp.[MaPhong] = p.[MaPhong]
    WHERE dp.[MaKhachHang] = @MaKH
);
GO
```

* **Câu lệnh khai thác hàm:**

```sql
-- Lọc lịch sử đặt phòng của khách hàng có Mã là 1
SELECT * FROM dbo.fn_LichSuDatPhongCuaKhach(1);
```

*Ảnh 4: Khởi tạo hàm Inline Table-Valued.*
<img width="1024" height="576" alt="image" src="https://github.com/user-attachments/assets/eb2b4c6a-565e-4314-8c69-b0afb0115be4" />

*Ảnh 5: Kết quả truy vấn hàm Inline Table-Valued để lấy lịch sử của Khách hàng có mã là 1.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8dd1e2cb-d953-4b79-a3fe-19953367db69" />


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2508bc8c-a05e-4c35-9164-f003da3d0511" />
