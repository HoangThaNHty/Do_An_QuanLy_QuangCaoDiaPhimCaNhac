# Hệ Thống Quản Lý Quảng Cáo Đĩa Phim & Ca Nhạc

[![ASP.NET MVC](https://img.shields.io/badge/ASP.NET%20MVC-5.0-blue?style=flat-square&logo=.net)](https://dotnet.microsoft.com/)
[![C#](https://img.shields.io/badge/C%23-8.0-purple?style=flat-square&logo=csharp)](https://docs.microsoft.com/en-us/dotnet/csharp/)
[![SQL Server](https://img.shields.io/badge/SQL%20Server-2012+-orange?style=flat-square&logo=sql)](https://www.microsoft.com/en-us/sql-server)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

Hệ thống web quản lý và bán đĩa phim, ca nhạc (DVD/CD) trực tuyến dành cho cửa hàng kinh doanh đĩa. Hỗ trợ 2 vai trò: Khách hàng và Người bán.

---

## Tính Năng

### Khách Hàng
- Xem danh sách sản phẩm nổi bật và mới nhất
- Tìm kiếm sản phẩm theo tên
- Lọc sản phẩm theo thể loại, khoảng giá, loại (phim/nhạc)
- Xem chi tiết sản phẩm kèm thông tin đánh giá
- Giỏ hàng: thêm, sửa số lượng, xóa sản phẩm
- Đặt hàng và thanh toán
- Đăng ký / Đăng nhập tài khoản

### Người Bán (Seller)
- Dashboard thống kê tổng quan (sản phẩm, đơn hàng, doanh thu)
- Quản lý sản phẩm: thêm, sửa, xóa sản phẩm (CRUD)
- Quản lý đơn hàng: xem danh sách, cập nhật trạng thái giao hàng
- Thống kê doanh thu theo tháng, top sản phẩm bán chạy
- Xem chi tiết đơn hàng

### Quản Trị
- Quản lý danh mục thể loại đĩa (CRUD)

---

## Công Nghệ Sử Dụng

| Thành phần | Công nghệ |
|---|---|
| Framework | ASP.NET MVC 5 (.NET Framework) |
| Ngôn ngữ | C# |
| Cơ sở dữ liệu | SQL Server 2012+ (Entity Framework EDMX) |
| Frontend | Razor, Bootstrap 5, HTML5, JavaScript, jQuery |
| UI | Giao diện dark theme |
| Authentication | Session-based |
| Khác | Newtonsoft.Json, Stored Procedures |

---

## Kiến Trúc Hệ Thống

```
┌─────────────────────────────────────────────────────────────┐
│                     Client (Browser)                        │
│              Bootstrap 5 + jQuery + AJAX                     │
└─────────────────────────┬───────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│              Backend (ASP.NET MVC 5 - C#)                    │
├─────────────────────────────────────────────────────────────┤
│  Controllers                                                 │
│  ├── HomeController       │ Trang chủ, tìm kiếm, lọc         │
│  ├── DiaPhimNhacController│ API RESTful (JSON responses)     │
│  ├── CartController       │ Giỏ hàng, thanh toán            │
│  ├── AccountController    │ Đăng nhập, đăng ký              │
│  ├── SellerController     │ Dashboard người bán             │
│  └── CategoryController   │ Quản lý thể loại                │
├─────────────────────────────────────────────────────────────┤
│  Models                                                  │
│  ├── Entity Framework (EDMX)                              │
│  ├── DTOs                │ DiaDTO, PagedResult             │
│  ├── ViewModels          │ TopProductViewModel             │
│  └── Stored Procedures   │ sp_GetChiTietDiaPhimCaNhac...    │
└─────────────────────────┬───────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│                    SQL Server Database                        │
│      QUANLY_DIAPHIM_CANHAC (21 bảng)                          │
└─────────────────────────────────────────────────────────────┘
```

---

## Cấu Trúc Dự Án

```
DoAnQuanLyQuangCaoDiaPhimCaNhac/
├── Controllers/
│   ├── API/                 # API Controllers
│   ├── AccountController.cs # Đăng nhập, đăng ký
│   ├── CartController.cs    # Giỏ hàng
│   ├── CategoryController.cs# Quản lý thể loại
│   ├── DiaPhimNhacController.cs # API sản phẩm (RESTful)
│   ├── HomeController.cs    # Trang chủ
│   └── SellerController.cs  # Dashboard người bán
├── Models/
│   ├── DTOs/               # Data Transfer Objects
│   ├── ViewModels/         # View Models
│   ├── *.cs                # Entity classes (21 bảng DB)
│   └── sp_*.cs             # Stored Procedure results
├── Views/
│   ├── Account/            # Login, Register
│   ├── Cart/               # Giỏ hàng
│   ├── Category/           # Quản lý thể loại
│   ├── Home/               # Trang chủ, chi tiết, tìm kiếm
│   ├── Seller/             # Dashboard người bán
│   └── Shared/_Layout.cshtml
├── Content/
│   ├── Images/             # Hình ảnh sản phẩm
│   ├── bootstrap.css
│   └── site-custom.css
├── Scripts/                # JavaScript, jQuery
├── App_Start/              # Bundle, Filter, Route config
├── Backup.sql              # Script tạo database
├── Web.config.example.txt  # Template cấu hình
└── DoAnQuanLyQuangCaoDiaPhimCaNhac.sln
```

---

## Các Bảng Chính Trong Database

- `KhachHang` - Thông tin khách hàng
- `NguoiBan` - Thông tin người bán
- `DiaPhimCaNhac` - Sản phẩm đĩa (phim/nhạc)
- `LoaiDia` - Thể loại đĩa
- `NhaSanXuat` - Nhà sản xuất
- `GioHang` - Giỏ hàng
- `DonHang` - Đơn hàng
- `ChiTietDonHang` - Chi tiết đơn hàng
- `DanhGiaSanPham` - Đánh giá sản phẩm
- `GiaoDichThanhToan` - Giao dịch thanh toán
- `KhuyenMai` - Khuyến mãi
- `TrangThaiGiaoHang` - Trạng thái giao hàng
- `NgheSi` - Nghệ sĩ
- `ThamGiaThucHien` - Tham gia thực hiện (phim/nhạc)

---

## Cài Đặt

### 1. Cấu hình Database

Chạy file `Backup.sql` trong SQL Server Management Studio để tạo database.

### 2. Cấu hình kết nối

Copy `Web.config.example.txt` thành `Web.config` trong thư mục project và sửa connection string:

```xml
<connectionStrings>
  <add name="QuanLyDiaPhimCaNhac_EditedEntities"
       connectionString="Data Source=TEN_MAY;Initial Catalog=QUANLY_DIAPHIM_CANHAC;User ID=sa;Password=your_password"
       providerName="System.Data.SqlClient"/>
</connectionStrings>
```

### 3. Chạy ứng dụng

Mở solution trong Visual Studio và nhấn **F5**.

---

## Tài Khoản Mặc Định

| Vai trò | Tài khoản | Mật khẩu |
|---|---|---|
| Người bán | seller1 | 123 |
| Người bán | seller2 | 123 |

*(Tài khoản khách hàng đăng ký trực tiếp trên web)*

---

## API Endpoints (RESTful)

| Method | Endpoint | Mô tả |
|---|---|---|
| GET | `/DiaPhimNhac/ChiTietDiaPhimCaNhac?id={id}` | Chi tiết sản phẩm |
| GET | `/DiaPhimNhac/GetByLoaiDia?id={loai}` | Lấy sản phẩm theo thể loại (có phân trang) |
| GET | `/DiaPhimNhac/Search?keyword={keyword}` | Tìm kiếm sản phẩm |
| GET | `/DiaPhimNhac/GetSanPhamNoiBat` | Sản phẩm nổi bật |
| POST | `/DiaPhimNhac/ThemVaoGioHang` | Thêm vào giỏ hàng |

---

## License

[MIT License](LICENSE)