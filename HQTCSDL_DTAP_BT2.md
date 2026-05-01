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
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e2705615-e2aa-46ea-a71c-a965e0cd325c" />

*Ảnh 5: Kết quả truy vấn hàm Inline Table-Valued để lấy lịch sử của Khách hàng có mã là 1.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8dd1e2cb-d953-4b79-a3fe-19953367db69" />

#### 2.5. Viết 01 Multi-statement Table-Valued Function (Hàm trả về bảng đa câu lệnh - MSTVF)

* **Yêu cầu nghiệp vụ của hàm:** Viết một hàm thống kê tổng doanh thu của từng phòng trong một năm cụ thể (tham số đầu vào là `@Nam`). Điểm đặc biệt của hàm MSTVF là cho phép tạo một bảng ảo `@BangThongKe` để lưu trữ tạm thời dữ liệu tổng tiền. Sau đó, sử dụng tiếp các câu lệnh `UPDATE` kết hợp điều kiện để tự động phân loại phòng thành "Doanh thu cao" (>= 2,000,000) hoặc "Doanh thu trung bình" (< 2,000,000) trước khi trả về kết quả cuối cùng.
  
* **Mã nguồn tạo và khai thác hàm:**

```sql
USE [QuanLyKhachSan_K235480106056];
GO

-- 1. Lệnh tạo hàm
CREATE FUNCTION [fn_ThongKeDoanhThuPhong] (@Nam INT)
RETURNS @BangThongKe TABLE (
    [MaPhong] VARCHAR(10),
    [LoaiPhong] NVARCHAR(50),
    [TongDoanhThu] DECIMAL(18,2),
    [DanhGia] NVARCHAR(50)
)
AS
BEGIN
    -- Đưa dữ liệu tổng tiền vào bảng ảo
    INSERT INTO @BangThongKe ([MaPhong], [LoaiPhong], [TongDoanhThu])
    SELECT 
        p.[MaPhong], 
        p.[LoaiPhong], 
        SUM(dp.[TongTien])
    FROM [Phong] p
    JOIN [DatPhong] dp ON p.[MaPhong] = dp.[MaPhong]
    WHERE YEAR(dp.[NgayTraPhong]) = @Nam
    GROUP BY p.[MaPhong], p.[LoaiPhong];

    -- Dùng lệnh UPDATE để tự động phân loại đánh giá
    UPDATE @BangThongKe
    SET [DanhGia] = N'Doanh thu cao'
    WHERE [TongDoanhThu] >= 2000000;

    UPDATE @BangThongKe
    SET [DanhGia] = N'Doanh thu trung bình'
    WHERE [TongDoanhThu] < 2000000;

    RETURN;
END;
GO
-- 2. Thống kê doanh thu phòng và tự động đánh giá trong năm 2023
SELECT * FROM dbo.fn_ThongKeDoanhThuPhong(2023);
```

*Ảnh 6: Khởi tạo và truy vấn hàm Multi-statement Table-Valued (MSTVF) thống kê doanh thu phòng.*

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2508bc8c-a05e-4c35-9164-f003da3d0511" />

### Phần 3: Xây dựng Store Procedure

#### 3.1. Tìm hiểu System Stored Procedure có sẵn (Thủ tục lưu trữ)

SQL Server cung cấp một tập hợp các Stored Procedure hệ thống (System Stored Procedures) được lưu trữ trong cơ sở dữ liệu `master`. Chúng thường có tiền tố `sp_` và được sử dụng để hỗ trợ các tác vụ quản trị, giám sát hoặc trích xuất thông tin từ hệ thống. 

Một số System SP phổ biến:
* `sp_help`: Hiển thị thông tin chi tiết về cấu trúc của một đối tượng cơ sở dữ liệu (ví dụ: bảng, view).
* `sp_databases`: Liệt kê danh sách tất cả các cơ sở dữ liệu hiện có trong SQL Server.
* `sp_who`: Hiển thị thông tin về các người dùng và tiến trình đang kết nối vào hệ thống.

