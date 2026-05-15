# :dvd: Hệ thống Quản lý Quảng Cáo Đĩa Phim & Ca Nhạc

[![ASP.NET MVC](https://camo.githubusercontent.com/cf2a5f6977504db45292b695446c0b4ae92c86c39bcda24728ca2453444a2a9b/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f2e4e45542d352e302d626c75653f7374796c653d666c61742d737175617265266c6f676f3d2e6e6574)](https://dotnet.microsoft.com/) [![C#](https://camo.githubusercontent.com/c3d02ad2645d9dd9461403eab0d4952cf0b1d75169c0e325a19498be00240f40/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f432532332d382e302d707572706c653f7374796c653d666c61742d737175617265266c6f676f3d637368617270)](https://docs.microsoft.com/en-us/dotnet/csharp/) [![SQL Server](https://camo.githubusercontent.com/0a8bbbcd431a6482208d1f56eb0ffc3b89f6a280ed8f5c65e72ee4ada773457f/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f53514c2532305365727665722d323031322b2d6f72616e67653f7374796c653d666c61742d737175617265266c6f676f3d73716c)](https://www.microsoft.com/en-us/sql-server) [![License](https://camo.githubusercontent.com/152aa2a37725b9fd554b28ff24d270f6071c67927a63e6d635a55c8e188e20c7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4c6963656e73652d4d49542d677265656e3f7374796c653d666c61742d737175617265)](/HoangThaNHty/Do_An_QuanLy_QuangCaoDiaPhimCaNhac/blob/main/LICENSE)

Ứng dụng web quản lý và bán đĩa phim, ca nhạc (DVD/CD) trực tuyến dành cho cửa hàng kinh doanh đĩa. Hỗ trợ 2 vai trò chính: Khách hàng và Người bán.

## Tính năng

- Tìm kiếm sản phẩm theo tên, lọc theo thể loại, khoảng giá
- Xem chi tiết sản phẩm kèm thông tin đánh giá
- Giỏ hàng: thêm, sửa số lượng, xóa sản phẩm
- Đặt hàng và thanh toán
- Dashboard người bán: quản lý sản phẩm, đơn hàng, thống kê doanh thu
- Thông báo real-time khi thêm sản phẩm vào giỏ
- API RESTful trả về JSON

## Kiến trúc hệ thống

```
┌─────────────────────────────────────────────────────────────┐
│                      Client (Browser)                        │
│              Bootstrap 5 + jQuery + AJAX                     │
└─────────────────────────┬───────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│              Backend (ASP.NET MVC 5 - C#)                    │
├─────────────────────────────────────────────────────────────┤
│  Controllers                                                 │
│  ├── HomeController        │ Trang chủ, tìm kiếm, lọc       │
│  ├── DiaPhimNhacController │ API RESTful (JSON responses)   │
│  ├── CartController        │ Giỏ hàng, thanh toán           │
│  ├── AccountController     │ Đăng nhập, đăng ký             │
│  ├── SellerController      │ Dashboard người bán            │
│  └── CategoryController    │ Quản lý thể loại                │
├─────────────────────────────────────────────────────────────┤
│  Models                                                     │
│  ├── Entity Framework (EDMX)                                 │
│  ├── DTOs                  │ DiaDTO, PagedResult            │
│  ├── ViewModels            │ TopProductViewModel            │
│  └── Stored Procedures     │ sp_GetChiTietDiaPhimCaNhac...  │
└─────────────────────────┬───────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│                    SQL Server Database                        │
│        QUANLY_DIAPHIM_CANHAC (21 bảng)                        │
└─────────────────────────────────────────────────────────────┘
```

## Cấu trúc dự án

```
DoAnQuanLyQuangCaoDiaPhimCaNhac/
├── Controllers/
│   ├── API/                      # API Controllers
│   ├── AccountController.cs      # Đăng nhập, đăng ký
│   ├── CartController.cs         # Giỏ hàng
│   ├── CategoryController.cs     # Quản lý thể loại
│   ├── DiaPhimNhacController.cs  # API sản phẩm (RESTful)
│   ├── HomeController.cs         # Trang chủ
│   └── SellerController.cs       # Dashboard người bán
├── Models/
│   ├── DTOs/                     # Data Transfer Objects
│   ├── ViewModels/               # View Models
│   ├── *.cs                      # Entity classes (21 bảng DB)
│   └── sp_*.cs                   # Stored Procedure results
├── Views/
│   ├── Account/                  # Login, Register
│   ├── Cart/                     # Giỏ hàng
│   ├── Category/                 # Quản lý thể loại
│   ├── Home/                     # Trang chủ, chi tiết, tìm kiếm
│   ├── Seller/                   # Dashboard người bán
│   └── Shared/_Layout.cshtml
├── Content/
│   ├── Images/                   # Hình ảnh sản phẩm
│   ├── bootstrap.css
│   └── site-custom.css
├── Scripts/                     # JavaScript, jQuery
├── App_Start/                   # Bundle, Filter, Route config
├── Backup.sql                   # Script tạo database
├── Web.config.example.txt        # Template cấu hình
└── DoAnQuanLyQuangCaoDiaPhimCaNhac.sln
```

## Công nghệ sử dụng

- **Backend:** ASP.NET MVC 5 (.NET Framework)
- **Ngôn ngữ:** C#
- **Cơ sở dữ liệu:** SQL Server 2012+ (Entity Framework EDMX)
- **Frontend:** Razor, Bootstrap 5, HTML5, JavaScript, jQuery
- **Authentication:** Session-based
- **Khác:** Newtonsoft.Json, Stored Procedures

## Yêu cầu hệ thống

- Windows 7 trở lên
- .NET Framework 4.7.2
- SQL Server 2012 trở lên
- Visual Studio 2019 trở lên

## Cài đặt

### 1. Cấu hình Database

Chạy file `Backup.sql` trong SQL Server Management Studio để tạo database:

```sql
-- Chạy toàn bộ nội dung file Backup.sql để tạo CSDL
```

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

Mở solution trong Visual Studio.

Nhấn **F5** để chạy.

## Sử dụng chức năng chính

| Chức năng | Mô tả |
|---|---|
| Trang chủ | Xem danh sách sản phẩm nổi bật, mới nhất |
| Tìm kiếm | Nhập tên sản phẩm để tìm |
| Lọc sản phẩm | Lọc theo thể loại, khoảng giá, loại (phim/nhạc) |
| Giỏ hàng | Thêm, sửa số lượng, xóa sản phẩm |
| Đặt hàng | Điền địa chỉ giao hàng và thanh toán |
| Đăng nhập người bán | seller1 / 123 để vào dashboard |

## API Endpoints

| Method | Endpoint | Mô tả |
|---|---|---|
| GET | `/DiaPhimNhac/ChiTietDiaPhimCaNhac?id={id}` | Chi tiết sản phẩm |
| GET | `/DiaPhimNhac/GetByLoaiDia?id={loai}` | Lấy sản phẩm theo thể loại (có phân trang) |
| GET | `/DiaPhimNhac/Search?keyword={keyword}` | Tìm kiếm sản phẩm |
| GET | `/DiaPhimNhac/GetSanPhamNoiBat` | Sản phẩm nổi bật |
| POST | `/DiaPhimNhac/ThemVaoGioHang` | Thêm vào giỏ hàng |

## Lưu ý

- Bản đồ sử dụng Bootstrap 5, cần kết nối Internet để hiển thị đúng giao diện
- Tài khoản người bán mặc định: `seller1` / `123`
- Cache được sử dụng để tối ưu truy vấn sản phẩm

## License

[MIT License](/HoangThaNHty/Do_An_QuanLy_QuangCaoDiaPhimCaNhac/blob/main/LICENSE)