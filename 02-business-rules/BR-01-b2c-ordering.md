# 📜 Business Rule: BR-01 - Đặt Hàng Cá Nhân & Tùy Chỉnh Hộp Quà (B2C Custom Box Ordering)

## 1. Goal (Mục tiêu)
Cho phép khách hàng cá nhân (B2C) dễ dàng lựa chọn giữa việc mua chiếc bánh lẻ hoặc tự cấu hình bộ hộp quà Trung Thu (loại 2, 4, 6 bánh), điền thông tin in ấn/tùy chỉnh tên tổ chức/lời chúc lên vỏ hộp, **lựa chọn ngày nhận bánh tươi ra lò** và thực hiện đặt hàng trực tuyến.

---

## 2. Core Rules (Quy tắc nghiệp vụ cốt lõi)

### 2.1. Quy tắc Mua Bánh Lẻ & Hạn Sử Dụng Bánh Tươi (Loose Mooncake & Fresh Shelf Life Rule)
- Khách hàng có thể thêm trực tiếp từng chiếc bánh lẻ vào giỏ hàng mà không bắt buộc phải chọn vỏ hộp.
- **Hiển thị Hạn Sử Dụng (Shelf Life Display)**:
  - Mọi sản phẩm bánh lẻ trên giao diện phải hiển thị rõ ràng nhãn Hạn sử dụng bánh tươi:
    - Bánh dẻo tươi: **7 - 10 ngày** kể từ ngày sản xuất.
    - Bánh nướng tươi: **10 - 15 ngày** kể từ ngày sản xuất.
  - Hiển thị cảnh báo bảo quản (VD: *"Bánh tươi không chất bảo quản, khuyên dùng ngay sau khi mở bao bì"*).

### 2.2. Quy tắc Tùy Chỉnh Hộp Quà (Custom Box Rule)
- **Chọn Vỏ Hộp**: Khách hàng chọn 1 trong các dung tích vỏ hộp cố định:
  - `BOX-2`: Hộp chứa đúng 2 chiếc bánh.
  - `BOX-4`: Hộp chứa đúng 4 chiếc bánh.
  - `BOX-6`: Hộp chứa đúng 6 chiếc bánh.
- **Ghép Bánh Vào Hộp**:
  - Khách hàng phải chọn đủ số lượng bánh tương ứng với dung tích vỏ hộp (VD: `BOX-4` phải chọn đúng 4 chiếc bánh) mới được phép kích hoạt nút **"Hoàn thành Hộp Quà"** hoặc **"Thêm vào giỏ hàng"**.
  - Cho phép chọn trùng vị bánh (VD: 4 chiếc Bánh Nướng Thập Cẩm trong 1 hộp 4).
- **Tính Giá Hộp Quà**:
  $$\text{Tổng giá Hộp Quà} = \text{Giá Vỏ Hộp} + \sum (\text{Giá các chiếc bánh lẻ được chọn}) + \text{Phí Customize (nếu có)}$$

### 2.3. Quy tắc In Tên Tổ Chức / Cá Nhân Lên Vỏ Hộp (Box Personalization & Live Preview)
- Tại bước xem trước hộp quà (Box Preview), hệ thống cung cấp ô nhập liệu **"Nội dung in lên vỏ hộp"**:
  - Giới hạn độ dài: Tối đa 50 ký tự.
  - Định dạng nhập: Tên tổ chức/công ty, tên cá nhân hoặc câu chúc (VD: *"Công ty Công nghệ ABC kính tặng"*).
  - **Kỹ thuật Xem trước (CSS Absolute Overlay Live Preview)**: Hiển thị dòng chữ in đè trực tiếp lên ảnh phôi vỏ hộp PNG bằng vị trí tọa độ tuyệt đối CSS (`position: absolute`). Không sử dụng thư viện đồ họa Canvas/WebGL nặng nề, đảm bảo mượt mà 60fps trên thiết bị di động.
- Trường thông tin in ấn là **Không bắt buộc** (nếu để trống, hộp sẽ giữ thiết kế vỏ hộp nguyên bản).
- **Validation Tồn kho 2 Cấp Tại Bước Checkout**: Hệ thống validate tồn kho 2 cấp (`Vỏ Hộp > 0` AND `Bánh Lẻ >= N`) tại thời điểm bấm Checkout thay vì dùng WebSockets đẩy realtime phức tạp.

### 2.4. Quy tắc Chọn Ngày Giao Bánh Tươi (Fresh Pre-order Scheduling Rule)
- Do bánh tươi có HSD ngắn (7-15 ngày), tại bước Checkout, hệ thống bắt buộc người dùng chọn **"Ngày nhận bánh mong muốn"** (`Expected Delivery Date`):
  - **Điều kiện hợp lệ**: Ngày nhận bánh phải nằm trong Mùa vụ Trung Thu (từ 01/07 Âm lịch đến 15/08 Âm lịch) và cách ngày đặt hàng hiện tại tối thiểu **3 ngày** (để xưởng lên lịch nướng bánh tươi ra lò).
  - Hệ thống tính toán và hiển thị dự kiến: **Ngày xưởng ra lò bánh** = `Expected Delivery Date` - `1 ngày shipping`.

---

## 3. Data Flow (Luồng dữ liệu)

```
[Khách Hàng B2C] 
    │
    ├─► Xem HSD Bánh Tươi (7-10 ngày dẻo / 10-15 ngày nướng)
    ├─► Chọn Vỏ Hộp (Set 2 / 4 / 6) & Ghép bánh lẻ
    ├─► Nhập Văn Bản In Tên Tổ Chức / Logo (Optional)
    │
    ▼
[Bộ Kiểm Tra Đủ Số Lượng Bánh] ──(Nếu thiếu)──► Hiển thị cảnh báo "Cần chọn thêm X bánh"
    │
    │ (Nếu hợp lệ)
    ▼
[Trang Checkout & Đặt Lịch Giao Bánh Tươi]
    │
    ├─► Chọn Ngày Nhận Bánh (Min: Hiện tại + 3 ngày)
    │
    ▼
[Lưu Đơn Hàng (Order & Production Schedule)]
    ├─► Đặt cọc/Thanh toán đơn hàng
    └─► Đẩy lịch nướng bánh mới vào Production Queue theo ngày giao
```

---

## 4. Non-goals (Phạm vi không thực hiện trong BR này)
- Không giao bánh tươi ngay trong ngày (Same-day delivery) do bánh cần thời gian sản xuất thủ công theo đợt ra lò.
- Không áp dụng chính sách chiết khấu sỉ cho đơn hàng B2C dưới 10 hộp.