**Ví dụ khai thác:** Sử dụng `sp_help` để xem cấu trúc chi tiết của bảng `Phong`.
```sql
USE [QuanLyKhachSan_K235480106056];
GO

-- Khai thác SP có sẵn: sp_help để xem cấu trúc bảng Phong
EXEC sp_help 'Phong';
```
*Ảnh 8: Kết quả thực thi System Stored Procedure sp_help.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0d256974-a111-40fa-ab80-908f9bd8af2b" />

#### 3.2. Viết 01 Stored Procedure cập nhật dữ liệu có kiểm tra điều kiện logic
* **Yêu cầu nghiệp vụ của SP:** Tạo thủ tục `sp_CapNhatGiaPhong` để hỗ trợ nhân viên thay đổi giá phòng. Tham số đầu vào gồm Mã Phòng (`@MaP`) và Giá Mới (`@GiaMoi`). Thủ tục sẽ kiểm tra logic: Nếu giá mới <= 0, hệ thống sẽ in ra thông báo lỗi và từ chối cập nhật. Nếu giá hợp lệ, hệ thống sẽ thực hiện lệnh `UPDATE` và báo thành công.
* **Mã nguồn tạo SP và lệnh khai thác:**

```sql
USE [QuanLyKhachSan_K235480106056];
GO

-- 1. Lệnh tạo Stored Procedure
CREATE PROCEDURE [sp_CapNhatGiaPhong]
    @MaP VARCHAR(10),
    @GiaMoi DECIMAL(18,2)
AS
BEGIN
    -- Kiểm tra điều kiện logic
    IF @GiaMoi <= 0
    BEGIN
        PRINT N'LỖI: Giá phòng mới phải lớn hơn 0. Cập nhật thất bại!';
        RETURN;
    END

    -- Nếu hợp lệ thì tiến hành UPDATE
    UPDATE [Phong]
    SET [GiaTheoNgay] = @GiaMoi
    WHERE [MaPhong] = @MaP;

    PRINT N'THÀNH CÔNG: Đã cập nhật giá phòng mới!';
END;
GO

-- 2. Khai thác (Test) Stored Procedure
-- Test 1: Cố tình nhập giá sai (Âm tiền) để xem SP bắt lỗi
EXEC sp_CapNhatGiaPhong @MaP = 'P101', @GiaMoi = -50000;

-- Test 2: Nhập giá đúng để SP cập nhật
EXEC sp_CapNhatGiaPhong @MaP = 'P101', @GiaMoi = 650000;
```
*Ảnh 9: Kết quả kiểm tra (Test) các trường hợp đúng/sai của Stored Procedure cập nhật giá phòng.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e73974b0-9288-427c-b890-fea797ea345e" />

#### 3.3. Viết 01 Stored Procedure có sử dụng tham số OUTPUT
* **Yêu cầu nghiệp vụ của SP:** Viết thủ tục `sp_TinhTongTienKhachHang` nhận tham số đầu vào là Mã Khách Hàng (`@MaKH`). Thủ tục thực hiện truy vấn và trả về đồng thời 2 giá trị thông qua tham số `OUTPUT`: Tên của khách hàng (`@TenKH`) và Tổng số tiền người đó đã chi tiêu (`@TongChiTieu`). Điều này giúp ứng dụng lấy được dữ liệu tính toán trực tiếp mà không cần trả về toàn bộ một bảng lớn.
* **Mã nguồn tạo SP và lệnh khai thác:**

