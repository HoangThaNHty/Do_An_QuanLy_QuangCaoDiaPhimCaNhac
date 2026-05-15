# :dvd: Hệ thống Quản lý Quảng Cáo Đĩa Phim & Ca Nhạc

[![ASP.NET MVC](https://camo.githubusercontent.com/cf2a5f6977504db45292b695446c0b4ae92c86c39bcda24728ca2453444a2a9b/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f2e4e45542d352e302d626c75653f7374796c653d666c61742d737175617265266c6f676f3d2e6e6574)](https://dotnet.microsoft.com/) [![C#](https://camo.githubusercontent.com/c3d02ad2645d9dd9461403eab0d4952cf0b1d75169c0e325a19498be00240f40/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f432532332d382e302d707572706c653f7374796c653d666c61742d737175617265266c6f676f3d637368617270)](https://docs.microsoft.com/en-us/dotnet/csharp/) [![SQL Server](https://camo.githubusercontent.com/0a8bbbcd431a6482208d1f56eb0ffc3b89f6a280ed8f5c65e72ee4ada773457f/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f53514c2532305365727665722d323031322b2d6f72616e67653f7374796c653d666c61742d737175617265266c6f676f3d73716c)](https://www.microsoft.com/en-us/sql-server) [![License](https://camo.githubusercontent.com/152aa2a37725b9fd554b28ff24d270f6071c67927a63e6d635a55c8e188e20c7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4c6963656e73652d4d49542d677265656e3f7374796c653d666c61742d737175617265)](/HoangThaNHty/Do_An_QuanLy_QuangCaoDiaPhimCaNhac/blob/main/LICENSE)

Ứng dụng web quản lý và bán đĩa phim, ca nhạc (DVD/CD) trực tuyến dành cho cửa hàng kinh doanh đĩa. Hỗ trợ 2 vai trò chính: Khách hàng và Người bán.

## Tính năng

- Tìm kiếm, lọc sản phẩm theo thể loại, khoảng giá
- Giỏ hàng: thêm, sửa số lượng, xóa sản phẩm
- Đặt hàng và thanh toán
- Dashboard người bán: quản lý sản phẩm, đơn hàng, thống kê doanh thu
- Quản lý danh mục thể loại đĩa (Admin)

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
│  ├── HomeController         │ Trang chủ, tìm kiếm, lọc       │
│  ├── CartController         │ Giỏ hàng, thanh toán            │
│  ├── AccountController      │ Đăng nhập, đăng ký              │
│  ├── SellerController       │ Dashboard người bán             │
│  └── CategoryController    │ Quản lý thể loại               │
├─────────────────────────────────────────────────────────────┤
│  Models                                                     │
│  ├── Entity Framework (EDMX)                                 │
│  ├── DTOs                   │ DiaDTO, PagedResult           │
│  ├── ViewModels             │ TopProductViewModel           │
│  └── Stored Procedures      │ sp_GetChiTiet...              │
└─────────────────────────┬───────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────────┐
│                    SQL Server Database                       │
│        QUANLY_DIAPHIM_CANHAC (21 bảng)                       │
└─────────────────────────────────────────────────────────────┘
```

## Cấu trúc dự án

```
DoAnQuanLyQuangCaoDiaPhimCaNhac/
├── Controllers/              # MVC Controllers
│   ├── AccountController.cs  # Đăng nhập, đăng ký
│   ├── CartController.cs     # Giỏ hàng
│   ├── CategoryController.cs  # Quản lý thể loại
│   ├── HomeController.cs     # Trang chủ
│   └── SellerController.cs    # Dashboard người bán
├── Models/
│   ├── DTOs/                 # Data Transfer Objects
│   ├── ViewModels/           # View Models
│   └── *.cs                  # Entity classes + SP results
├── Views/                    # Razor Views
├── Backup.sql                # Script tạo database
└── DoAnQuanLyQuangCaoDiaPhimCaNhac.sln
```

## Công nghệ sử dụng

- **Backend:** ASP.NET MVC 5 (.NET Framework)
- **Ngôn ngữ:** C#
- **Cơ sở dữ liệu:** SQL Server 2012+ (Entity Framework EDMX)
- **Frontend:** Razor, Bootstrap 5, jQuery
- **Authentication:** Session-based

## Cài Đặt

### 1. Database

Chạy file `Backup.sql` trong SQL Server Management Studio.

### 2. Kết nối

Copy `Web.config.example.txt` thành `Web.config` và sửa connection string phù hợp.

### 3. Chạy ứng dụng

Mở solution trong Visual Studio, nhấn **F5**.

## Tài khoản mặc định

| Vai trò | Tài khoản | Mật khẩu |
|---|---|---|
| Người bán | seller1 | 123 |

*(Tài khoản khách hàng đăng ký trực tiếp trên web)*

## License

[MIT License](LICENSE)