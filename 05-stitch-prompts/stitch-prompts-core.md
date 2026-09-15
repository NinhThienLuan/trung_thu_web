# 🎨 Bộ Stitch UI Prompts Cho 4 Màn Hình Cốt Lõi (Core Screens)

Tài liệu này chứa các Stitch Prompts chuẩn hóa được tổng hợp từ toàn bộ tài liệu BA (`BR-01` ➔ `BR-05`, `sitemap.md`, `screen-specs-core.md`, `system-data-dictionary.md`). Bạn có thể copy trực tiếp từng prompt bên dưới dán vào **Google Stitch / UI Generation Tool** để tạo giao diện/mã nguồn Frontend.

---

## 📱 1. STITCH PROMPT: Tự Ghép Hộp Quà & In Tên (`/custom-box`)

```markdown
Generate a high-converting, premium Mooncake Custom Box Builder UI component for an e-commerce web application.

- DESIGN THEME & BRANDING:
  * Application: Mooncake E-commerce Platform (Bánh Trung Thu Tươi).
  * Color Palette: Primary Deep Red (#9B1C1C), Warm Gold accents (#D97706), Elegant Dark Navy (#1E1B4B).
  * Layout: Modern, clean, fully responsive (Mobile & Desktop).

- TARGET ROUTE & USER ROLE:
  * Route: `/custom-box`
  * Persona: B2C Individual Shoppers buying personalized gift boxes.

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
  * Success: All slots filled ➔ "Thêm Vào Giỏ Hàng" button highlights in active Gold/Red styling.
  * Error: Show a red toast alert if selected flavor goes out of stock: "Vị bánh [X] tạm thời hết tồn kho".
```

---

## 🛒 2. STITCH PROMPT: Thanh Toán, Đặt Cọc & Đặt Lịch Giao (`/checkout`)

```markdown
Generate a secure, high-trust Checkout & Fresh Pre-order Delivery Scheduler UI for a Mooncake E-commerce website.

- DESIGN THEME & BRANDING:
  * Color Palette: Deep Red (#9B1C1C), Warm Gold (#D97706), Clean White background.
  * Target Route: `/checkout`

- UI COMPONENTS & LAYOUT:
  1. Customer Info Form: Inputs for Full Name, Phone Number, Shipping Address (Province, District, Ward).
  2. Pre-order Fresh Delivery Scheduler Widget:
     - Date Picker supporting Lunar Calendar dates alongside Solar dates.
     - Date Selection Restriction: Only dates within the Mid-Autumn Season (01/07 to 15/08 Lunar calendar) and minimum +3 days from current date.
     - Notice Badge: "Xưởng sẽ nướng bánh mới ra lò trước ngày giao 1 ngày".
  3. Payment & Deposit Section:
     - Customization Deposit Banner: Highlight "Bắt buộc đặt cọc 50% trước khi in vỏ hộp" if cart contains custom text items.
     - Payment Options: Bank Transfer 50% Deposit (with QR code preview), 100% Online Payment (VNPAY/Momo), COD (disabled if custom items exist).
  4. Corporate VAT Invoice Form (Collapsible Checkbox):
     - Inputs for Tax Code (MST), Company Name, Company Address, E-Invoice Email.
  5. Order Summary Card: Breakdown lines for Product Subtotal, Box Shell Fees, Shipping Fee, Early Bird Discount, Deposit Required, Total Due.

- FOUR MANDATORY UI STATES:
  * Loading: Show a spinner overlay during shipping fee calculation & coupon validation.
  * Empty: Redirect to `/catalog` with toast "Giỏ hàng trống" if accessed with empty cart.
  * Success: Order created ➔ Display Order Confirmation Card with Order ID, status "Chờ cọc 50%", and Banking QR Code.
  * Error: Show red alert if selected delivery date exceeds bakery capacity cap: "Ngày [X] xưởng đã đạt hạn ngạch tối đa. Vui lòng chọn ngày khác".
```

---

## 📋 3. STITCH PROMPT: Form Đăng Ký Báo Giá B2B (`/b2b-quotation`)

```markdown
Generate a professional B2B Corporate Bulk Quotation Request Form UI for a Mooncake brand.

- DESIGN THEME & BRANDING:
  * Target Route: `/b2b-quotation`
  * Theme: Executive, trustworthy corporate B2B feel with Deep Red & Gold accents.

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
  4. Submit Button: "Gửi Yêu Cầu Báo Giá B2B".

- FOUR MANDATORY UI STATES:
  * Loading: Show progress bar during file upload.
  * Empty: Outside season ➔ Display banner "Hệ thống Báo Giá B2B Mùa Tết Trung Thu sẽ mở vào tháng 7 Âm lịch".
  * Success: Modal popup: "Mã RFQ [Code] đã được gửi thành công. Bộ phận Sales sẽ liên hệ tư vấn trong 2 giờ".
  * Error: Inline error if logo file exceeds 10MB: "File đính kèm vượt quá 10MB. Vui lòng chọn file dung lượng nhỏ hơn".
```

---

## 📅 4. STITCH PROMPT: Admin Lịch Sản Xuất Song Lịch Âm/Dương (`/admin/calendar`)

```markdown
Generate an advanced Admin Production Schedule Dual-Calendar Dashboard UI for a Mooncake Store Owner.

- DESIGN THEME & BRANDING:
  * Target Route: `/admin/calendar`
  * Theme: Clean Admin Portal Dashboard, Dark Mode / Light Mode compatible.

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