```sql
USE [QuanLyKhachSan_K235480106056];
GO

-- 1. Lệnh tạo Stored Procedure có 2 biến OUTPUT
CREATE PROCEDURE [sp_TinhTongTienKhachHang]
    @MaKH INT,
    @TenKH NVARCHAR(100) OUTPUT,
    @TongChiTieu DECIMAL(18,2) OUTPUT
AS
BEGIN
    -- Tìm tên khách hàng
    SELECT @TenKH = [HoVaTen] 
    FROM [KhachHang] 
    WHERE [MaKhachHang] = @MaKH;

    -- Tính tổng chi tiêu
    SELECT @TongChiTieu = SUM([TongTien])
    FROM [DatPhong]
    WHERE [MaKhachHang] = @MaKH;

    IF @TongChiTieu IS NULL
        SET @TongChiTieu = 0;
END;
GO

-- 2. Khai thác Stored Procedure
DECLARE @Tien_Output DECIMAL(18,2); 
DECLARE @Ten_Output NVARCHAR(100);

-- Gọi SP và đưa biến vào hứng kết quả
EXEC sp_TinhTongTienKhachHang 
    @MaKH = 1, 
    @TenKH = @Ten_Output OUTPUT,
    @TongChiTieu = @Tien_Output OUTPUT;

-- Hiển thị kết quả ra màn hình
SELECT 
    @Ten_Output AS [TenKhachHang],
    @Tien_Output AS [TongTienChiTieu];
```

*Ảnh 10: Khởi tạo và thực thi Stored Procedure có sử dụng tham số OUTPUT.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/14fa7f6e-33c5-4cdf-b229-58433b3811c2" />

#### 3.4. Viết 01 Stored Procedure trả về một tập kết quả (Result set) từ lệnh SELECT kết hợp JOIN nhiều bảng
* **Yêu cầu nghiệp vụ của SP:** Viết thủ tục sp_TraCuuThongTinDatPhong nhận tham số đầu vào là Loại phòng (@LoaiPhong). Thủ tục này có nhiệm vụ kết nối (JOIN) dữ liệu từ 3 bảng gồm DatPhong, KhachHang và Phong để trả về danh sách chi tiết các giao dịch đặt phòng tương ứng với loại phòng được yêu cầu, đi kèm thông tin liên hệ của khách hàng để nhân viên dễ dàng quản lý.

* **Mã nguồn tạo SP và lệnh khai thác:**

```SQL
USE [QuanLyKhachSan_K235480106056];
GO

-- 1. Lệnh tạo Stored Procedure JOIN 3 bảng
CREATE PROCEDURE [sp_TraCuuThongTinDatPhong]
    @LoaiPhong NVARCHAR(50)
AS
BEGIN
    SELECT 
        dp.[MaDatPhong],
        kh.[HoVaTen] AS [TenKhachHang],
        kh.[SoDienThoai],
        p.[MaPhong],
        p.[LoaiPhong],
        dp.[NgayNhanPhong],
        dp.[TongTien]
    FROM [DatPhong] dp
    JOIN [KhachHang] kh ON dp.[MaKhachHang] = kh.[MaKhachHang]
    JOIN [Phong] p ON dp.[MaPhong] = p.[MaPhong]
    WHERE p.[LoaiPhong] = @LoaiPhong;
END;
GO

-- 2. Khai thác (Test) Stored Procedure
EXEC sp_TraCuuThongTinDatPhong @LoaiPhong = N'Phòng VIP';
```
*Ảnh 11: Kết quả truy vấn Stored Procedure có sử dụng JOIN 3 bảng để tra cứu thông tin đặt phòng.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/af5e3fd9-be2d-475b-962c-ad048f3090fd" />

### Phần 4: Trigger và Xử lý logic nghiệp vụ

#### 4.1. Viết 01 Trigger tự động cập nhật dữ liệu liên bảng
* **Yêu cầu nghiệp vụ của SP:**  Thiết lập hệ thống tự động tích điểm thưởng thành viên. Mỗi khi có một đơn đặt phòng mới được thanh toán (dữ liệu được INSERT vào bảng DatPhong), hệ thống sẽ tự động tính toán điểm thưởng dựa trên tổng tiền (quy đổi 100.000 VNĐ = 1 điểm) và cộng dồn trực tiếp vào cột DiemTichLuy của khách hàng đó trong bảng KhachHang. Điều này giúp tăng tính tự động hóa và đảm bảo quyền lợi cho khách hàng thân thiết.

