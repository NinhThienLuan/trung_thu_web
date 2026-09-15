# 🖥️ Mô Tả Chi Tiết Tất Cả 14 Màn Hình (Full Screen Specifications)

Tài liệu này tả chi tiết **100% toàn bộ 14 màn hình** trong hệ thống (bao phủ toàn bộ các URL Routes trong `sitemap.md`), bao gồm các thành phần UI layout, luồng tương tác và 4 trạng thái màn hình (`Loading`, `Empty`, `Success`, `Error`) dành cho 2 lập trình viên Frontend (FE) và UI/UX Designer.

---

## 🌐 MỤC A: PHÂN HỆ PUBLIC PORTAL (KHÁCH HÀNG B2C & B2B)

---

### 📱 1. Trang Chủ (`/`)
- **Mục tiêu**: Quảng bá thương hiệu bánh Trung Thu tươi, Banner mùa vụ, danh mục sản phẩm hot và kêu gọi hành động (CTA) Ghép Hộp Custom / Nhận Báo Giá B2B.
- **Thành phần UI**:
  - Banner Hero: Slider khuyến mãi Early Bird & đếm ngược ngày đến Tết Trung Thu.
  - Quick Customizer Box Banner: CTA "Tự ghép vỏ hộp & In tên riêng".
  - Grid Sản Phẩm Hot: Top 6 vị bánh nướng/dẻo tươi bán chạy nhất kèm nhãn HSD (7-15 ngày).
  - B2B Corporate Section: Banner quà tặng doanh nghiệp + Nút "Tải hồ sơ ATTP".
- **4 UI States**:
  - `Loading`: Skeleton shimmer loader cho Hero Slider & Product Grid.
  - `Empty`: Khi chưa đến mùa vụ (Hiển thị banner đăng ký nhận thông báo mở bán).
  - `Success`: Tải đầy đủ banner, slider hoạt động trượt mượt mà.
  - `Error`: Lỗi tải dữ liệu sản phẩm ➔ Hiển thị nút "Tải lại trang".

---

### 📱 2. Danh Mục Sản Phẩm & Vỏ Hộp (`/catalog`)
- **Mục tiêu**: Hiển thị danh sách tất cả chiếc bánh lẻ và các loại mẫu vỏ hộp quà (Set 2, 4, 6 bánh).
- **Thành phần UI**:
  - Tab Switcher: `Bánh Nướng`, `Bánh Dẻo`, `Bánh Chay / Low-Sugar`, `Mẫu Vỏ Hộp`.
  - Bộ lọc (Filter): Lọc theo mức giá, theo loại nhân (Thập cẩm, Nhân ngọt, Trứng chảy).
  - Card Sản phẩm: Ảnh nét, Tên vị bánh, Giá lẻ, Badge HSD tươi (7-10 ngày / 10-15 ngày), Nút `Thêm vào giỏ` & Nút `Ghép hộp`.
- **4 UI States**:
  - `Loading`: 8 Skeleton cards nhấp nháy.
  - `Empty`: Khi chọn bộ lọc không có sản phẩm phù hợp ➔ "Không tìm thấy bánh phù hợp với bộ lọc".
  - `Success`: Hiển thị danh sách sản phẩm phân trang hoặc Infinite Scroll.
  - `Error`: Inline error toast "Không thể tải danh mục sản phẩm".

---

### 📱 3. Chi Tiết Sản Phẩm (`/catalog/[id]`)
- **Mục tiêu**: Cung cấp chi tiết thành phần nguyên liệu, hàm lượng đường, hướng dẫn bảo quản bánh tươi và nhãn HSD.
- **Thành phần UI**:
  - Gallery ảnh sản phẩm & zoom kính phóng đại.
  - Khối thông tin: Tên sản phẩm, SKU, Giá, Hạn sử dụng tươi, Ngày ra lò dự kiến.
  - Accordion chi tiết: Nguyên liệu (gà quay, lạp xưởng, mứt bí...), Hướng dẫn bảo quản (nhiệt độ phòng / ngăn mát).
  - Bộ chọn số lượng + Nút `Thêm vào giỏ hàng`.
- **4 UI States**:
  - `Loading`: Skeleton cho ảnh gallery & khối thông tin giá.
  - `Empty`: Sản phẩm không tồn tại / đã xóa ➔ Hiển thị 404 Not Found + Nút "Quay lại danh mục".
  - `Success`: Hiển thị thông tin chi tiết đầy đủ.
  - `Error`: Hết hàng trong kho ➔ Nút "Thêm vào giỏ" đổi thành "Hết hàng" (Disabled).

