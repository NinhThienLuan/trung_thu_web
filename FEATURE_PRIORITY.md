# 📋 Danh Sách Ưu Tiên Phát Triển Tính Năng (Feature Priority Matrix)

Tài liệu này tổng hợp ma trận phân rã thứ tự ưu tiên triển khai tính năng cho hệ thống **Nền Tảng Bán Bánh Trung Thu Trực Tuyến (`trung_thu_web`)**, giúp nhóm phát triển tối ưu nguồn lực và triển khai nhanh phiên bản MVP.

---

## 🎯 1. Chiến Lược Kỹ Thuật Đơn Giản Hóa (Technical Simplification Principles)

1. **Lịch Âm Chuyển Về Dạng Hiển Thị Tham Khảo (`Solar-First Calendar`)**:
   * Hệ thống Backend, CSDL, API, Hạn ngạch xưởng (`Capacity Cap`) và Ngày giao bánh hoạt động **100% bằng Ngày Dương Lịch chuẩn (`YYYY-MM-DD`)**.
   * Lịch Âm chỉ là nhãn tham khảo hiển thị phụ trên UI: `[Ngày Dương Lịch] (Tham khảo: [Ngày Âm Lịch])`.
2. **Validation Tồn Kho 2 Cấp Tại Bước Checkout**:
   * Bỏ WebSockets/Polling phức tạp. Validate tồn kho vỏ hộp và bánh lẻ đồng thời (`Vỏ Hộp > 0` AND `Bánh Lẻ >= N`) tại thời điểm bấm Checkout.
3. **Live Text Preview Bằng CSS Absolute Overlay**:
   * Bỏ Canvas JS / WebGL nặng nề. Đè văn bản in tên lên ảnh phôi vỏ hộp PNG bằng vị trí tọa độ tuyệt đối CSS (`position: absolute`).
4. **Tích Hợp VietQR Webhook Callback Cho Luồng Cọc 50%**:
   * Bỏ hệ thống giữ chỗ Redis 15p rắc rối. Checkout sinh mã VietQR, chỉ cập nhật trạng thái cọc thành công khi nhận Webhook từ ngân hàng/cổng thanh toán.
5. **B2B Đơn Giao Nhiều Đợt Quy Về Đơn Hàng Con (`Child Orders`)**:
   * Tự động tách 1 đơn B2B giao 3 đợt thành 3 Đơn hàng con (`Order-A-1`, `Order-A-2`, `Order-A-3`), mỗi đơn con chứa 1 ngày Dương Lịch riêng.

---

## 📊 2. Ma Trận Phân Rã Thứ Tự Ưu Tiên (P0 / P1 / P2)

```
[DANH SÁCH ƯU TIÊN PHÁT TRIỂN DỰ ÁN TRUNG_THU_WEB]
  │
  ├── 🥇 KHỐI P0 (Bắt Buộc Cho MVP - Core Requirements for Launch)
  │    ├── P0.1: Catalog Bánh Lẻ & Vỏ Hộp (Set 2, 4, 6) + Tồn kho 2 cấp tại Checkout.
  │    ├── P0.2: Bộ ghép Hộp tùy chỉnh & In tên/lời chúc đơn giản (CSS Absolute Overlay Live Preview).
  │    ├── P0.3: Checkout chọn Ngày giao Dương Lịch + Đặt cọc 50% bắt buộc cho đơn custom (VietQR).
  │    ├── P0.4: Seller Dashboard quản lý Đơn hàng, Duyệt cọc & Công tắc Mùa vụ thủ công.
  │    └── P0.5: Nhãn hiển thị Lịch Âm tham khảo: `[Ngày Dương] (Tham khảo: [Ngày Âm])`.
  │
  ├── 🥈 KHỐI P1 (Nâng Cao Cho Vận Hành & B2B - Should-Have)
  │    ├── P1.1: Form đăng ký Báo Giá Sỉ B2B (RFQ) + Upload file Logo công ty (< 10MB).
  │    ├── P1.2: Hạn ngạch nướng bánh theo ngày Dương Lịch (Capacity Cap).
  │    ├── P1.3: Gom kế hoạch nướng bánh trong ngày Dương Lịch (Daily Production Sheet).
  │    └── P1.4: Form khiếu nại đổi trả 24h + Tạm giữ tiền thanh toán (Escrow Hold).
  │
  └── 🥉 KHỐI P2 (Mở Rộng & Tối Ưu Mùa Vụ - Nice-To-Have)
       ├── P2.1: Dynamic Pricing (Phụ thu cao điểm Early Bird / Rush Peak).
       ├── P2.2: B2B Đơn giao nhiều đợt tách Đơn hàng con (Child Orders).
       └── P2.3: Quảng cáo Banner & Top Listing gian hàng cho Platform Admin.
```

