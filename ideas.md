# 💡 Ý Tưởng Sản Phẩm: Nền Tảng Bán Bánh Trung Thu Trực Tuyến

## 1. Bối Cảnh & Vấn Đề Cốt Lõi (Context & Problem)
Thị trường bánh Trung Thu trực tuyến có các rủi ro vận hành và bài toán đặc thù cần giải quyết:
- **Khung thời gian mùa vụ (Seasonality Window)**: Mùa bánh kéo dài từ **1.5 đến 2 tháng** (từ khoảng đầu tháng 7 Âm lịch đến ngày Rằm tháng 8 Âm lịch), cao điểm mua sắm dồn vào 30 ngày trước Tết Trung Thu.
- **Thời hạn sử dụng bánh tươi (Fresh Shelf Life)**: Bánh Trung Thu tươi có hạn sử dụng ngắn, chỉ từ **7 đến 15 ngày** (bánh dẻo tươi: 7-10 ngày, bánh nướng tươi: 10-15 ngày).
- **Rủi ro bùng đơn đối với đơn Customize**: Bánh và vỏ hộp đã in tên/logo riêng không thể bán lại cho khách khác nếu bị hủy đơn $\rightarrow$ Cần cơ chế **đặt cọc trước $\ge 50\%$**.
- **Bài toán Pháp lý & Hồ sơ ATTP cho B2B**: Doanh nghiệp mua bánh sỉ luôn yêu cầu Giấy chứng nhận An toàn thực phẩm, Bản công bố chất lượng và Hóa đơn VAT $\rightarrow$ Cần trang công khai & tải xuống Hồ sơ năng lực.
- **Bài toán Tồn kho Đa tầng**: Đơn hàng kết hợp 1 vỏ hộp + $N$ vị bánh lẻ $\rightarrow$ Cần quản lý tồn kho đồng thời thời gian thực.
- **Bài toán Quản lý Lịch ra lò cho Chủ cửa hàng / Quản lý trang**:
  - Quản lý đơn hàng trực quan hiển thị song song **Ngày Dương Lịch và Ngày Âm Lịch** (ví dụ: `25/09/2026 (15/08 Âm Lịch)`).
  - Tự động gom tổng số chiếc bánh từng loại cần nướng theo ngày & Quản lý hạn ngạch nướng bánh (Capacity Cap).

---

## 2. Đối Tượng Người Dùng Mục Tiêu (3 Core Actors)

### 🛒 1. Bên Mua (Buyers - Gộp Cá Nhân & Doanh Nghiệp / B2C & B2B)
- **Nhu cầu**: 
  - Mua bánh lẻ / ghép bộ hộp quà (Set 2, 4, 6 bánh) + Customize in tên/lời chúc (Live Preview) & thiệp chúc.
  - Chọn ngày nhận bánh tươi theo **Lịch Âm/Dương Lịch**.
  - Thanh toán trực tuyến hoặc **Đặt cọc trước $\ge 50\%$** đối với đơn custom.
  - Có tùy chọn đăng ký **Yêu cầu Báo Giá mua sỉ**, đính kèm logo in ấn, yêu cầu chia đợt giao bánh tươi & nhập thông tin **Xuất Hóa đơn VAT**.

### 🏪 2. Bên Bán (Sellers / Cửa Hàng / Quản Lý Biz)
- **Nhu cầu**: 
  - Quản lý danh mục sản phẩm bánh tươi, mẫu vỏ hộp & tồn kho đa tầng thời gian thực.
  - Xử lý & chuyển đổi trạng thái đơn hàng (Chờ cọc, Đã cọc, Đang nướng, Đang giao, Hoàn thành).
  - Quản lý **Dashboard Lịch Sản Xuất Song Lịch Âm/Dương** (`25/09/2026 (15/08 Âm Lịch)`).
  - Thiết lập **Hạn ngạch nướng bánh theo ngày (Daily Capacity Cap)** và tự động gom tổng chiếc bánh cần nướng theo ngày (Daily Production Sheet).

### 👑 3. Chủ Trang Web Trung Gian (Platform Admin - Bạn)
- **Nhu cầu**: 
  - Quản lý danh sách các Cửa hàng / Bên bán trên nền tảng.
  - Giám sát toàn bộ lưu lượng giao dịch, đơn hàng và báo cáo tổng quan nền tảng.
  - Cấu hình các thiết lập chung toàn trang web.

---

## 3. Phạm Vi Tính Năng MVP (Minimum Viable Product Scope)