---

### 📱 4. Tự Ghép Hộp Quà & In Tên (`/custom-box`)
- **Mục tiêu**: Công cụ kéo/chọn loại vỏ hộp set 2/4/6 bánh, chọn bánh lẻ điền vào hộp, nhập nội dung in tên/lời chúc và preview trực quan.
- **Thành phần UI**:
  - Box Selector: Tabs `Set 2 Bánh`, `Set 4 Bánh`, `Set 6 Bánh`.
  - Interactive Slots: Khung vị trí $N$ ô trống bánh.
  - Drawer Bánh Lẻ: Grid danh sách bánh lẻ để bấm chọn điền vào ô trống.
  - Personalization Input: Input nhập chữ in vỏ hộp (Max 50 chars) + Live Canvas Preview.
  - Dropdown Thiệp & Textarea Lời chúc (Max 150 chars).
  - Sticky Bar: Tổng tiền + Tiến độ điền bánh (`3/4 bánh`) + Nút `Thêm Vào Giỏ Hàng`.
- **4 UI States**:
  - `Loading`: Skeleton loader cho danh mục bánh lẻ & vỏ hộp.
  - `Empty`: Chưa chọn vỏ hộp ➔ "Vui lòng chọn loại vỏ hộp để bắt đầu ghép bánh".
  - `Success`: Điền đủ bánh vào hộp ➔ Nút "Thêm Vào Giỏ Hàng" sáng xanh (Active).
  - `Error`: Chọn vị bánh lẻ đã HẾT TỒN KHO ➔ Toast lỗi "Vị bánh [X] vừa hết tồn kho".

---

### 📱 5. Form Đăng Ký Báo Giá B2B (`/b2b-quotation`)
- **Mục tiêu**: Tiếp nhận yêu cầu báo giá đặt sỉ cho doanh nghiệp, chọn lịch chia đợt giao bánh tươi và tải file logo.
- **Thành phần UI**:
  - Form Fields: Tên công ty, Người liên hệ, SĐT, Email, Số lượng dự kiến ($\ge 20$), Upload Logo (PNG/SVG/AI), Checkbox Chia đợt giao.
  - Section Hồ sơ ATTP: Link tải Giấy ATTP & Bản tự công bố.
- **4 UI States**:
  - `Loading`: Progress bar khi upload file Logo.
  - `Empty`: Ngoài mùa vụ ➔ Banner "Hệ thống Báo Giá B2B sẽ mở vào tháng 7 Âm lịch".
  - `Success`: Modal thông báo "Mã RFQ [Mã] đã gửi thành công. Sales sẽ liên hệ trong 2h".
  - `Error`: File logo quá 10MB ➔ Inline error "File đính kèm vượt quá 10MB".

---

### 📱 6. Hồ Sơ Năng Lực & ATTP (`/compliance`)
- **Mục tiêu**: Công khai chứng nhận An toàn thực phẩm, Bản tự công bố chất lượng bánh và mẫu hợp đồng mua bán B2B cho khách doanh nghiệp kiểm tra.
- **Thành phần UI**:
  - Viewer hiển thị file PDF giấy chứng nhận ATTP & Bản tự công bố.
  - Nút `Tải về trọn bộ Hồ sơ Pháp lý (Zip/PDF)`.
- **4 UI States**:
  - `Loading`: Spinner render PDF Viewer.
  - `Empty`: Chưa có file công bố ➔ "Hồ sơ đang được cập nhật".
  - `Success`: Hiển thị bản vẽ/ảnh chụp giấy chứng nhận sắc nét.
  - `Error`: Lỗi tải file PDF ➔ Link fallback "Tải trực tiếp file PDF tại đây".

---

### 📱 7. Giỏ Hàng (`/cart`)
- **Mục tiêu**: Xem danh sách hộp quà custom & bánh lẻ đã chọn, chỉnh sửa số lượng, nhập mã giảm giá (Early Bird Coupon).
- **Thành phần UI**:
  - List Items: Hình ảnh hộp/bánh, Tên vị bánh trong hộp, Dòng chữ in trên vỏ hộp, Đơn giá, Nút tăng/giảm số lượng & Nút Xóa.
  - Input Mã giảm giá + Nút `Áp dụng`.
  - Tóm tắt đơn hàng: Tiền bánh + Tiền vỏ hộp - Chiết khấu.
  - Nút `Tiến Hành Thanh Toán`.