---

## 📝 3. Chi Tiết Các Hạng Mục Tính Năng Theo Cấp Độ

### 🥇 KHỐI P0: MVP Core (Phải có để Launch sản phẩm)

| Mã Tính Năng | Tên Tính Năng | Mô Tả Kỹ Thuật & Nghiệp Vụ | Phân Quyền |
| :--- | :--- | :--- | :--- |
| `P0.1` | Showcase Bánh & Vỏ Hộp | Hiển thị vị bánh lẻ (kèm nhãn HSD 7-10d dẻo, 10-15d nướng) và vỏ hộp Set 2, 4, 6. | Public / Buyer |
| `P0.2` | Box & Card Customizer | Ghép bánh vào slot hộp + In tên vỏ hộp (CSS Absolute Overlay) + Thiệp chúc. | Public / Buyer |
| `P0.3` | Checkout & Cọc 50% | Chọn ngày nhận Dương Lịch, cọc 50% bắt buộc cho đơn in tên (VietQR Webhook). | Public / Buyer |
| `P0.4` | Seller Orders & Store Switch | Duyệt cọc, cập nhật trạng thái đơn & Nút công tắc `[Bật/Tạm Ngừng Mùa Vụ]` thủ công. | Seller Admin |
| `P0.5` | Nhãn Lịch Âm Tham Khảo | Helper hiển thị xâu ký tự tham khảo Âm Lịch trên DatePicker / Calendar. | Public & Seller |

### 🥈 KHỐI P1: Advanced Operations & B2B (Mở rộng vận hành)

| Mã Tính Năng | Tên Tính Năng | Mô Tả Kỹ Thuật & Nghiệp Vụ | Phân Quyền |
| :--- | :--- | :--- | :--- |
| `P1.1` | Form Báo Giá B2B RFQ | Form gửi yêu cầu sỉ ($\ge 20$ hộp), đính kèm Logo công ty ($< 10\text{MB}$), tải hồ sơ ATTP. | Buyer & Seller |
| `P1.2` | Daily Capacity Cap | Cài đặt số bánh tối đa/ngày Dương Lịch (VD: 500 bánh). Tự động khóa ngày khi 100%. | Seller Admin |
| `P1.3` | Daily Production Sheet | Gom tổng chiếc bánh cần nướng theo vị trong ngày Dương Lịch để in phiếu ra lò. | Seller Admin |
| `P1.4` | Complaint 24h & Escrow | Form khiếu nại 24h (kèm Video Unboxing) + Tạm giữ tiền thanh toán làm trọng tài. | Buyer, Seller & Admin |

### 🥉 KHỐI P2: Platform Optimizations (Tối ưu & Mở rộng)

| Mã Tính Năng | Tên Tính Năng | Mô Tả Kỹ Thuật & Nghiệp Vụ | Phân Quyền |
| :--- | :--- | :--- | :--- |
| `P2.1` | Dynamic Pricing Engine | Phụ thu/Giảm giá theo mùa vụ (Early Bird -10-15%, Rush Peak +10-20%). | Engine Backend |
| `P2.2` | B2B Child Orders | Tách 1 đơn B2B giao nhiều đợt thành các đơn hàng con theo mốc ngày Dương Lịch. | Seller Admin |
| `P2.3` | Platform Promoted & Ads | Quản lý Banner trang chủ và vị trí ưu tiên `Featured Sellers` cho Platform Admin. | Platform Admin |
