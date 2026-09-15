# 🎨 Bộ Stitch Prompts Phối Hợp 3 Style Thiết Kế Cho 3 Phân Hệ (Combined Multi-Style Stitch Prompts)

Tài liệu này chứa các Stitch Prompts được phối hợp phong cách thiết kế linh hoạt theo đúng đề xuất:
- **Phân hệ B2C (`/custom-box`, `/checkout`)**: Áp dụng **Style 2 (Tiệm Bánh Tươi Mộc Mạc)** — Ấm áp, mộc mạc, tôn màu bánh tươi.
- **Phân hệ B2B (`/b2b-quotation`, `/compliance`)**: Áp dụng **Style 1 (Hoàng Gia Thượng Uyển)** — Sang trọng, ép kim Vàng Gold, uy tín doanh nghiệp.
- **Phân hệ Admin (`/admin/calendar`, `/admin/dashboard`)**: Áp dụng **Style 3 (Midnight Glassmorphism)** — Giao diện tối hiện đại, tương phản nét cao cho Lịch Âm/Dương.

---

## 🛍️ PROMPT 1: Màn Hình Tự Ghép Hộp Quà & In Tên (B2C - Artisan Fresh Theme)

```markdown
Generate a high-converting, warm Artisan Fresh Mooncake Custom Box Builder UI component for an e-commerce web application.

- DESIGN THEME & BRANDING (Style 2 - Artisan Fresh Bakery):
  * Application: Mooncake E-commerce Platform (Bánh Trung Thu Tươi).
  * Aesthetic: Organic fresh mooncake bakery, clean warm artisan feel, soft cream & terracotta vibe.
  * Color Palette: Primary Baked Brick Red (#9E2A2B), Terracotta (#C86D51), Soft Cream Background (#FAF7F2), Pure White Cards (#FFFFFF with subtle shadow), Matcha Green HSD Badges (#5F7A3C).
  * Typography: Friendly Modern Sans-serif (Plus Jakarta Sans / Inter).
  * Visual Accents: 16px rounded card corners, generous whitespace, prominent Fresh Shelf Life (7-15 days) pills, warm natural photography style.

- TARGET ROUTE & USER ROLE:
  * Route: `/custom-box`
  * Persona: B2C Individual Shoppers buying personalized fresh mooncake gift boxes.

- UI COMPONENTS & LAYOUT:
  1. Box Shell Selector Tabs: Radio cards for "Set 2 Bánh", "Set 4 Bánh", "Set 6 Bánh".
  2. Interactive Box Grid Slots: Visual container showing N slots for mooncakes based on selected box set.
  3. Loose Mooncake Drawer/Grid: Product cards featuring:
     - Image, Product Name, Price.
     - Fresh Shelf Life Badge: "HSD Tươi: 7-10 ngày (Dẻo) / 10-15 ngày (Nướng)".
     - Select Button ("+ Chọn").
  4. Box Personalization Panel:
     - Text Input: "Nội dung in lên vỏ hộp" (Max 50 characters, placeholder: "Kính tặng: Tập đoàn ABC").
     - Live Canvas Preview: Real-time visual rendering of custom text overlaid on the gift box lid.
     - Greeting Card Selector: Dropdown for Mid-Autumn card design + Textarea for custom gift message (Max 150 chars).
  5. Sticky Bottom Summary Bar:
     - Displays Subtotal Price (Box Shell + Cakes).
     - Slot Progress Indicator (e.g., "Đã chọn 3/4 bánh").
     - CTA Button: "Thêm Vào Giỏ Hàng" (Disabled until all slots are filled).

- BUSINESS CONSTRAINTS & DATA VALIDATION:
  * Input Sanitization: Reject HTML/script tags in custom text input.
  * Real-time Inventory Lock: If a mooncake flavor stock reaches 0, display a grayed-out "Hết hàng" badge.

- FOUR MANDATORY UI STATES:
  * Loading: Display Skeleton shimmer loaders for the product cards and box slots.
  * Empty: Show helper prompt "Vui lòng chọn loại vỏ hộp (Set 2, 4, hoặc 6) để bắt đầu ghép bánh".
  * Success: All slots filled ➔ "Thêm Vào Giỏ Hàng" button highlights in active Terracotta/Brick Red styling.
  * Error: Show a red toast alert if selected flavor goes out of stock: "Vị bánh [X] tạm thời hết tồn kho".
```

---

## 🏛️ PROMPT 2: Màn Hình Form Báo Giá B2B Sỉ (B2B - Imperial Gold Luxury Theme)