* **Mã nguồn tạo SP và lệnh khai thác:**
```
USE [QuanLyKhachSan_K235480106056];
GO

-- 1. Thêm cột DiemTichLuy vào bảng KhachHang (nếu chưa có) để chuẩn bị cho Trigger
IF NOT EXISTS (SELECT * FROM sys.columns WHERE object_id = OBJECT_ID(N'[dbo].[KhachHang]') AND name = 'DiemTichLuy')
BEGIN
    ALTER TABLE [KhachHang] ADD [DiemTichLuy] INT DEFAULT 0;
END
GO

-- 2. Lệnh tạo Trigger tự động tích điểm
CREATE TRIGGER trg_TichDiemKhachHang
ON [DatPhong]
AFTER INSERT
AS
BEGIN
    -- Lấy Tổng Tiền từ bản ghi vừa thêm (bảng inserted) để quy đổi điểm
    UPDATE kh
    SET kh.[DiemTichLuy] = ISNULL(kh.[DiemTichLuy], 0) + (i.[TongTien] / 100000)
    FROM [KhachHang] kh
    JOIN inserted i ON kh.[MaKhachHang] = i.[MaKhachHang];

    PRINT N'HỆ THỐNG: Đã tự động cộng điểm tích lũy thành công cho khách hàng!';
END;
GO
```
*Ảnh 1: Chạy xong code thêm cột và lệnh tạo Trigger*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5d542717-446b-4fe5-9854-fc3f0fe9896a" />
```
-- 3. Khai thác (Test) Trigger: Thêm 1 đơn đặt phòng trị giá 2.000.000 VNĐ
INSERT INTO [DatPhong] ([MaKhachHang], [MaPhong], [NgayNhanPhong], [NgayTraPhong], [TongTien])
VALUES (1, 'P101', '2026-05-01', '2026-05-03', 2000000);

-- Kiểm tra kết quả trong bảng Khách Hàng
SELECT [MaKhachHang], [HoVaTen], [DiemTichLuy] FROM [KhachHang] WHERE [MaKhachHang] = 1;
```
*Ảnh 2: Kết quả thực thi Trigger tự động cộng 20 điểm tích lũy cho khách hàng*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7b4deed8-d5c5-4476-a115-a8cc397577ab" />

#### 4.2. Khảo sát lỗi vòng lặp Trigger (Circular Trigger)

* **Yêu cầu nghiệp vụ của SP:** Thử nghiệm tình trạng xung đột logic khi hai bảng cập nhật qua lại lẫn nhau. Tạo BangA và BangB. Thiết lập Trigger sao cho: Khi BangA được chèn dữ liệu thì cập nhật sang BangB, và ngược lại khi BangB cập nhật thì lại tác động ngược về BangA.

* **Mã nguồn thực thi:**

``` SQL
USE [QuanLyKhachSan_K235480106056];
GO

-- 1. Tạo 2 bảng tạm để thử nghiệm vòng lặp
CREATE TABLE BangA (ID INT, DuLieu NVARCHAR(50));
CREATE TABLE BangB (ID INT, DuLieu NVARCHAR(50));
INSERT INTO BangB VALUES (1, N'Dữ liệu gốc B');
GO

-- 2. Trigger trên BangA: Kích hoạt khi Insert/Update để cập nhật sang BangB
CREATE TRIGGER trg_LoiVongLap_A ON BangA AFTER INSERT, UPDATE AS
BEGIN
    UPDATE BangB SET DuLieu = N'A vừa tác động' WHERE ID = 1;
END;
GO

-- 3. Trigger trên BangB: Kích hoạt khi Update để cập nhật ngược về BangA
CREATE TRIGGER trg_LoiVongLap_B ON BangB AFTER UPDATE AS
BEGIN
    UPDATE BangA SET DuLieu = N'B vừa phản hồi' WHERE ID = 1;
END;
GO

-- 4. Thực thi lệnh "châm ngòi" vòng lặp
INSERT INTO BangA VALUES (1, N'Bắt đầu');
```

