# 💿🎬🎵 HỆ THỐNG QUẢN LÝ VÀ BÁN ĐĨA PHIM CA NHẠC

[![ASP.NET MVC](https://img.shields.io/badge/ASP.NET%20MVC-5-blue?style=flat-square&logo=.net)](https://dotnet.microsoft.com/)
[![C#](https://img.shields.io/badge/C%23-8.0-purple?style=flat-square&logo=csharp)](https://docs.microsoft.com/en-us/dotnet/csharp/)
[![SQL Server](https://img.shields.io/badge/SQL%20Server-2012+-orange?style=flat-square&logo=microsoftsqlserver)](https://www.microsoft.com/en-us/sql-server)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

Nền tảng E-commerce đa người bán (**Multi-vendor**) được xây dựng trên **ASP.NET MVC 5**, **Entity Framework 6** và **SQL Server**, cho phép quản lý và giao dịch các sản phẩm đĩa phim ca nhạc. Dự án tập trung vào việc cung cấp một hệ thống mạnh mẽ, linh hoạt với các tính năng nghiệp vụ phức tạp và trải nghiệm người dùng tối ưu.

---

## 📋 Mục Lục

- [Kiến Trúc Hệ Thống](#-kiến-trúc-hệ-thống)
- [Tính Năng Chính](#-tính-năng-chính)
- [Cấu Trúc Thư Mục](#-cấu-trúc-thư-mục)
- [Công Nghệ Sử Dụng](#-công-nghệ-sử-dụng)
- [Điểm Nhấn Kỹ Thuật](#-điểm-nhấn-kỹ-thuật)
- [Cài Đặt và Khởi Chạy](#-cài-đặt-và-khởi-chạy)
- [Tài Khoản Mặc Định](#-tài-khoản-mặc-định)
- [Mẹo Khi Phát Triển](#-mẹo-khi-phát-triển)

---

## 🏗 Kiến Trúc Hệ Thống

```
┌─────────────────────────────────────────────────────────────┐
│                      Client (Browser)                        │
│              Bootstrap 5 + jQuery + AJAX                     │
└─────────────────────────┬───────────────────────────────────┘
                          │ HTTP Request / AJAX
┌─────────────────────────▼───────────────────────────────────┐
│              Backend (ASP.NET MVC 5 - C#)                    │
├─────────────────────────────────────────────────────────────┤
│  Controllers                                                 │
│  ├── HomeController         │ Trang chủ, tìm kiếm, lọc       │
│  ├── CartController         │ Giỏ hàng, thanh toán            │
│  ├── AccountController      │ Đăng nhập, đăng ký, phân quyền │
│  ├── SellerController       │ Dashboard người bán             │
│  └── CategoryController     │ Quản lý thể loại               │
├─────────────────────────────────────────────────────────────┤
│  Models                                                      │
│  ├── Entity Framework (EDMX Database First)                  │
│  ├── DTOs                   │ DiaDTO, PagedResult            │
│  ├── ViewModels             │ TopProductViewModel            │
│  └── Stored Procedures      │ sp_GetChiTiet...               │
└─────────────────────────┬───────────────────────────────────┘
                          │ Entity Framework / ADO.NET
┌─────────────────────────▼───────────────────────────────────┐
│                    SQL Server Database                       │
│        QUANLY_DIAPHIM_CANHAC (21 bảng)                       │
└─────────────────────────────────────────────────────────────┘
```

---

## 🚀 Tính Năng Chính

| Tính năng | Mô tả |
|-----------|-------|
| **Quản lý Sản phẩm (CRUD)** | Thêm, sửa, xóa và theo dõi chi tiết đĩa phim/nhạc |
| **Tìm kiếm & Lọc thông minh** | Tra cứu nhanh theo từ khóa, thể loại, định dạng và khoảng giá bằng AJAX (không tải lại trang) |
| **Giỏ hàng & Thanh toán** | Cập nhật giỏ hàng trực quan; tự động tách đơn hàng theo nhà cung cấp (Multi-vendor Order Splitting) |
| **Quản lý tồn kho** | Tự động cập nhật số lượng kho ngay khi thanh toán thành công |
| **Xác thực & Phân quyền (RBAC)** | Đăng ký/đăng nhập và kiểm soát quyền truy cập riêng biệt cho Khách hàng, Người bán và Admin |
| **Thống kê & Báo cáo** | Biểu đồ doanh thu trực quan, theo dõi tăng trưởng tháng và sản phẩm bán chạy |

---

## 📂 Cấu Trúc Thư Mục

```
DoAnQuanLyQuangCaoDiaPhimCaNhac/
├── App_Start/                   # Cấu hình khởi tạo (Routes, Bundles, Filters)
│   ├── BundleConfig.cs          # Gộp và nén tài nguyên CSS/JS
│   ├── FilterConfig.cs          # Bộ lọc toàn cục
│   ├── RouteConfig.cs           # Định tuyến URL cho MVC
│   └── WebApiConfig.cs          # Định tuyến cho Web API
├── Content/                     # Tài nguyên tĩnh (CSS, hình ảnh)
│   ├── Images/                  # Ảnh sản phẩm và banner
│   ├── Site.css                 # CSS tùy chỉnh
│   └── site-custom.css          # CSS bổ sung (card sản phẩm, ...)
├── Controllers/                 # Xử lý logic nghiệp vụ và điều hướng
│   ├── API/                     # API Controllers (CategoryApiController, ...)
│   ├── AccountController.cs     # Đăng nhập, đăng ký, phân quyền
│   ├── CartController.cs        # Giỏ hàng và thanh toán
│   ├── HomeController.cs        # Trang chủ, tìm kiếm, lọc sản phẩm
│   ├── SellerController.cs      # Dashboard người bán (sản phẩm, đơn hàng, doanh thu)
│   └── ...
├── Models/                      # Entity, DTOs, ViewModels, EDMX
│   ├── DTOs/                    │ DiaDTO, PagedResult
│   ├── ViewModels/              │ TopProductViewModel
│   ├── QuanLyQuangCaoDiaPhimCaNhac.edmx # Entity Data Model (Database First)
│   └── ...                      # Entity classes (DiaPhimCaNhac, KhachHang, DonHang, ...)
├── Scripts/                     # jQuery, Bootstrap JS, Validation
├── Views/                       # Razor Views (.cshtml)
│   ├── Account/                 # Views tài khoản
│   ├── Cart/                    # Views giỏ hàng
│   ├── Category/                # Views quản lý danh mục
│   ├── Home/                    # Views trang chủ và sản phẩm
│   ├── Seller/                  # Views người bán
│   └── Shared/                  # Views dùng chung (_Layout, Error, ...)
├── Backup.sql                   # Script tạo database
├── Global.asax                  # Cấu hình ứng dụng toàn cục
├── packages.config              # Danh sách gói NuGet
├── Web.config                   # Cấu hình ứng dụng (connection string, app settings)
└── DoAnQuanLyQuangCaoDiaPhimCaNhac.sln
```

---

## 🛠 Công Nghệ Sử Dụng

### Backend
- **Ngôn ngữ:** `C#`
- **Framework:** `ASP.NET MVC 5`
- **ORM:** `Entity Framework 6` (Database First)
- **API:** `ASP.NET Web API 2`

### Database
- **Hệ quản trị:** `Microsoft SQL Server 2012+`

### Frontend
- **Core:** `HTML5`, `CSS3`, `JavaScript (ES6+)`
- **UI Framework:** `Bootstrap 5.2.3`
- **Libraries:** `jQuery 3.7.0`, `jQuery Validation`, `jQuery Unobtrusive Validation`

### Công cụ phát triển
- **IDE:** `Visual Studio 2022` (hoặc 2019) với workload *ASP.NET and web development*
- **.NET Framework:** `4.7.2`

---

## 💡 Điểm Nhấn Kỹ Thuật

1. **Kiến trúc Multi-vendor & Tách đơn hàng**  
   Tự động phân tích và bóc tách giỏ hàng tổng thành các đơn hàng con theo từng người bán, đảm bảo minh bạch dòng tiền và đồng bộ tồn kho chính xác.

2. **Tối ưu hóa LINQ nâng cao**  
   Sử dụng `GroupBy`, `Include`, `Select` để trích xuất dữ liệu đa tầng; tách biệt truy vấn thô và định dạng hiển thị trong bộ nhớ (In-memory Formatting) giúp giảm tải cho SQL Server.

3. **Phân quyền RBAC & Luồng an toàn**  
   Quản lý trạng thái qua Session để bảo vệ tài nguyên từ tầng Controller; bao bọc các nghiệp vụ nhạy cảm (như thanh toán) bằng try-catch chặt chẽ nhằm kiểm soát lỗi hệ thống.

4. **Tương tác mượt mà với AJAX**  
   Tích hợp các AJAX Endpoints xử lý cập nhật giỏ hàng thời gian thực và bộ lọc động, tối ưu hóa băng thông và hạn chế tải lại trang.

---

## 💻 Cài Đặt và Khởi Chạy

### 1. Tiền đề

| Phần mềm | Yêu cầu |
|----------|---------|
| **IDE** | Visual Studio 2022 (hoặc 2019) với workload *ASP.NET and web development* |
| **Database** | SQL Server Management Studio (SSMS) hoặc SQL Server Express |
| **Runtime** | .NET Framework 4.7.2 |

### 2. Các bước thực hiện

#### Bước 1: Tải mã nguồn

```bash
git clone https://github.com/tuhaovan917-ship-it/DoAnQuanLyQuangCaoDiaPhimCaNhac.git
cd DoAnQuanLyQuangCaoDiaPhimCaNhac
```

#### Bước 2: Thiết lập Cơ sở dữ liệu

1. Mở **SQL Server Management Studio (SSMS)**
2. Tạo Database mới tên: `QuanLyDiaPhimCaNhac_Edited`
3. Mở và thực thi (**Execute**) tệp script `Backup.sql` để khởi tạo cấu trúc bảng và dữ liệu mẫu

#### Bước 3: Cấu hình Connection String

1. Copy file `Web.config.example.txt` → đổi tên thành `Web.config`
2. Mở solution `DoAnQuanLyQuangCaoDiaPhimCaNhac.sln` bằng **Visual Studio**
3. Cập nhật `connectionString` trong `Web.config` cho khớp với SQL Server trên máy:

```xml
<add name="QuanLyDiaPhimCaNhac_EditedEntities"
     connectionString="metadata=res://*/Models.QuanLyQuangCaoDiaPhimCaNhac.csdl|res://*/Models.QuanLyQuangCaoDiaPhimCaNhac.ssdl|res://*/Models.QuanLyQuangCaoDiaPhimCaNhac.msl;provider=System.Data.SqlClient;provider connection string=&quot;
     data source=TEN_MAY_CUA_BAN\SQLEXPRESS;
     initial catalog=QuanLyDiaPhimCaNhac_Edited;
     integrated security=True;
     MultipleActiveResultSets=True;
     App=EntityFramework&quot;"
     providerName="System.Data.EntityClient" />
```

> **Lưu ý:** Thay `TEN_MAY_CUA_BAN\SQLEXPRESS` bằng tên SQL Server thực tế trên máy của bạn.

#### Bước 4: Khởi chạy dự án

1. Nhấp chuột phải vào **Solution** → chọn **Restore NuGet Packages**
2. Nhấn **F5** hoặc bấm **Start (IIS Express)** để khởi chạy

---

## 👤 Tài Khoản Mặc Định

| Vai trò | Tài khoản | Mật khẩu |
|---------|-----------|----------|
| Người bán | `seller1` | `123` |

> *(Tài khoản khách hàng có thể đăng ký trực tiếp trên website)*

---

## 💡 Mẹo Khi Phát Triển

- **NuGet Restore:** Nếu project báo lỗi thư viện khi vừa mở, hãy chọn **Build Solution** để Visual Studio tự động tải lại package còn thiếu.
- **Database First (.edmx):** Nếu thay đổi cấu trúc Database trong SQL Server, hãy mở file `.edmx` → chuột phải → chọn **Update Model from Database** để đồng bộ.
- **Debug AJAX:** Sử dụng **Browser DevTools (F12)** → tab **Network** để theo dõi các request AJAX và kiểm tra response từ server.

---

## 📄 License

[MIT License](LICENSE)