### 🛒 3.1. Luồng B2C - Mua Bánh Lẻ & Customize Hộp Quà (Có Lịch Giao Bánh Tươi)
1. **Catalog Bánh Tươi & Vỏ Hộp (Mooncake Showcase)**:
   - Danh mục vị bánh lẻ kèm nhãn HSD (7-15 ngày) & Tồn kho đa tầng thời gian thực.
   - Danh mục vỏ hộp cao cấp (Set 2, 4, 6 bánh).
2. **Bộ Công Cụ Ghép Hộp, In Tên & Thiệp Chúc (Box & Card Customizer)**:
   - Ghép bánh lẻ vào vỏ hộp + Customize in tên lên vỏ hộp (Live Preview).
   - Nhập nội dung **Thiệp chúc mừng Tết Trung Thu** đi kèm.
3. **Giỏ Hàng, Đặt Cọc & Chọn Ngày Nhận (Checkout & Deposit Flow)**:
   - Bắt buộc đặt cọc $\ge 50\%$ đối với đơn in tên riêng.
   - Chọn ngày nhận bánh tươi (Pre-order schedule) & Tính phí vận chuyển.

### 📋 3.2. Luồng B2B - Yêu Cầu Báo Giá & Hồ Sơ Pháp Lý
1. **Trang Hồ Sơ Năng Lực & ATTP**: Tải chứng nhận ATTP, Tự công bố sản phẩm & Hợp đồng mẫu.
2. **Form Yêu Cầu Báo Giá (B2B RFQ Form)**: Nhập số lượng, đợt giao, thông tin xuất hóa đơn VAT & gửi Lead cho Sales.

### 📅 3.3. Luồng Quản Lý Dành Cho Chủ Cửa Hàng / Quản Lý Trang (Admin Production Calendar)
1. **Dashboard Lịch Song Lịch (Dual Calendar View)**: Xem đơn hàng theo Ngày Dương & Âm Lịch.
2. **Kế Hoạch Ra Lò Bánh Tươi Tự Động (Auto Production Sheet)**: Gom tổng số lượng chiếc bánh cần nướng theo ngày.
3. **Quản Lý Hạn Ngạch Sản Xuất & Đơn Cọc**: Quản lý hạn ngạch ngày & trạng thái cọc/VAT của đơn hàng.

---

## 4. Mục Tiêu Tiếp Theo (Next Steps)
1. Xây dựng **Từ điển thuật ngữ (Glossary)** chuẩn hóa khái niệm (`ba/01-overview/glossary.md`).
2. Viết chi tiết **Business Rules** cho B2C (`BR-01`), B2B (`BR-02`), Dynamic Pricing (`BR-03`), Admin Calendar (`BR-04`) và Operational Risks (`BR-05`).

---

## 🏛️ 5. Mô Hình Kinh Doanh Sàn Nền Tảng (Marketplace Business Model)
- **Mô hình Sàn Trung Gian (Two-Sided Marketplace)**:
  - **Bên Bán (Sellers)**: Quản lý bánh tươi, vỏ hộp, cấu hình Lịch nướng Âm/Dương và vận hành xưởng.
  - **Bên Mua (Buyers)**: Chọn mua bánh lẻ, ghép hộp custom in tên/thiệp, cọc 50% & chọn ngày giao.
  - **Platform Admin (Bạn)**: Cung cấp hạ tầng công nghệ, quản lý gian hàng & thu phí hoa hồng.
- **Nguồn Thu Doanh Thu (Revenue Streams)**:
  1. *Phí hoa hồng giao dịch (Transaction Commission)*: Thu 5% - 10% (B2C lẻ) & 3% - 5% (B2B sỉ).
  2. *Gói đăng ký gian hàng Seller (Season Pass Subscription)*: Gói Pro cho Seller mở tính năng Lịch Âm/Dương & gom phiếu ra lò.
  3. *Phí dịch vụ VAS*: In ấn vỏ hộp/thiệp chiết khấu từ đối tác & chênh lệch giao nhận.
  4. *Quảng cáo Banner & Top Listing*: Vị trí ưu tiên cho các gian hàng nổi bật.
- **Phân Loại 2 Nhóm Seller**:
  - *Hãng lớn (như Kinh Đô)*: Bán thuần mùa vụ (Thuê gian hàng 2 tháng cao điểm Tết Trung Thu, giao ngay theo tồn kho sẵn).
  - *Tiệm nhỏ / Handmade*: Bán quanh năm hoặc Hybrid (nhận Pre-order bánh tươi theo mốc ngày Âm/Dương, chuyển sang bán Bánh Lễ Rằm/Mùng 1 hoặc Hộp Quà Tết ngoài mùa vụ).