*Ảnh 3: Thông báo lỗi hệ thống khi Trigger rơi vào vòng lặp vô hạn.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c67b800a-96d7-42d2-b1dd-99d241e59be2" />

##### Giải thích và Nhận xét:
- Thông báo của hệ thống: Maximum stored procedure, function, trigger, or view nesting level exceeded (limit 32).
- Giải thích lỗi: Khi ta INSERT vào BangA, Trigger A chạy và thực hiện lệnh UPDATE trên BangB. Lệnh này ngay lập tức kích hoạt Trigger B chạy, và Trigger B lại thực hiện UPDATE trên BangA. Chu kỳ này lặp đi lặp lại không có điểm dừng (Vòng lặp vô hạn).
- Cơ chế bảo vệ: SQL Server có cơ chế kiểm soát mức độ lồng nhau (nesting level). Để tránh việc hệ thống bị treo hoặc tràn bộ nhớ, SQL Server quy định giới hạn tối đa là 32 cấp. Khi vòng lặp chạm ngưỡng này, hệ thống sẽ tự động ngắt kết nối, hủy bỏ giao dịch và xuất thông báo lỗi như trên.
- Nhận xét cuối cùng: Đây là một lỗi thiết kế nghiêm trọng trong cơ sở dữ liệu (Circular Dependency). Khi xây dựng hệ thống thực tế, lập trình viên cần hết sức thận trọng khi viết Trigger liên bảng, phải đảm bảo luồng dữ liệu đi theo một chiều nhất định để tránh gây sập dịch vụ hoặc làm sai lệch dữ liệu hàng loạt.

### Phần 5: Cursor và Duyệt dữ liệu
#### 5.1. Sử dụng CURSOR để xử lý dữ liệu từng bản ghi
* **Yêu cầu nghiệp vụ của SP:** Duyệt qua danh sách khách hàng. Với mỗi khách hàng, hệ thống sẽ kiểm tra tổng chi tiêu. Nếu chi tiêu > 5.000.000 VNĐ, in ra thông báo tặng mã giảm giá "VIP10", nếu dưới mức đó thì tặng mã "WELCOME5". (Đây là logic xử lý riêng biệt mà SQL dạng tập hợp thông thường khó diễn đạt dưới dạng thông báo văn bản cá nhân hóa).

* **Mã nguồn thực thi:**

