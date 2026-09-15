# 📜 Business Rule: BR-02 - Yêu Cầu Báo Giá Đặt Hàng Số Lượng Lớn (B2B Bulk Quote Request)

## 1. Goal (Mục tiêu)
Cho phép các doanh nghiệp, tổ chức có nhu cầu mua bánh Trung Thu số lượng lớn gửi thông tin Yêu cầu báo giá (RFQ), **đăng ký lịch chia đợt giao bánh tươi** (để đảm bảo hạn sử dụng 7-15 ngày). Hệ thống ghi nhận yêu cầu và chuyển dữ liệu về cho bộ phận Sales để tiến hành tư vấn, báo giá và đàm phán thủ công.

---

## 2. Core Rules (Quy tắc nghiệp vụ cốt lõi)

### 2.1. Điều Kiện Kích Hoạt & Khung Thời Gian Mùa Vụ (Trigger Conditions & Seasonality)
- **Thời gian hoạt động**: Form RFQ chỉ mở tiếp nhận trong mùa vụ Trung Thu (từ đầu tháng 7 Âm lịch đến 10/8 Âm lịch). Ngoài khung thời gian này, hiển thị thông báo *"Hệ thống đăng ký báo giá mùa Tết Trung Thu sẽ mở vào tháng 7 Âm lịch"*.
- **Điều kiện số lượng**: Đơn hàng dự kiến có số lượng $\ge 20$ hộp (hoặc tổng giá trị dự kiến $\ge 10.000.000$ VNĐ).

### 2.2. Quy Định Dữ Liệu Form Yêu Cầu Báo Giá (RFQ Form Fields Validation)
- Các trường bắt buộc (`Required`):
  - **Tên Doanh Nghiệp / Tổ Chức**: Chuỗi văn bản ($\ge 3$ ký tự).
  - **Họ và Tên Người Liên Hệ**: Chuỗi văn bản.
  - **Số Điện Thoại**: Định dạng SĐT Việt Nam hợp lệ (10 chữ số).
  - **Email**: Định dạng email hợp lệ.
  - **Số Lượng Dự Kiến**: Số nguyên $\ge 20$.
  - **Yêu cầu Lịch Giao Bánh Tươi**:
    - [ ] Giao 1 đợt duy nhất (chọn ngày cụ thể).
    - [ ] Chia thành nhiều đợt giao (đặc thù do bánh tươi HSD ngắn 7-15 ngày, doanh nghiệp chọn các mốc ngày giao khác nhau).
- Các trường tự chọn (`Optional`):
  - **Yêu cầu in Logo / Tên công ty lên vỏ hộp**: Checkbox + đính kèm file Logo (định dạng PNG, SVG, AI, PDF).
  - **Mức Ngân Sách Dự Kiến / Hộp**: Dropdown phân khúc (Ví dụ: 300k - 500k, 500k - 1 triệu, > 1 triệu).
  - **Ghi chú thêm**: Textarea nhập yêu cầu xuất hóa đơn VAT, danh sách địa chỉ giao hàng nhiều chi nhánh...

### 2.3. Quy Trình Chuyển Tiếp & Xử Lý Dữ Liệu Sales (Lead Routing & Sales Workflow)
- **Tạo Mã RFQ**: Ngay khi người dùng nhấn "Gửi Yêu Cầu", hệ thống tự động sinh mã định danh duy nhất theo định dạng `RFQ-YYYYMMDD-XXXX` (VD: `RFQ-20260913-0042`).
- **Gửi Thông Báo Tức Thời (Real-time Notification)**:
  - Gửi email xác nhận kèm mã RFQ cho Khách hàng doanh nghiệp.
  - Gửi thông báo email + Webhook đẩy dữ liệu Lead về **Dashboard Quản Trị Sales / CRM**.
- **Quy Trình Sales Tư Vấn Thủ Công (Manual Consultation)**:
  - Trạng thái ban đầu của RFQ: `NEW` (Mới tiếp nhận).
  - Nhân viên Sales được phân công nhận Lead, liên hệ khách hàng qua Điện thoại/Zalo trong vòng **2 giờ làm việc**.
  - Sales chủ động tư vấn phương án **chia đợt giao bánh tươi ra lò**, thiết kế bản mẫu (Mockup) hộp in logo, lập bảng báo giá PDF có chiết khấu và gửi riêng cho khách hàng.
  - Trạng thái cập nhật bởi Sales: `CONTACTED` ➔ `QUOTATION_SENT` ➔ `WON` (Chốt đơn) / `LOST` (Thất bại).

---

## 3. Data Flow (Luồng dữ liệu)

```
[Đại diện Doanh nghiệp (B2B)]
    │
    ▼ Điền Form RFQ (Số lượng, Logo, Ngân sách, Đăng ký Chia Đợt Giao Bánh Tươi)
[Hệ Thống Web Portal]
    │
    ├─► Kiểm tra Khung thời gian mùa vụ (Tháng 7 Âm lịch -> 10/8 Âm lịch)
    ├─► Validates Thông tin Form
    ├─► Sinh Mã RFQ (RFQ-YYYYMMDD-XXXX)
    │
    ├───► [Email Server] ──► Gửi Email Xác Nhận cho Khách B2B
    │
    └───► [Database & CRM Sales] 
             │
             ▼ Trạng thái: NEW
      [Bộ Phận Sales] ──► Liên hệ tư vấn thủ công (Lịch bánh tươi & Báo giá PDF)
```

---

## 4. Non-goals (Phạm vi không thực hiện trong BR này)
- Hệ thống **KHÔNG tự động tính toán giá chiết khấu** để xuất hợp đồng trực tuyến tự động (nhằm đảm bảo tính linh hoạt đàm phán cho bộ phận Sales).
- Không yêu cầu khách B2B thanh toán tiền cọc ngay trên website khi gửi form RFQ.
