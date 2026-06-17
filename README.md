# VietTravel - Tour Management System

Ứng dụng quản lý tour du lịch xây dựng bằng **.NET / C# / WPF**, sử dụng mô hình tách lớp gồm Core, Data và UI. Hệ thống hỗ trợ quản lý tour, khách hàng, hướng dẫn viên, booking, thanh toán, mã giảm giá, đánh giá và báo cáo.

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Công nghệ sử dụng](#công-nghệ-sử-dụng)
- [Chức năng chính](#chức-năng-chính)
- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Yêu cầu cài đặt](#yêu-cầu-cài-đặt)
- [Cấu hình môi trường](#cấu-hình-môi-trường)
- [Cài đặt và chạy dự án](#cài-đặt-và-chạy-dự-án)
- [Cơ sở dữ liệu](#cơ-sở-dữ-liệu)
- [Tài khoản mẫu](#tài-khoản-mẫu)
- [Ghi chú triển khai](#ghi-chú-triển-khai)

## Giới thiệu

**VietTravel** là phần mềm desktop phục vụ nghiệp vụ quản lý du lịch. Ứng dụng được thiết kế cho nhiều nhóm người dùng như quản trị viên, nhân viên quản lý tour, khách hàng và hướng dẫn viên.

Mục tiêu của hệ thống:

- Quản lý thông tin tour du lịch.
- Quản lý lịch khởi hành, booking và thanh toán.
- Quản lý khách hàng, hướng dẫn viên và phân công tour.
- Theo dõi đánh giá tour, đánh giá hướng dẫn viên.
- Quản lý mã giảm giá và báo cáo doanh thu.
- Lưu trữ dữ liệu tập trung thông qua Supabase/PostgreSQL.

## Công nghệ sử dụng

- **Ngôn ngữ:** C#
- **Nền tảng:** .NET 10
- **Giao diện:** WPF
- **Kiến trúc UI:** MVVM
- **Cơ sở dữ liệu:** PostgreSQL / Supabase
- **ORM/API Client:** Supabase C# Client, PostgREST C#
- **UI Library:** MaterialDesignThemes
- **MVVM Toolkit:** CommunityToolkit.Mvvm
- **Biểu đồ:** LiveChartsCore.SkiaSharpView.WPF
- **Mã hóa mật khẩu:** BCrypt.Net-Next
- **Quản lý biến môi trường:** DotNetEnv
- **Lưu trữ ảnh:** CloudinaryDotNet

## Chức năng chính

### 1. Đăng nhập và phân quyền

- Đăng nhập tài khoản theo vai trò.
- Phân quyền giao diện và chức năng theo loại người dùng.
- Hỗ trợ xử lý thông tin đăng nhập qua tầng `AuthService`.

### 2. Quản lý tour

- Thêm, sửa, xóa và tìm kiếm tour.
- Quản lý thông tin tour: tên tour, điểm đến, giá, mô tả, thời lượng, trạng thái.
- Quản lý lịch khởi hành của từng tour.
- Gán tài nguyên liên quan như khách sạn, phương tiện, điểm tham quan.

### 3. Quản lý booking

- Tạo và quản lý booking của khách hàng.
- Theo dõi trạng thái đặt tour.
- Quản lý số lượng khách, ngày khởi hành và thông tin thanh toán.
- Hỗ trợ danh sách booking trong giao diện quản trị.

### 4. Quản lý khách hàng

- Quản lý danh sách khách hàng.
- Xem thông tin cá nhân, lịch sử đặt tour.
- Cập nhật trạng thái hoặc thông tin người dùng.

### 5. Quản lý hướng dẫn viên

- Quản lý hồ sơ hướng dẫn viên.
- Theo dõi phân công tour.
- Quản lý đánh giá hướng dẫn viên.
- Hỗ trợ nghiệp vụ chấm điểm và thống kê chất lượng hướng dẫn viên.

### 6. Quản lý thanh toán

- Theo dõi danh sách thanh toán.
- Quản lý trạng thái thanh toán của booking.
- Phục vụ báo cáo doanh thu và công nợ.

### 7. Quản lý mã giảm giá

- Tạo, sửa, xóa mã khuyến mãi.
- Quản lý điều kiện áp dụng mã giảm giá.
- Áp dụng mã giảm giá vào booking/tour phù hợp.

### 8. Đánh giá tour và hướng dẫn viên

- Khách hàng có thể đánh giá tour.
- Khách hàng có thể đánh giá hướng dẫn viên.
- Admin có thể xem danh sách đánh giá và thống kê điểm.

### 9. Báo cáo và dashboard

- Thống kê số lượng tour, booking, khách hàng.
- Báo cáo doanh thu.
- Hiển thị biểu đồ trực quan bằng LiveCharts.

### 10. Thông báo

- Quản lý danh sách thông báo trong hệ thống.
- Hiển thị thông báo nghiệp vụ cho người dùng.

## Cấu trúc thư mục

```text
TourManagement/
│
├── VietTravel.slnx
├── database.sql
│
├── VietTravel.Core/
│   ├── Models/
│   └── VietTravel.Core.csproj
│
├── VietTravel.Data/
│   ├── Services/
│   │   ├── AuditLogService.cs
│   │   ├── AuthService.cs
│   │   ├── CloudinaryImageService.cs
│   │   ├── DepartureSlotService.cs
│   │   ├── EmailService.cs
│   │   ├── GuideRatingService.cs
│   │   ├── PromoCodeService.cs
│   │   └── TourRatingService.cs
│   ├── SupabaseClientFactory.cs
│   └── VietTravel.Data.csproj
│
└── VietTravel.UI/
    ├── App.xaml
    ├── App.xaml.cs
    ├── MainWindow.xaml
    ├── MainWindow.xaml.cs
    ├── Converters/
    ├── Fonts/
    ├── Helpers/
    ├── Models/
    ├── Services/
    ├── Themes/
    ├── UI/
    ├── ViewModels/
    │   ├── AdminShellViewModel.cs
    │   ├── BookingListViewModel.cs
    │   ├── CustomerListViewModel.cs
    │   ├── DashboardViewModel.cs
    │   ├── DepartureListViewModel.cs
    │   ├── GuideManagementViewModel.cs
    │   ├── LoginViewModel.cs
    │   ├── PaymentListViewModel.cs
    │   ├── PromoCodeManagementViewModel.cs
    │   ├── RatingManagementViewModel.cs
    │   ├── ReportViewModel.cs
    │   ├── TourListViewModel.cs
    │   └── UserManagementViewModel.cs
    ├── Views/
    └── VietTravel.UI.csproj
```

## Yêu cầu cài đặt

Trước khi chạy dự án, cần cài đặt:

- Visual Studio 2022 hoặc mới hơn.
- .NET SDK hỗ trợ `net10.0` và `net10.0-windows`.
- PostgreSQL hoặc Supabase project.
- Git.

Kiểm tra .NET SDK:

```bash
dotnet --version
```

## Cấu hình môi trường

Tạo file `.env` tại thư mục gốc của project:

```env
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_anon_or_service_key

CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

SMTP_HOST=your_smtp_host
SMTP_PORT=587
SMTP_USERNAME=your_email
SMTP_PASSWORD=your_email_password
SMTP_FROM=your_email
```

Tùy theo code thực tế trong `SupabaseClientFactory.cs`, `EmailService.cs` và `CloudinaryImageService.cs`, tên biến môi trường có thể cần điều chỉnh cho khớp.

## Cài đặt và chạy dự án

Clone repository:

```bash
git clone https://github.com/pon0212/TourManagement.git
cd TourManagement
```

Restore package:

```bash
dotnet restore
```

Build solution:

```bash
dotnet build
```

Chạy ứng dụng WPF:

```bash
dotnet run --project VietTravel.UI/VietTravel.UI.csproj
```

Hoặc mở file `VietTravel.slnx` bằng Visual Studio, chọn project `VietTravel.UI` làm Startup Project rồi bấm `Start`.

## Cơ sở dữ liệu

File `database.sql` dùng để khởi tạo database PostgreSQL/Supabase cho hệ thống.

Các nhóm bảng chính thường bao gồm:

- Người dùng / tài khoản.
- Tour du lịch.
- Lịch khởi hành.
- Booking.
- Thanh toán.
- Hướng dẫn viên.
- Đánh giá tour.
- Đánh giá hướng dẫn viên.
- Mã giảm giá.
- Thông báo.
- Khách sạn, phương tiện, điểm tham quan.

Cách khởi tạo database:

1. Tạo project Supabase hoặc database PostgreSQL.
2. Mở SQL Editor.
3. Chạy toàn bộ nội dung file `database.sql`.
4. Cập nhật thông tin kết nối vào file `.env`.
5. Chạy ứng dụng.

## Tài khoản mẫu

Tài khoản mẫu phụ thuộc vào dữ liệu seed trong `database.sql`. Sau khi import database, kiểm tra bảng người dùng/tài khoản để lấy thông tin đăng nhập.

Có thể bổ sung vào README sau khi xác nhận dữ liệu seed:

```text
Admin:
- Email/Tên đăng nhập: ...
- Mật khẩu: ...

Khách hàng:
- Email/Tên đăng nhập: ...
- Mật khẩu: ...

Hướng dẫn viên:
- Email/Tên đăng nhập: ...
- Mật khẩu: ...
```

## Ghi chú triển khai

- Không commit file `.env` chứa khóa thật lên GitHub.
- Nếu dùng Supabase, cần kiểm tra quyền bảng, RLS policy và API key.
- Nếu ứng dụng không kết nối được database, kiểm tra lại `SUPABASE_URL`, `SUPABASE_KEY` và trạng thái mạng.
- Nếu lỗi package, chạy lại:

```bash
dotnet restore
dotnet clean
dotnet build
```

- Nếu dùng Visual Studio, nên đặt `VietTravel.UI` là startup project.

## Hướng phát triển

- Hoàn thiện phân quyền chi tiết theo vai trò.
- Bổ sung xuất báo cáo Excel/PDF.
- Bổ sung gửi email tự động khi booking hoặc thanh toán.
- Bổ sung dashboard realtime.
- Bổ sung kiểm thử unit test cho tầng Core và Data.
- Tối ưu UI/UX cho các màn hình quản trị.