``` SQL
USE [QuanLyKhachSan_K235480106056];
GO

-- Khai báo biến để chứa dữ liệu từ Cursor
DECLARE @TenKH NVARCHAR(100);
DECLARE @TongTien DECIMAL(18,2);

-- 1. Khai báo Cursor
DECLARE cur_KhuyenMai CURSOR FOR 
SELECT kh.HoVaTen, SUM(dp.TongTien)
FROM KhachHang kh
LEFT JOIN DatPhong dp ON kh.MaKhachHang = dp.MaKhachHang
GROUP BY kh.HoVaTen;

-- 2. Mở Cursor
OPEN cur_KhuyenMai;

-- 3. Đọc bản ghi đầu tiên
FETCH NEXT FROM cur_KhuyenMai INTO @TenKH, @TongTien;

-- 4. Vòng lặp duyệt qua từng bản ghi
WHILE @@FETCH_STATUS = 0
BEGIN
    IF @TongTien > 5000000
        PRINT N'Gửi tới khách hàng ' + @TenKH + N': Bạn là khách hàng VIP. Tặng bạn mã giảm giá VIP10!';
    ELSE
        PRINT N'Gửi tới khách hàng ' + @TenKH + N': Cảm ơn bạn đã sử dụng dịch vụ. Tặng bạn mã WELCOME5!';
        
    -- Đọc bản ghi tiếp theo
    FETCH NEXT FROM cur_KhuyenMai INTO @TenKH, @TongTien;
END;

-- 5. Đóng và giải phóng Cursor
CLOSE cur_KhuyenMai;
DEALLOCATE cur_KhuyenMai;
```
*Ảnh 1: Kết quả chạy Cursor in ra thông báo cá nhân hóa trong tab Messages.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/df915e37-e913-4b87-8443-784732bee052" />
##### Giải thích Sử dụng CURSOR để xử lý dữ liệu từng bản ghi:
- Cơ chế hoạt động: Cursor cur_KhuyenMai đã duyệt qua danh sách các khách hàng trong hệ thống. Tại mỗi dòng (row), nó lấy ra tên khách hàng và tổng chi tiêu để kiểm tra điều kiện.
- Kết quả hiển thị: Trong tab Messages, ta thấy hệ thống đã in ra các dòng thông báo khác nhau: Khách hàng "Nguyễn Văn An" được nhận mã VIP10 vì có chi tiêu thỏa mãn điều kiện, trong khi các khách hàng khác nhận mã WELCOME5.
- Đặc điểm: Đây là minh chứng cho việc Cursor có thể can thiệp vào từng bản ghi để thực hiện các tác vụ ngoài SQL (như in thông báo văn bản cá nhân hóa) mà câu lệnh SELECT thông thường không làm trực tiếp được trong tab Messages.

#### 5.2. Giải quyết bài toán không dùng CURSOR (Sử dụng SQL Set-based)
* **Cách làm:** Thay vì duyệt từng dòng bằng Cursor, ta sử dụng câu lệnh `SELECT` kết hợp với biểu thức điều kiện `CASE WHEN`. Cách tiếp cận này cho phép SQL Server tính toán trên toàn bộ tập dữ liệu khách hàng cùng một lúc

* **Mã nguồn thực thi:**

``` SQL
SELECT kh.HoVaTen, 
       CASE 
            WHEN SUM(dp.TongTien) > 5000000 THEN N'Tặng mã VIP10'
            ELSE N'Tặng mã WELCOME5'
       END AS [ThongBaoKhuyenMai]
FROM KhachHang kh
LEFT JOIN DatPhong dp ON kh.MaKhachHang = dp.MaKhachHang
GROUP BY kh.HoVaTen;
```
*Ảnh 2: Kết quả truy vấn dữ liệu tập hợp nhanh chóng và chính xác.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8c6535d8-3f1b-4c1c-91bf-a6fa082d7a13" />

##### Giải thích:
- Hiển thị dữ liệu: Kết quả trả về dưới dạng bảng (Grid) rất trực quan. Ta có thể thấy ngay danh sách khách hàng đi kèm với thông báo khuyến mãi tương ứng.
- Tính chính xác: Khách hàng "Nguyễn Văn An" có mức chi tiêu trên 5 triệu đã được hệ thống tự động gán nhãn "Tặng mã VIP10", trong khi các khách hàng khác nhận nhãn "WELCOME5".
-Ưu điểm: Code ngắn gọn, dễ đọc, dễ bảo trì và đặc biệt là hiệu năng thực thi cực cao so với việc dùng vòng lặp Cursor.
#### So sánh tốc độ và Hiệu năng
* **So sánh:** *
- Sử dụng Cursor: Xử lý theo kiểu "Row-by-row" (từng dòng một). Giống như việc bạn đi đưa thư cho từng nhà một. Rất chậm khi dữ liệu lớn vì SQL Server phải thực hiện nhiều thao tác quản lý con trỏ.
- Sử dụng SQL Set-based: Xử lý theo kiểu "Tập hợp". Giống như việc bạn gửi email hàng loạt cho toàn thành phố cùng lúc. Cực kỳ nhanh vì tối ưu được bộ máy truy vấn của SQL.
*Ảnh 3: Màn hình Client Statistics so sánh thời gian thực thi.*
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fa114dc0-e559-49c4-9370-f10501d89902" />
<img width="572" height="470" alt="image" src="https://github.com/user-attachments/assets/613a7b35-cf2b-4dd3-8416-6e18917b773d" />

