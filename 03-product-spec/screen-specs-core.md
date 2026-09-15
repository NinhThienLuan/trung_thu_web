# 🖥️ Mô Tả Chi Tiết Các Màn Hình Cốt Lõi (Core Screen Specifications)

Tài liệu này tập trung mô tả chi tiết **4 Màn Hình Cốt Lõi (Core Screens)** phức tạp nhất của Nền Tảng Bán Bánh Trung Thu. Dành cho nhóm phát triển nhanh MVP và thiết kế UI/UX ưu tiên.

---

## 📱 1. Màn Hình Cốt Lõi 1: Tự Ghép Hộp Quà & In Tên (`/custom-box`)

### 1.1. Mục Tiêu Màn Hình
Cho phép người dùng chọn vỏ hộp (set 2, 4, 6 bánh), gắp từng chiếc bánh lẻ điền đầy dung tích hộp, nhập nội dung in tên/lời chúc lên vỏ hộp và xem trước kết quả trực quan (Live Preview).

### 1.2. Các Thành Phần Giao Diện (UI Layout Components)
- **Khu vực 1: Box Selector (Thanh chọn loại vỏ hộp)**: Radio buttons `Set 2 Bánh`, `Set 4 Bánh`, `Set 6 Bánh`.
- **Khu vực 2: Interactive Box Slots (Khung vị trí bánh)**: $N$ ô trống chứa bánh lẻ.
- **Khu vực 3: Loose Mooncake Drawer**: Grid bánh lẻ (Ảnh, Tên, Giá, HSD 7-15 ngày, Nút `Chọn`).
- **Khu vực 4: Personalization Panel**: Input văn bản in vỏ hộp (Max 50 chars) + Live Canvas Preview + Dropdown thiệp chúc.
- **Khu vực 5: Sticky Summary Bar**: Tổng tiền + Tiến độ điền bánh (`3/4 bánh`) + Nút `Thêm Vào Giỏ Hàng`.

### 1.3. Bốn Trạng Thái Giao Diện (4 UI States)
```
[Loading State]  ──► Skeleton Shimmer loader cho danh mục bánh lẻ & vỏ hộp.
[Empty State]    ──► "Vui lòng chọn loại vỏ hộp (Set 2, 4, hoặc 6) để bắt đầu".
[Success State]  ──► Điền đủ bánh vào hộp, nút "Thêm Vào Giỏ Hàng" sáng xanh (Active).
[Error State]    ──► Vị bánh chọn vừa hết tồn kho ➔ Toast "Vị bánh [X] tạm thời hết kho".
```

---

## 🛒 2. Màn Hình Cốt Lõi 2: Thanh Toán, Đặt Cọc & Đặt Lịch Giao (`/checkout`)

### 2.1. Mục Tiêu Màn Hình
Thu thập thông tin người nhận, chọn ngày nhận bánh tươi trong Mùa vụ, đặt cọc 50% (nếu in tên), tính phí vận chuyển và nhập thông tin xuất Hóa đơn VAT.

### 2.2. Các Thành Phần Giao Diện (UI Layout Components)
- **Khu vực 1: Form Người Nhận**: Họ tên, SĐT, Địa chỉ chi tiết.
- **Khu vực 2: Pre-order Fresh Delivery Scheduler**: Date Picker chọn ngày nhận bánh tươi trong Mùa vụ.
- **Khu vực 3: Deposit & Payment**: Bắt buộc đặt cọc 50% đối với đơn in tên custom.
- **Khu vực 4: Corporate VAT Form**: Form MST, Tên công ty, Email nhận hóa đơn VAT.
- **Khu vực 5: Order Summary Panel**: Chi tiết tiền bánh, vỏ hộp, cước ship, hệ số cao điểm & nút `Xác Nhận Đặt Hàng`.

### 2.3. Bốn Trạng Thái Giao Diện (4 UI States)
```
[Loading State]  ──► Spinner loader khi tính toán Phí Vận Chuyển & Đặt cọc.
[Empty State]    ──► Giỏ hàng trống ➔ Redirect về /catalog kèm Toast thông báo.
[Success State]  ──► Đặt hàng thành công ──► Hiển thị Mã Đơn Hàng & QR Code Chuyển Khoản Cọc.
[Error State]    ──► Ngày chọn bị FULL Hạn Ngạch Xưởng ➔ Alert "Ngày [X] xưởng đã đạt hạn ngạch tối đa".
```

---

## 📋 3. Màn Hình Cốt Lõi 3: Form Đăng Ký Báo Giá B2B (`/b2b-quotation`)

### 3.1. Mục Tiêu Màn Hình
Thu thập yêu cầu báo giá sỉ cho doanh nghiệp, đính kèm file logo in hộp và chọn lịch chia đợt giao bánh tươi.

### 3.2. Các Thành Phần Giao Diện (UI Layout Components)
- **Form Fields**: Tên công ty, Người liên hệ, SĐT, Email, Số lượng dự kiến ($\ge 20$), Upload Logo (PNG/SVG/AI), Checkbox Chia đợt giao bánh, Ghi chú.
- **Section Hồ sơ ATTP**: Link tải Giấy chứng nhận ATTP, Tự công bố sản phẩm & Hợp đồng mẫu.

### 3.3. Bốn Trạng Thái Giao Diện (4 UI States)
```
[Loading State]  ──► Progress bar khi tải file Logo doanh nghiệp lên server.
[Empty State]    ──► Ngoài mùa vụ ➔ Banner "Hệ thống Báo Giá B2B sẽ mở vào tháng 7 Âm lịch".
[Success State]  ──► Modal "Mã RFQ [Mã] đã gửi thành công. Sales sẽ liên hệ trong 2h".
[Error State]    ──► Dung lượng file Logo > 10MB ➔ Inline Error "File vượt quá 10MB".
```

---

## 📅 4. Màn Hình Cốt Lõi 4: Admin Lịch Sản Xuất Song Lịch Âm/Dương (`/admin/calendar`)

### 4.1. Mục Tiêu Màn Hình
Dành cho Chủ cửa hàng & Quản lý trang xem tổng quan lịch trả bánh theo Ngày Âm Lịch & Dương Lịch, xem tổng bánh cần nướng từng ngày và xuất Phiếu ra lò bánh cho thợ.

### 4.2. Các Thành Phần Giao Diện (UI Layout Components)
- **Control Bar**: Xem theo Tháng Âm Lịch (Tháng 7 Âm, Tháng 8 Âm) hoặc Dương Lịch.
- **Grid Calendar**: Ô ngày hiển thị song song Ngày Dương & Âm, kèm thanh tiến độ Capacity Cap `350/500 bánh`.
- **Daily Drawer**: Gom tổng số bánh cần nướng theo vị trong ngày + Nút `In Phiếu Ra Lò` & `Khóa Ngày`.

### 4.3. Bốn Trạng Thái Giao Diện (4 UI States)
```
[Loading State]  ──► Grid Skeleton Loader khi chuyển đổi giữa các tháng.
[Empty State]    ──► Ngày chọn không có đơn bánh ➔ "Không có đơn nướng bánh ngày này".
[Success State]  ──► Hiển thị đầy đủ màu chỉ báo đơn và tiến độ xưởng.
[Error State]    ──► Lỗi tải lịch ➔ Alert Banner "Không thể tải dữ liệu lịch sản xuất".
```