- **4 UI States**:
  - `Loading`: Shimmer list item loader.
  - `Empty`: Giỏ hàng trống ➔ Icon giỏ hàng rỗng + Nút "Khám phá danh mục bánh".
  - `Success`: Hiển thị chính xác tổng tiền và danh sách sản phẩm.
  - `Error`: Mã giảm giá hết hạn / không hợp lệ ➔ Alert đỏ "Mã giảm giá không hợp lệ".

---

### 📱 8. Thanh Toán, Đặt Cọc & Đặt Lịch Giao (`/checkout`)
- **Mục tiêu**: Điền địa chỉ giao hàng, chọn Ngày nhận bánh tươi trong Mùa vụ, đặt cọc 50% (nếu in tên), tính phí vận chuyển & điền form VAT.
- **Thành phần UI**:
  - Form Thông tin người nhận: Họ tên, SĐT, Địa chỉ chi tiết.
  - Pre-order Date Picker: Chọn Ngày nhận bánh tươi (Âm/Dương Lịch).
  - Deposit Section: Cảnh báo đặt cọc 50% đối với đơn custom.
  - Corporate VAT Section: Form nhập MST, Tên công ty, Email nhận hóa đơn.
  - Shipping Fee Breakdown: Dòng Phí vận chuyển được tính.
  - Nút `Xác Nhận Đặt Hàng & Thanh Toán`.
- **4 UI States**:
  - `Loading`: Spinner khi tính Phí vận chuyển & Áp mã cọc.
  - `Empty`: Giỏ hàng trống truy cập checkout ➔ Redirect về `/catalog`.
  - `Success`: Đặt hàng thành công ➔ Chuyển sang màn hình Mã Đơn Hàng & QR Code Chuyển Khoản Cọc.
  - `Error`: Ngày chọn bị FULL Hạn Ngạch Xưởng ➔ Alert đỏ "Ngày [X] xưởng đã đạt hạn ngạch tối đa".

---

### 📱 9. Tra Cứu Đơn Hàng (`/order-tracking/[id]`)
- **Mục tiêu**: Khách hàng kiểm tra tiến độ đơn hàng (Đã cọc, Xưởng đang nướng bánh, Đã đóng gói, Đang giao).
- **Thành phần UI**:
  - Timeline Trạng thái: `Đã Nhận Đơn` ➔ `Đã Cọc 50%` ➔ `Xưởng Ra Lò Bánh` ➔ `Đã Đóng Hộp In Tên` ➔ `Đang Giao Hàng`.
  - Chi tiết đơn hàng: Lịch nhận bánh tươi (Âm/Dương Lịch), Nội dung in vỏ hộp, Thông tin chuyển khoản cọc.
- **4 UI States**:
  - `Loading`: Pulse animation trên thanh Timeline.
  - `Empty` / Not Found: Mã đơn hàng không tồn tại ➔ "Không tìm thấy thông tin đơn hàng".
  - `Success`: Hiển thị chính xác trạng thái thực tế của đơn.
  - `Error`: Lỗi hệ thống ➔ "Vui lòng liên hệ Hotline để tra cứu trực tiếp".

---

## 🔐 MỤC B: PHÂN HỆ ADMIN & STORE OWNER PORTAL

---

### 📱 10. Admin Dashboard Tổng Quan (`/admin/dashboard`)
- **Mục tiêu**: Báo cáo doanh số mùa vụ, tỷ lệ đơn B2C vs B2B, số lượng bánh đã bán và cảnh báo đầy tải xưởng.
- **Thành phần UI**:
  - Metric Cards: Tổng Doanh Thu Mùa Vụ, Tổng Đơn Hàng, Đơn Cần Đặt Cọc, Tỷ lệ Lấp Đầy Hạn Ngạch.
  - Chart: Biểu đồ doanh thu theo Ngày Âm Lịch (Tháng 7 Âm & Tháng 8 Âm).
  - Quick Alert List: Các ngày cận Rằm sắp vượt 90% Capacity Cap.
- **4 UI States**:
  - `Loading`: Dashboard Card Skeleton Loader.
  - `Empty`: Chưa có dữ liệu đơn hàng mùa vụ ➔ "Chưa có dữ liệu giao dịch trong mùa vụ này".
  - `Success`: Hiển thị biểu đồ & chỉ số trực quan.
  - `Error`: Lỗi tải báo cáo ➔ Alert "Không thể kết nối máy chủ dữ liệu".

---

