# 🗺️ Sơ Đồ Cấu Trúc Trang & Điều Hướng (Sitemap & Navigation Routes)

Tài liệu này định nghĩa cấu trúc cây thư mục trang, danh sách URL Routes, các luồng chuyển trang và phân quyền truy cập cho **Nền Tảng Bán Bánh Trung Thu**.

---

## 1. Cấu Trúc Cây Sitemap Tổng Quan (Sitemap Tree)

```
[Nền Tảng Bán Bánh Trung Thu]
 ├── 🌐 PUBLIC PORTAL (Khách mua lẻ B2C & Khách doanh nghiệp B2B)
 │    ├── / (Trang chủ / Home Page)
 │    ├── /catalog (Danh mục Bánh lẻ & Vỏ hộp)
 │    │    └── /catalog/[id] (Chi tiết sản phẩm Bánh/Hộp)
 │    ├── /custom-box (Bộ công cụ Ghép Hộp tùy chỉnh & In tên/logo)
 │    ├── /b2b-quotation (Form đăng ký Báo giá Doanh nghiệp B2B)
 │    ├── /compliance (Hồ sơ năng lực & Chứng nhận ATTP)
 │    ├── /cart (Giỏ hàng)
 │    ├── /checkout (Thanh toán, Đặt cọc 50%, Đặt lịch giao bánh tươi & VAT)
 │    └── /order-tracking/[orderId] (Tra cứu đơn hàng)
 │
 └── 🔐 ADMIN & STORE OWNER PORTAL (Chủ cửa hàng & Quản lý trang)
      ├── /admin/login (Đăng nhập Admin)
      ├── /admin/dashboard (Tổng quan doanh số & Lịch sản xuất)
      ├── /admin/calendar (Lịch Sản Xuất Song Lịch Âm/Dương)
      ├── /admin/orders (Quản lý danh sách đơn hàng B2C/B2B & Đặt cọc)
      ├── /admin/b2b-leads (Quản lý Yêu cầu báo giá B2B RFQ)
      └── /admin/inventory (Quản lý Tồn kho đa tầng & Hạn ngạch ngày)
```

---

## 2. Danh Sách URL Routes & Phân Quyền Truy Cập (Route Matrix)

| URL Route | Tên Màn Hình | Vai Trò Cho Phép | Mục Đích Sử Dụng |
| :--- | :--- | :--- | :--- |
| `/` | Trang chủ (Home) | Public (Tất cả) | Giới thiệu thương hiệu, Banner mùa vụ, Bánh hot & Khuyến mãi Early Bird. |
| `/catalog` | Danh mục Sản phẩm | Public (Tất cả) | Hiển thị vị bánh lẻ (kèm HSD 7-15 ngày) & Các mẫu vỏ hộp set 2, 4, 6. |
| `/catalog/[id]` | Chi tiết Sản phẩm | Public (Tất cả) | Xem chi tiết thành phần, nhân bánh, hướng dẫn bảo quản & nút thêm giỏ. |
| `/custom-box` | Tự Ghép Hộp Quà | Public (Tất cả) | Chọn vỏ hộp set 2/4/6 + Gắp bánh lẻ + Live preview in tên/lời chúc. |
| `/b2b-quotation` | Báo Giá B2B | Public (Tất cả) | Form gửi thông tin sỉ, đính kèm logo, chọn lịch chia đợt giao bánh tươi. |
| `/compliance` | Hồ Sơ Pháp Lý & ATTP | Public (Tất cả) | Công khai chứng nhận ATTP, Tự công bố sản phẩm & Hợp đồng mẫu. |
| `/cart` | Giỏ Hàng | Public (Tất cả) | Xem danh sách hộp custom/bánh lẻ, thay đổi số lượng, nhập coupon. |
| `/checkout` | Thanh Toán & Đặt Lịch | Public (Tất cả) | Chọn ngày nhận bánh tươi, Đặt cọc 50% (nếu in tên), Xuất Hóa đơn VAT. |
| `/order-tracking/[id]` | Tra Cứu Đơn Hàng | Public (Tất cả) | Kiểm tra trạng thái đơn hàng & lịch ra lò bánh qua Mã đơn hàng + SĐT. |
| `/admin/login` | Đăng Nhập Admin | Public (Unauthenticated) | Trang đăng nhập dành cho Quản lý trang & Chủ cửa hàng. |
| `/admin/dashboard` | Dashboard Tổng Quan | Seller, Platform Admin | Thống kê doanh thu mùa vụ, tỷ lệ đơn lẻ/sỉ, cảnh báo đầy tải xưởng. |
| `/admin/calendar` | Lịch Sản Xuất Âm/Dương | Seller, Platform Admin | Xem lịch trả bánh theo ngày Âm/Dương, xuất Phiếu nướng bánh cho xưởng. |
| `/admin/orders` | Quản Lý Đơn Hàng | Seller, Platform Admin | Duyệt đơn cọc, cập nhật trạng thái thanh toán & lịch giao hàng. |
| `/admin/b2b-leads` | Quản Lý RFQ B2B | Seller, Platform Admin | Tiếp nhận Lead sỉ, tư vấn báo giá & đàm phán hợp đồng. |
| `/admin/inventory` | Tồn Kho & Hạn Ngạch | Seller, Platform Admin | Cập nhật số lượng vỏ hộp, vị bánh lẻ và cài đặt Capacity Cap ngày. |

---

## 3. Sơ Đồ Điều Hướng Luồng Người Dùng Chính (Navigation Flow Diagrams)

### 🛍️ Luồng 1: Khách hàng B2C Mua Hộp Quà Tùy Chỉnh (Custom Box Flow)
`Trang chủ / Catalog` ➔ `Custom Box Builder (/custom-box)` ➔ `Nhập tên in vỏ hộp & Thiệp` ➔ `Giỏ hàng (/cart)` ➔ `Checkout (/checkout)` *(Chọn ngày nhận bánh tươi + Đặt cọc 50%)* ➔ `Xác nhận Đơn hàng (/order-tracking/[id])`.

### 🏢 Luồng 2: Khách hàng Doanh Nghiệp Đặt Báo Giá Sỉ (B2B RFQ Flow)
`Trang chủ` ➔ `Trang Báo Giá B2B (/b2b-quotation)` ➔ `Tải Hồ sơ ATTP (/compliance)` ➔ `Điền Form RFQ (Số lượng, Logo, Chia đợt giao)` ➔ `Gửi Yêu Cầu` ➔ `Email Xác Nhận RFQ` ➔ `Sales liên hệ tư vấn thủ công`.

### 👨‍🍳 Luồng 3: Quản Lý Trang / Chủ Cửa Hàng Gom Đơn Nướng Bánh (Admin Calendar Flow)
`Đăng nhập Admin (/admin/login)` ➔ `Lịch Sản Xuất (/admin/calendar)` ➔ `Chọn Tháng Âm Lịch (VD: Tháng 8 Âm)` ➔ `Chọn Ngày cụ thể` ➔ `Tự động dồn đơn & In Phiếu Ra Lò Bánh` ➔ `Chuyển xưởng sản xuất`.
