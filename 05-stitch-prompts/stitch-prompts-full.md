# 🎨 Bộ Stitch UI Prompts Cho Tất Cả 14 Màn Hình (Full 14 Screens)

Tài liệu này chứa danh sách trọn vẹn **14 Stitch UI Prompts** (bao phủ 100% tất cả các URL Routes trong `sitemap.md` và `screen-specs-full.md`).

---

## 🌐 MỤC A: PUBLIC PORTAL PROMPTS

### 1. Route `/` - Trang Chủ
```markdown
Generate a high-converting Mooncake E-commerce Home Page UI.
Theme: Deep Red (#9B1C1C) & Gold (#D97706).
Components: Hero Banner Slider (Early Bird promotion + Mid-Autumn Countdown timer), Quick Custom Box CTA Section ("Tự ghép vỏ hộp & In tên"), Featured Fresh Mooncakes Grid (Top 6 flavors with HSD 7-15 days badges), Corporate B2B Section with "Tải hồ sơ ATTP" CTA.
4 UI States: Loading (Skeleton), Empty (Off-season banner), Success (Full hero & slider), Error (Retry button).
```

### 2. Route `/catalog` - Danh Mục Sản Phẩm
```markdown
Generate a Mooncake Product Catalog & Gift Box Catalog Grid UI.
Components: Tab Switcher (Bánh Nướng, Bánh Dẻo, Bánh Chay/Low-Sugar, Mẫu Vỏ Hộp), Filter sidebar (Price range, Flavor type), Product Cards with fresh shelf life badge (HSD 7-10 ngày / 10-15 ngày), "Thêm vào giỏ" & "Ghép hộp" buttons.
4 UI States: Loading (8 Skeleton cards), Empty ("Không tìm thấy bánh phù hợp"), Success (Paginated grid), Error (Inline error toast).
```

### 3. Route `/catalog/[id]` - Chi Tiết Sản Phẩm
```markdown
Generate a detailed Product Specification Detail Page UI for fresh mooncakes.
Components: Image gallery with zoom preview, Product Title, SKU, Price, Fresh Shelf Life badge, Ra Lò Date estimate, Ingredient Accordion (Gà quay, Mứt bí, Trứng muối...), Storage Instructions (Room temp / Refrigerator), Quantity selector, "Thêm vào giỏ hàng" button.
4 UI States: Loading (Image & info skeletons), Empty (404 Not Found), Success (Full specs), Error (Disabled "Hết hàng" button).
```

