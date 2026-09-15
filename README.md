# 🌕 Nền Tảng Bán Bánh Trung Thu Trực Tuyến (`trung_thu_web`)

Chào mừng bạn đến với dự án **Nền Tảng Bán Bánh Trung Thu Trực Tuyến**! Tài liệu này hướng dẫn tổng quan cho thành viên (Lập trình viên, Designer, AI Coding Agents, ...) khi bắt đầu tiếp cận dự án.

---

## 🎯 1. Bối Cảnh & Mục Tiêu Dự Án

* **Mô hình kiến trúc**: Sàn Trung Gian 2 Chiều (Two-Sided Marketplace).
* **Bài toán nghiệp vụ**: Giải quyết các đặc thù của thương mại điện tử bánh Trung Thu bao gồm: tính mùa vụ cao điểm, hạn sử dụng bánh tươi ngắn (7-15 ngày), rủi ro bùng đơn custom in tên riêng, và quản lý lịch nướng bánh ra lò theo ngày.

### 👤 3 Actors Chính Trong Hệ Thống
1. **🛒 Bên Mua (Buyer - B2C & B2B)**: Chọn mua bánh lẻ, tự ghép bộ hộp quà (Set 2, 4, 6), customize in tên riêng (Live Preview) & thiệp chúc, chọn ngày giao bánh tươi Dương Lịch (kèm Âm Lịch tham khảo), đặt cọc $\ge 50\%$ hoặc gửi Yêu cầu Báo Giá Sỉ (B2B RFQ).
2. **🏪 Bên Bán (Seller / Cửa Hàng / Nhà Lò)**: Quản lý sản phẩm, tồn kho 2 cấp, công tắc Bật/Tắt mùa vụ thủ công, duyệt cọc, xem Lịch sản xuất, đặt Hạn ngạch nướng bánh ngày (Capacity Cap) và gom Phiếu ra lò bánh tươi (`Daily Production Sheet`).
3. **👑 Chủ Trang Web Trung Gian (Platform Admin - Bạn)**: Quản lý danh sách Bên Bán, thu phí hoa hồng giao dịch (5-10% B2C, 3-5% B2B), tạm giữ tiền (Escrow Hold) làm trọng tài giải quyết khiếu nại và cấu hình hệ thống chung.

---

## 📂 2. Cấu Trúc Thư Mục Tài Liệu & Mã Nguồn

Dự án được tổ chức theo chuẩn đặc tả nghiệp vụ phân cấp:

```
trung_thu_web/
 ├── README.md                           ──► [Hồ sơ Onboarding cho người mới]
 ├── FEATURE_PRIORITY.md                 ──► [Danh sách Ưu tiên Phát triển Tính năng P0/P1/P2]
 ├── ideas.md                            ──► [Ý tưởng sản phẩm & Mô hình kinh doanh Sàn]
 ├── BRD/                                ──► [Thư mục Tài liệu Đặc tả Nghiệp vụ Business Requirements Document]
 │    ├── 01-overview/
 │    │    └── glossary.md               ──► [Từ điển thuật ngữ nghiệp vụ]
 │    ├── 02-business-rules/             ──► [Các bộ Quy tắc Nghiệp vụ Cốt lõi]
 │    │    ├── BR-01-b2c-ordering.md     ──► (Đơn lẻ B2C & Ghép Hộp Customizer)
 │    │    ├── BR-02-b2b-quote-request.md ──► (Yêu cầu Báo giá Sỉ B2B RFQ)
 │    │    ├── BR-03-dynamic-pricing.md  ──► (Chính sách Giá biến động & Phụ thu)
 │    │    ├── BR-04-admin-production-calendar.md ──► (Lịch Âm Dương & Capacity Cap)
 │    │    └── BR-05-operational-risks-and-policy.md ──► (Hoàn hàng, Escrow Hold & HSD)
 │    ├── 03-product-spec/               ──► [Đặc tả Sản phẩm & Màn hình]
 │    │    ├── sitemap.md                ──► [Sơ đồ trang & Ma trận Phân quyền Route]
 │    │    ├── screen-specs.md           ──► [Tổng quan đặc tả màn hình]
 │    │    ├── screen-specs-core.md      ──► [Đặc tả 4 Màn hình Cốt lõi MVP]
 │    │    └── screen-specs-full.md      ──► [Đặc tả toàn bộ màn hình]
 │    ├── 04-agent-and-dev-guidelines/   ──► [Hướng dẫn Lập trình & Schema CSDL]
 │    │    ├── system-data-dictionary.md ──► [Từ điển dữ liệu & Schema CSDL]
 │    │    └── edge-cases-and-validation.md ──► [Ma trận xử lý lỗi biên & ngoại lệ]
 │    └── 05-stitch-prompts/            ──► [Prompt thiết kế UI/UX]
 │         ├── design-style-guide.md     ──► [Hướng dẫn Phong cách Thiết kế]
 │         ├── project-tailored-style.md ──► [Phong cách thiết kế Độc bản cho Dự án]
 │         ├── stitch-prompts-core.md    ──► [Prompt Stitch Cốt lõi]
 │         ├── stitch-prompts-full.md    ──► [Prompt Stitch toàn bộ 14 màn hình]
 │         └── stitch-prompts-combined-styles.md ──► [Prompt Stitch tổng hợp]
 └── trungthuweb/                        ──► [Thư mục Mã Nguồn Thực Tế]
      ├── BE/                            ──► (Backend Codebase: Node.js Express REST API)
      └── FE/                            ──► (Frontend Codebase: React Vite + Tailwind CSS)
```

---

## 🛠️ 3. Kiến Trúc Kỹ Thuật & Giải Pháp Đơn Giản Hóa

* **Solar-First Calendar Engine**: Toàn bộ Backend, CSDL và API hoạt động **100% bằng Ngày Dương Lịch (`YYYY-MM-DD`)**. Lịch Âm chỉ hiển thị dưới dạng nhãn phụ tham khảo (`[Ngày Dương] (Tham khảo: [Ngày Âm])`).
* **Validation Tồn Kho 2 Cấp**: Kiểm tra tồn kho vỏ hộp và bánh lẻ đồng thời tại bước Checkout (bỏ WebSockets rắc rối).
* **Live Text Preview**: Dùng kỹ thuật **CSS Absolute Overlay** đè chữ in tên lên ảnh phôi vỏ hộp PNG, mượt 60fps trên mobile.
* **Thanh Toán Cọc 50%**: Tích hợp mã **VietQR / Payment Webhook Callback** để cập nhật trạng thái đơn cọc.

---

## 🚀 4. Quy Trình Bắt Đầu Cho Lập Trình Viên Mới

1. Đọc [README.md](file:///d:/GitHub/trung_thu_web/README.md) và [FEATURE_PRIORITY.md](file:///d:/GitHub/trung_thu_web/FEATURE_PRIORITY.md) để nắm rõ bức tranh tổng thể và thứ tự ưu tiên làm tính năng.
2. Đọc [BRD/02-business-rules/](file:///d:/GitHub/trung_thu_web/BRD/02-business-rules) để hiểu quy tắc nghiệp vụ trước khi viết logic.
3. Đọc [BRD/04-agent-and-dev-guidelines/system-data-dictionary.md](file:///d:/GitHub/trung_thu_web/BRD/04-agent-and-dev-guidelines/system-data-dictionary.md) trước khi tạo bảng/thêm trường trong CSDL.
4. Bắt đầu phát triển từ các tính năng thuộc nhóm **P0 (MVP Core)** trước khi làm các khối P1, P2.
