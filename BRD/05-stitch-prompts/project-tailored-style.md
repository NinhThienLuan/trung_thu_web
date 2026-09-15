# 🎨 Phong Cách Thiết Kế Độc Bản Được AI Sinh Tự Động (Project-Tailored Dynamic Style System)

Tài liệu này là kết quả phân tích tự động từ toàn bộ hệ thống tài liệu BA (`ideas.md`, `glossary.md`, `BR-01` ➔ `BR-05`, `sitemap.md`, `screen-specs.md`). AI Agent đã tự suy luận và xây dựng một **Hệ Thống Phong Cách Thiết Kế Độc Bản (Tailored Design System)** đong đo ni đóng giày cho dự án Nền Tảng Bán Bánh Trung Thu hiện tại.

---

## 📊 1. Kết Quả Phân Tích Yếu Tố Định Hình UI (Design Drivers Analysis)

| Yếu tố Nghiệp vụ (From BA Files) | Tác động lên Thiết kế Giao diện (UI Impact) |
| :--- | :--- |
| **Bánh Tươi Thủ Công (HSD 7-15 ngày)** | Cần nhãn HSD màu sắc nổi bật (Badge HSD Tươi), tông màu nền Trắng Kem nhã nhặn tôn lên màu bánh nướng/dẻo. |
| **Custom Box & In Tên/Logo riêng** | Cần khu vực Live Preview Canvas trực quan, nổi bật dòng chữ in ép kim Vàng Gold trên phôi vỏ hộp. |
| **Báo giá B2B & Hồ sơ ATTP** | Cần phông chữ Sans-serif chỉn chu, bảng biểu dữ liệu rõ ràng, nút tải file PDF màu Vàng Gold sang trọng. |
| **Dashboard Lịch Âm/Dương Admin** | Cần chế độ giao diện Lịch Âm/Dương tối (Dark Navy `#0F172A`), phân màu rõ rệt cho đơn B2C, đợt giao B2B và ngày Full hạn ngạch. |
| **Quy định Đặt cọc 50% & VAT** | Cần Banner cảnh báo màu Amber/Gold thu hút sự chú ý tại Checkout mà không gây cảm giác khó chịu cho khách. |

---

## 🎨 2. Bảng Màu & Phông Chữ Độc Bản Cho Dự Án (Dynamic Tokens)

### 🔴 Bảng Màu (Color System - 60:30:10 Rule)
- **Primary / Dominant (60%)**: Đỏ Crimson Đêm Rằm (`#9B1C1C`) — Mang đậm bản sắc truyền thống Tết Trung Thu Việt Nam.
- **Secondary Surface (30%)**: Trắng Kem Ngà Lụa (`#FFFDF9`) cho B2C Portal & Đêm Chàm Thẫm (`#0F172A`) cho Admin Portal.
- **Accent Gold Foil (10%)**: Vàng Kim Loại Ép Kim (`#D97706` / `#D4AF37`) — Dành cho nút CTA chính (*Ghép Hộp, Thanh Toán, Đặt Cọc 50%, Tải ATTP*).
- **Status Colors**:
  - `B2C Order`: Xanh Dương (`#2563EB`)
  - `B2B Batch`: Tím Thẫm (`#7C3AED`)
  - `Pending Deposit`: Vàng Hổ Phách (`#D97706`)
  - `Deposited / Paid`: Xanh Lá (`#059669`)
  - `Capacity Full`: Đỏ Cảnh Báo (`#DC2626`)

### ✒️ Phông Chữ (Typography System)
- **Heading Display**: `Playfair Display` (Serif) — Thể hiện tính truyền thống, lịch sụ và cao cấp của hộp quà Trung Thu.
- **Body & Controls**: `Be Vietnam Pro` (Sans-serif) — Tối ưu hóa đọc chữ tiếng Việt nét mượt, rõ ràng thông số HSD và số tiền.

---

## 📝 3. Stitch Prompt Theme Snippet Độc Bản (Dán Trực Tiếp Vào Stitch)

Dưới đây là khối Stitch Prompt Theme được AI sinh tự động dựa trên dự án này. Bạn có thể copy và nhúng vào mọi Stitch Prompts:

```markdown
- DESIGN THEME & BRANDING (Project-Tailored Dynamic Style for Mooncake Platform):
  * Project Concept: Premium Fresh Mooncake E-commerce & Corporate Gift Customization Platform.
  * Color System (60:30:10 Rule):
    - Primary (60%): Deep Crimson Red (#9B1C1C) - Traditional Vietnamese Mid-Autumn heritage.
    - Secondary/Surface (30%): Silk Ivory Cream (#FFFDF9) for B2C Public Portal; Midnight Slate (#0F172A) for Admin Portal.
    - Accent Gold (10%): Metallic Gold Foil (#D97706 / #D4AF37) for primary CTA buttons (Checkout, Deposit 50%, Custom Box Builder).
  * Status Color Badges: Fresh Shelf Life Pill (#059669 Green), B2C Order (#2563EB Blue), B2B Multi-batch (#7C3AED Purple), Full Capacity Alert (#DC2626 Red).
  * Typography: Regal Serif Headings (Playfair Display) + Clean Vietnamese Sans-serif Body (Be Vietnam Pro).
  * Visual Accents: Real-time Live Canvas text overlay preview for custom box lids, dual Solar/Lunar date picker badges, 12px rounded cards with subtle drop-shadows.
```