### 4. Route `/custom-box` - Tự Ghép Hộp Quà & In Tên
*(Xem chi tiết Stitch Prompt tại [`stitch-prompts-core.md`](file:///d:/GitHub/Luan_ai_workflow/ba/05-stitch-prompts/stitch-prompts-core.md#1-stitch-prompt-t%E1%BB%B1-gh%C3%A9p-h%E1%BB%99p-qu%C3%A0--in-t%C3%AAn-custom-box))*

### 5. Route `/b2b-quotation` - Form Đăng Ký Báo Giá B2B
*(Xem chi tiết Stitch Prompt tại [`stitch-prompts-core.md`](file:///d:/GitHub/Luan_ai_workflow/ba/05-stitch-prompts/stitch-prompts-core.md#3-stitch-prompt-form-%C4%91%C4%83ng-k%C3%BD-b%C3%A1o-gi%C3%A1-b2b-b2b-quotation))*

### 6. Route `/compliance` - Hồ Sơ Năng Lực & ATTP
```markdown
Generate a Corporate Food Safety & Compliance Documentation Page UI.
Components: PDF Viewer embed showing Food Safety Certificates (Giấy ATTP), Product Quality Self-Declarations, and Sample B2B Sales Contract. Large "Tải về trọn bộ Hồ sơ Pháp lý (ZIP/PDF)" button.
4 UI States: Loading (PDF spinner), Empty ("Hồ sơ đang được cập nhật"), Success (Crisp document viewer), Error (Direct PDF download link fallback).
```

### 7. Route `/cart` - Giỏ Hàng
```markdown
Generate a Mooncake Cart Page UI supporting custom gift boxes.
Components: List of Cart Items (Custom Box item showing selected box shell, loose cake flavors inside, custom printed text, unit price, quantity modifier, remove button), Early Bird Coupon Code Input with "Áp dụng" button, Summary Card (Cake Total, Box Shell Total, Discount, Checkout Button).
4 UI States: Loading (List skeletons), Empty (Empty cart illustration + "Khám phá danh mục bánh"), Success (Accurate total calculation), Error (Invalid coupon alert).
```

### 8. Route `/checkout` - Thanh Toán, Đặt Cọc & Đặt Lịch Giao
*(Xem chi tiết Stitch Prompt tại [`stitch-prompts-core.md`](file:///d:/GitHub/Luan_ai_workflow/ba/05-stitch-prompts/stitch-prompts-core.md#2-stitch-prompt-thanh-to%C3%A1n-%C4%91%E1%BA%B7t-c%E1%BB%8Dc--%C4%91%E1%BA%B7t-l%E1%BB%8Bch-giao-checkout))*

### 9. Route `/order-tracking/[id]` - Tra Cứu Đơn Hàng
```markdown
Generate a Customer Order Tracking Status Page UI for fresh mooncakes.
Components: Horizontal Order Timeline (Đã Nhận Đơn -> Đã Cọc 50% -> Xưởng Ra Lò Bánh -> Đã Đóng Hộp In Tên -> Đang Giao Hàng), Expected Delivery Date (Solar & Lunar), Order Summary, Banking Deposit Receipt Status.
4 UI States: Loading (Timeline pulse animation), Empty/Not Found ("Không tìm thấy đơn hàng"), Success (Live status tracking), Error ("Liên hệ Hotline tra cứu").
```

---

## 🔐 MỤC B: ADMIN PORTAL PROMPTS

### 10. Route `/admin/dashboard` - Dashboard Tổng Quan
```markdown
Generate a Store Owner Executive Dashboard UI for Mid-Autumn Festival Sales.
Components: Metric Cards (Total Season Revenue, Total Orders, Pending Deposit Orders, Bakery Capacity Fill Rate), Revenue Bar Chart grouped by Lunar Dates (Tháng 7 Âm & Tháng 8 Âm), Urgent Capacity Risk Alert Widget.
4 UI States: Loading (Metric card skeletons), Empty ("Chưa có dữ liệu mùa vụ"), Success (Live charts), Error (Server connection failure).
```

### 11. Route `/admin/calendar` - Lịch Sản Xuất Song Lịch Âm/Dương
*(Xem chi tiết Stitch Prompt tại [`stitch-prompts-core.md`](file:///d:/GitHub/Luan_ai_workflow/ba/05-stitch-prompts/stitch-prompts-core.md#4-stitch-prompt-admin-l%E1%BB%8Bch-s%E1%BA%A3n-xu%E1%BA%A5t-song-l%E1%BB%8Bch-%C3%A2md%C6%B0%C6%A1ng-admincalendar))*

### 12. Route `/admin/orders` - Quản Lý Đơn Hàng & Đặt Cọc
```markdown
Generate a Store Admin Order & Deposit Management Table UI.
Components: Filter Tabs (Tất cả, Chờ Cọc, Đã Cọc 50%, Chờ Nướng Bánh, Hoàn Thành), Data Table with columns (Order ID, Customer Name, Phone, Delivery Date Solar/Lunar, Custom Printed Text, Deposit Amount, Status), Action Dropdown (Duyệt Cọc, Xác nhận VAT, Hủy Đơn).
4 UI States: Loading (Row skeletons), Empty ("Không tìm thấy đơn hàng"), Success (Paginated table), Error (Status update error toast).
```

### 13. Route `/admin/b2b-leads` - Quản Lý Yêu Cầu Báo Giá B2B
```markdown
Generate a Sales CRM Kanban Board UI for Mooncake B2B RFQ Leads.
Components: Kanban Columns (Mới tiếp nhận, Đã liên hệ, Đã gửi Báo giá PDF, Chốt đơn WON, Thất bại LOST), Lead Cards (Company Name, Contact Person, Phone, Estimated Quantity, Uploaded Logo File link, Assign Sales Rep button).
4 UI States: Loading (Column skeletons), Empty ("Chưa có yêu cầu báo giá mới"), Success (Smooth drag-and-drop lead cards), Error (Revert card position on network error).
```

### 14. Route `/admin/inventory` - Quản Lý Tồn Kho & Hạn Ngạch Xưởng
```markdown
Generate a Store Admin Real-time Multi-level Inventory & Daily Capacity Cap Management UI.
Components: Section 1 (Table of Loose Mooncake Flavors & Box Shell Items with stock count input fields), Section 2 (Daily Production Capacity Cap Setting Widget - Default 500 cakes/day, date-override input).
4 UI States: Loading (Table spinner), Empty ("Chưa khai báo danh mục kho"), Success (Real-time stock update), Error (Invalid capacity input < 0 error).
```
