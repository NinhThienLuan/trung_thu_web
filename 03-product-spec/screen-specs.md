# 🖥️ Tổng Quan Mô Tả Giao Diện Màn Hình (Screen Specifications Index)

Thư mục này chứa tài liệu mô tả chi tiết giao diện màn hình, luồng tương tác và 4 trạng thái UI (`Loading`, `Empty`, `Success`, `Error`) được phân chia thành 2 file phục vụ cho các mục đích phát triển khác nhau:

---

## 📁 1. Tài Liệu Màn Hình Cốt Lõi (Core Screens Specification)
- **Tập tin**: [`ba/03-product-spec/screen-specs-core.md`](file:///d:/GitHub/Luan_ai_workflow/ba/03-product-spec/screen-specs-core.md)
- **Số lượng**: 4 Màn hình cốt lõi phức tạp nhất.
- **Đối tượng sử dụng**: Nhóm phát triển MVP ưu tiên, lập trình viên FE dựng trước các luồng quan trọng nhất trong Sprint 1 & 2.
- **Danh sách màn hình**:
  1. `/custom-box`: Bộ công cụ Ghép Hộp tùy chỉnh & In tên/lời chúc lên vỏ hộp.
  2. `/checkout`: Màn hình Thanh toán, Đặt cọc 50%, Đặt lịch giao bánh tươi (Âm/Dương Lịch) & Hóa đơn VAT.
  3. `/b2b-quotation`: Form đăng ký Báo giá Sỉ Doanh Nghiệp (RFQ) & đính kèm file logo.
  4. `/admin/calendar`: Admin Dashboard Lịch Sản Xuất Song Lịch Âm/Dương & Phiếu nướng bánh ra lò.

---

## 📁 2. Tài Liệu Đầy Đủ Tất Cả Màn Hình (Full 14 Screens Specification)
- **Tập tin**: [`ba/03-product-spec/screen-specs-full.md`](file:///d:/GitHub/Luan_ai_workflow/ba/03-product-spec/screen-specs-full.md)
- **Số lượng**: 14 Màn hình (phủ 100% tất cả các URL Routes trong `sitemap.md`).
- **Đối tượng sử dụng**: Đội ngũ phát triển hoàn thiện toàn bộ sản phẩm, đảm bảo không bỏ sót bất kỳ trang nào.
- **Danh sách màn hình**:
  - **Public Portal**: `/` (Trang chủ), `/catalog` (Catalog), `/catalog/[id]` (Chi tiết bánh), `/custom-box` (Ghép hộp), `/b2b-quotation` (Báo giá B2B), `/compliance` (Hồ sơ ATTP), `/cart` (Giỏ hàng), `/checkout` (Thanh toán), `/order-tracking/[id]` (Tra cứu đơn).
  - **Admin Portal**: `/admin/dashboard` (Dashboard doanh số), `/admin/calendar` (Lịch Âm/Dương), `/admin/orders` (Quản lý đơn & cọc), `/admin/b2b-leads` (Quản lý RFQ B2B), `/admin/inventory` (Quản lý tồn kho & Hạn ngạch).