### 📱 11. Admin Lịch Sản Xuất Song Lịch Âm/Dương (`/admin/calendar`)
- **Mục tiêu**: Xem tổng quan lịch trả bánh theo Ngày Âm & Dương Lịch, xem tổng bánh cần nướng từng ngày và xuất Phiếu ra lò bánh cho thợ.
- **Thành phần UI**:
  - Month Picker: Chọn xem theo Tháng Âm Lịch (Tháng 7 Âm, Tháng 8 Âm).
  - Grid Calendar: Các ô ngày hiển thị ngày Dương (to) và ngày Âm (nhỏ), kèm thanh tiến độ Capacity Cap `350/500 bánh`.
  - Drawer Chi tiết: Khi bấm 1 ngày ➔ Gom tổng bánh cần nướng theo vị (`200 Thập Cẩm`, `150 Đậu Xanh`) + Nút `In Phiếu Ra Lò` & `Khóa Ngày`.
- **4 UI States**:
  - `Loading`: Skeleton Grid Loader.
  - `Empty`: Ngày chọn không có đơn bánh tươi ➔ "Không có đơn nướng bánh ngày này".
  - `Success`: Hiển thị đầy đủ màu chỉ báo đơn và tiến độ xưởng.
  - `Error`: Lỗi tải lịch ➔ Alert Banner "Không thể tải dữ liệu lịch sản xuất".

---

### 📱 12. Quản Lý Đơn Hàng & Đặt Cọc (`/admin/orders`)
- **Mục tiêu**: Duyệt trạng thái cọc 50%, lọc đơn theo ngày giao Âm/Dương, xem nội dung custom in vỏ hộp và xuất Hóa đơn VAT.
- **Thành phần UI**:
  - Filter Tabs: `Tất cả`, `Chờ Cọc`, `Đã Cọc 50%`, `Chờ Nướng Bánh`, `Đã Hoàn Thành`.
  - Data Table: Mã Đơn, Tên Khách, SĐT, Ngày Nhận (Âm/Dương), Nội dung In Vỏ Hộp, Số Tiền Cọc, Trạng Thái.
  - Action Dropdown: `Duyệt Cọc`, `Xác Nhận Đã Xuất VAT`, `Hủy Đơn`.
- **4 UI States**:
  - `Loading`: Table Row Skeleton.
  - `Empty`: Danh sách đơn trống ➔ "Không tìm thấy đơn hàng phù hợp".
  - `Success`: Hiển thị bảng dữ liệu có phân trang.
  - `Error`: Lỗi duyệt cọc ➔ Toast "Cập nhật trạng thái thất bại".

---

### 📱 13. Quản Lý Yêu Cầu Báo Giá B2B (`/admin/b2b-leads`)
- **Mục tiêu**: Quản lý các đơn đăng ký sỉ B2B (RFQ), phân công Sales chăm sóc, tải file logo doanh nghiệp và cập nhật tiến độ đàm phán hợp đồng.
- **Thành phần UI**:
  - Kanban Board / List View: 5 cột trạng thái (`Mới tiếp nhận`, `Đã liên hệ`, `Đã gửi Báo giá PDF`, `Chốt đơn (WON)`, `Thất bại (LOST)`).
  - Card Lead: Tên công ty, Người liên hệ, SĐT, Số lượng dự kiến, File Logo đính kèm.
- **4 UI States**:
  - `Loading`: Kanban Column Skeleton.
  - `Empty`: Chưa có Yêu cầu báo giá B2B ➔ "Chưa có yêu cầu báo giá mới".
  - `Success`: Kéo thả Card Lead giữa các cột trạng thái mượt mà.
  - `Error`: Lỗi đổi trạng thái Lead ➔ Revert card về vị trí cũ.

---

### 📱 14. Quản Lý Tồn Kho Đa Tầng & Hạn Ngạch Xưởng (`/admin/inventory`)
- **Mục tiêu**: Cập nhật số lượng tồn kho từng loại vỏ hộp, vị bánh lẻ và thiết lập Hạn ngạch nướng bánh (Capacity Cap) cho từng ngày.
- **Thành phần UI**:
  - Section 1: Quản lý Kho Vỏ Hộp (Set 2, 4, 6) & Vị Bánh Lẻ.
  - Section 2: Quản lý Capacity Cap (Nhập số lượng bánh nướng tối đa/ngày, mặc định 500 chiếc/ngày).
- **4 UI States**:
  - `Loading`: Spinner loader cho bảng tồn kho.
  - `Empty`: Danh sách vật tư rỗng ➔ "Chưa khai báo danh mục tồn kho".
  - `Success`: Cập nhật kho thời gian thực.
  - `Error`: Nhập hạn ngạch $< 0$ ➔ Inline error "Hạn ngạch phải là số nguyên lớn hơn 0".