#### 5.3. Bài toán "Chỉ CURSOR mới giải quyết được" (hoặc SQL rất khó giải quyết)
   Trong tư duy SQL hiện đại, xử lý tập hợp (Set-based) luôn được ưu tiên. Tuy nhiên, có những bài toán thuộc nhóm "Row-by-Row Dependent Logic" (Dòng sau bắt buộc phụ thuộc vào kết quả tính toán của dòng trước), nơi mà SQL thuần rất khó diễn đạt hoặc gây sai số. Dưới đây là các ví dụ điển hình chứng minh sức mạnh của Cursor:

*Ví dụ 1: Bài toán trừ tồn kho theo phương pháp FIFO (First-In, First-Out)*

+ Bối cảnh: Khách sạn nhập khăn tắm theo nhiều lô. Lô A nhập 10 cái, Lô B nhập 20 cái. Khi xuất 15 cái cho buồng phòng, hệ thống phải trừ hết 10 cái ở Lô A rồi mới nhảy sang Lô B trừ tiếp 5 cái nữa.

+ Vấn đề của SQL thuần: Xử lý tập hợp tất cả các dòng cùng lúc, nên hệ thống không thể "nhớ" được sau khi trừ Lô A thì số lượng cần trừ còn lại là bao nhiêu để áp dụng chuẩn xác cho Lô B.

+ Giải pháp Cursor: Duyệt từng lô theo thời gian. Tại mỗi dòng, Cursor thực hiện phép tính: Số lượng cần trừ còn lại = Số lượng cần trừ - Số lượng lô hiện tại. Giá trị này được lưu vào một biến số và mang đi trừ tiếp ở dòng sau. Đây là quá trình duy trì "trạng thái" mà chỉ vòng lặp mới làm tốt.

*Ví dụ 2: Bài toán tính tiền dịch vụ theo định mức lũy tiến (Bậc thang)*

+ Bối cảnh: Tiền điện/nước của phòng khách sạn tính theo bậc thang: 50 số đầu giá 2.000đ, từ số 51-100 giá 2.500đ...

+ Vấn đề của SQL thuần: Nếu khách dùng 120 số, việc viết một câu SELECT bóc tách từng phần đòi hỏi rất nhiều lệnh CASE WHEN lồng nhau, cực kỳ phức tạp và khó bảo trì khi khách sạn đổi giá.

+ Giải pháp Cursor: Duyệt qua bảng cấu hình định mức. Với mỗi bậc, tính toán phần sản lượng nằm trong bậc đó rồi cộng dồn vào biến TongTien. Logic rõ ràng và dễ dàng mở rộng.

*Ví dụ 3: Gọi thủ tục hệ thống (Stored Procedure) cho từng bản ghi*

+ Bối cảnh: Cuối tháng, khách sạn cần duyệt danh sách 100 khách VIP để sinh mã giảm giá ngẫu nhiên và gửi Email tự động cho từng người.

+ Vấn đề của SQL thuần: Lệnh SELECT thông thường không thể tự động kích hoạt một Stored Procedure khác cho từng dòng dữ liệu mà nó đang truy vấn.

+ Giải pháp Cursor: Tại mỗi dòng dữ liệu khách hàng, Cursor lấy địa chỉ Email và thực thi lệnh EXEC sp_SendMail @EmailCustomer. Đây là cách an toàn và duy nhất để làm cầu nối giữa dữ liệu bảng và các tác vụ hệ thống phức tạp bên ngoài.