```markdown
Generate a professional, executive B2B Corporate Bulk Quotation Request Form UI for a high-end Mooncake brand.

- DESIGN THEME & BRANDING (Style 1 - Imperial Royal Luxury):
  * Application: Corporate Mooncake Gifting Portal.
  * Aesthetic: Royal Vietnamese Mid-Autumn heritage, luxury corporate gift boxes, dark crimson & gold foil ambiance.
  * Color Palette: Primary Crimson (#8B0000), Metallic Imperial Gold (#D4AF37), Dark Obsidian Background (#181212), Cards (#2B0C0C with 1px Gold border).
  * Typography: Regal Serif Headings (Playfair Display) + Clean Sans-serif Body (Be Vietnam Pro).
  * Visual Accents: Gold foil stamping effects, traditional moonlit borders, luxury shadow drop.

- TARGET ROUTE & USER ROLE:
  * Route: `/b2b-quotation`
  * Persona: Corporate Procurement Officers & Business Buyers.

- UI COMPONENTS & LAYOUT:
  1. Header Banner: "Chương Trình Quà Tặng Doanh Nghiệp Tết Trung Thu - Chiết Khấu Đến 25%".
  2. RFQ Input Form:
     - Company Name (Required, min 3 chars).
     - Contact Person Name & Title (Required).
     - Phone Number & Email (Required).
     - Estimated Quantity (Required, number input min 20 boxes).
     - File Upload Drag-and-Drop Area: For Company Logo file (Supports PNG, SVG, AI, PDF < 10MB).
     - Delivery Schedule Option: Checkbox for "Yêu cầu chia đợt giao bánh tươi (Multi-batch delivery)".
     - Additional Notes Textarea.
  3. Food Safety & Legal Compliance Download Section:
     - Download Card Widget: Direct links/buttons to download "Giấy chứng nhận ATTP", "Bản tự công bố chất lượng", "Mẫu hợp đồng mua bán B2B".
  4. Submit Button: "Gửi Yêu Cầu Báo Giá B2B" (Gold foil metallic button).

- FOUR MANDATORY UI STATES:
  * Loading: Show progress bar during logo file upload.
  * Empty: Outside season ➔ Display banner "Hệ thống Báo Giá B2B Mùa Tết Trung Thu sẽ mở vào tháng 7 Âm lịch".
  * Success: Modal popup: "Mã RFQ [Code] đã được gửi thành công. Bộ phận Sales sẽ liên hệ tư vấn trong 2 giờ".
  * Error: Inline error if logo file exceeds 10MB: "File đính kèm vượt quá 10MB. Vui lòng chọn file dung lượng nhỏ hơn".
```

---

## 🌌 PROMPT 3: Admin Dashboard Lịch Sản Xuất (Admin - Midnight Glassmorphism Theme)

```markdown
Generate an advanced Admin Production Schedule Dual-Calendar Dashboard UI for a Mooncake Store Owner.

- DESIGN THEME & BRANDING (Style 3 - Midnight Glassmorphism & Neo-Lunar):
  * Application: Admin & Store Owner Portal.
  * Aesthetic: Neo-oriental festival night, glowing full moon visuals, dark mode glassmorphism UI.
  * Color Palette: Primary Midnight Slate (#0F172A), Amber Glow (#F59E0B), Cyan Accents (#06B6D4), Semi-transparent Glass Cards (rgba(30, 41, 59, 0.7) with 12px backdrop blur).
  * Typography: Bold Modern Display (Montserrat / Space Grotesk).
  * Visual Accents: Glowing moon backdrop, frosted glass cards, vibrant high-contrast status pills for Dual Solar/Lunar Calendar.

- TARGET ROUTE & USER ROLE:
  * Route: `/admin/calendar`
  * Persona: Store Owner, Admin & Master Baker.

- UI COMPONENTS & LAYOUT:
  1. Top Control Bar:
     - View Switcher: Toggle between "Tháng Âm Lịch (Lunar Month)" (e.g., Tháng 7 Âm, Tháng 8 Âm) and Solar Month.
     - Legend Indicators: Blue badge for B2C Orders, Purple badge for B2B Batches, Red badge for Full Capacity Days.
  2. Dual Calendar Grid:
     - Calendar Day Cells displaying BOTH Solar Date (Large number) and Lunar Date (Small label, e.g., "15/08").
     - Capacity Progress Bar per day cell (e.g., "350/500 bánh - 70%").
  3. Daily Production Sheet Drawer (Opens on clicking any calendar day):
     - Aggregated Baking Summary: Matrix of total loose mooncakes needed per flavor for that specific date (e.g., "200 Nướng Thập Cẩm", "150 Dẻo Đậu Xanh").
     - Action Buttons: "In Phiếu Ra Lò Bánh (Print Bake Ticket)" and "Khóa Ngày (Lock Date Capacity)".

- FOUR MANDATORY UI STATES:
  * Loading: Display Skeleton Grid shimmer during month switching.
  * Empty: Selected day has no orders ➔ "Không có đơn nướng bánh trong ngày này".
  * Success: Full interactive calendar grid showing color-coded order metrics & capacity progress bars.
  * Error: Server fetch failure ➔ Top red alert banner "Không thể tải dữ liệu lịch sản xuất. Vui lòng thử lại".
```
