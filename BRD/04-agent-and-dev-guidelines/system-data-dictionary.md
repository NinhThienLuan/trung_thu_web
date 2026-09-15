# 🗄️ Từ Điển Dữ Liệu Hệ Thống (System Data Dictionary)

Tài liệu này quy định cấu trúc Schema dữ liệu, các bảng/thực thể (Entities), kiểu dữ liệu và ràng buộc kỹ thuật dành cho Backend Developer, Database Admin và AI Coding Agents.

---

## 1. Thực Thể: `products` (Sản Phẩm Bánh Lẻ & Vỏ Hộp)

| Tên Trường (Field) | Kiểu Dữ Liệu (Type) | Ràng Buộc (Constraints) | Mô Tả |
| :--- | :--- | :--- | :--- |
| `id` | `UUID` / `String` | Primary Key, Auto-gen | Định danh duy nhất sản phẩm. |
| `sku` | `String` | Unique, Not Null | Mã SKU sản phẩm (VD: `MOON-N-THAPCAM-150G`). |
| `name` | `String` | Not Null | Tên hiển thị (VD: "Bánh Nướng Thập Cẩm Gà Quay"). |
| `type` | `Enum` | `LOOSE_CAKE`, `BOX_SHELL` | Loại: Bánh lẻ hoặc Vỏ hộp quà. |
| `category` | `Enum` | `BAKED`, `SNOWSKIN`, `VEGAN`, `LOW_SUGAR` | Phân loại vị bánh. |
| `price` | `Decimal` | Not Null, $\ge 0$ | Giá bán niêm yết (VNĐ). |
| `shelf_life_days` | `Integer` | Default: 10 | Hạn sử dụng bánh tươi tính theo ngày (7-15 ngày). |
| `box_capacity` | `Integer` | Nullable (chỉ dùng cho `BOX_SHELL`) | Dung tích vỏ hộp chứa 2, 4 hoặc 6 bánh. |
| `stock_quantity` | `Integer` | Not Null, $\ge 0$ | Số lượng tồn kho hiện tại. |

---

## 2. Thực Thể: `orders` (Đơn Hàng Tổng B2C / B2B)

| Tên Trường (Field) | Kiểu Dữ Liệu (Type) | Ràng Buộc (Constraints) | Mô Tả |
| :--- | :--- | :--- | :--- |
| `id` | `UUID` / `String` | Primary Key | Mã đơn hàng (VD: `ORD-20260913-9821`). |
| `customer_name` | `String` | Not Null | Họ tên người mua. |
| `customer_phone` | `String` | Not Null | SĐT liên hệ. |
| `order_type` | `Enum` | `B2C_RETAIL`, `B2B_BULK` | Loại đơn hàng. |
| `expected_delivery_date` | `Date` | Not Null | Ngày nhận bánh tươi mong muốn (Dương Lịch). |
| `expected_lunar_date` | `String` | Computed | Ngày Âm lịch quy đổi tương ứng (VD: `"15/08"`). |
| `subtotal_amount` | `Decimal` | Not Null | Tổng tiền sản phẩm trước giảm giá & ship. |
| `shipping_fee` | `Decimal` | Default: 0 | Phí vận chuyển được tính. |
| `deposit_amount` | `Decimal` | Default: 0 | Số tiền cọc bắt buộc ( $\ge 50\%$ nếu custom). |
| `deposit_status` | `Enum` | `UNPAID`, `DEPOSITED`, `PAID_FULL` | Trạng thái cọc. |
| `status` | `Enum` | `PENDING`, `BAKING_QUEUED`, `DELIVERING`, `COMPLETED`, `CANCELLED` | Trạng thái đơn hàng. |

---

## 3. Thực Thể: `custom_boxes` (Bộ Hộp Quà Tùy Chỉnh)

| Tên Trường (Field) | Kiểu Dữ Liệu (Type) | Ràng Buộc (Constraints) | Mô Tả |
| :--- | :--- | :--- | :--- |
| `id` | `UUID` / `String` | Primary Key | Mã định danh hộp custom. |
| `order_id` | `UUID` | Foreign Key (`orders.id`) | Mã đơn hàng sở hữu. |
| `box_shell_id` | `UUID` | Foreign Key (`products.id`) | Mã vỏ hộp (Set 2, 4, 6). |
| `custom_text` | `String(50)` | Nullable | Nội dung chữ in/customize lên vỏ hộp. |
| `greeting_card_text` | `String(150)` | Nullable | Lời chúc in lên thiệp Trung Thu. |
| `selected_cake_ids` | `Array[UUID]` | Length = `box_capacity` | Danh sách ID các chiếc bánh lẻ ghép vào hộp. |

---

## 4. Thực Thể: `b2b_rfqs` (Yêu Cầu Báo Giá Doanh Nghiệp)

| Tên Trường (Field) | Kiểu Dữ Liệu (Type) | Ràng Buộc (Constraints) | Mô Tả |
| :--- | :--- | :--- | :--- |
| `id` | `UUID` / `String` | Primary Key | Mã RFQ (VD: `RFQ-20260913-0042`). |
| `company_name` | `String` | Not Null | Tên công ty/tổ chức. |
| `tax_code` | `String` | Nullable | Mã số thuế doanh nghiệp. |
| `contact_person` | `String` | Not Null | Họ tên người đại diện mua. |
| `phone` | `String` | Not Null | SĐT người liên hệ. |
| `email` | `String` | Not Null | Email nhận báo giá PDF. |
| `estimated_quantity` | `Integer` | Not Null, $\ge 20$ | Số lượng hộp dự kiến. |
| `logo_file_url` | `String` | Nullable | URL file đính kèm logo in ấn. |
| `sales_status` | `Enum` | `NEW`, `CONTACTED`, `QUOTATION_SENT`, `WON`, `LOST` | Trạng thái xử lý của Sales. |
