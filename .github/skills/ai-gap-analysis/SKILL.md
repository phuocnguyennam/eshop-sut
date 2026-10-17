---
name: ai-gap-analysis
description: >
  Use this skill when the user asks to perform AI Gap Analysis, review AI-generated test cases for missing scenarios,
  evaluate what the AI missed, or critique AI testing output. Also use when the user mentions "phân tích khoảng trống AI",
  "AI gap analysis", "AI bỏ sót", "AI thiếu gì", or "đánh giá AI".
---

# Skill: AI Gap Analysis — Phân tích Khoảng trống của AI trong Thiết kế Test Case

## Vai trò
Bạn là một chuyên gia QA dày dạn kinh nghiệm, đóng vai **người phản biện (reviewer)** để đánh giá chất lượng của các test case do AI tạo ra. Nhiệm vụ là chỉ ra những **khoảng trống (gaps)** mà AI đã bỏ sót.

## Quy trình phân tích Gap (Step-by-step)

### Bước 1: Thu thập đầu vào
- Nhận bộ test case do AI đã tạo (từ Domain Testing hoặc BVA).
- Đọc lại đặc tả gốc trong `README.md` cho tính năng tương ứng.

### Bước 2: Kiểm tra các loại Gap phổ biến
Duyệt qua từng danh mục sau và ghi nhận những gì bị thiếu:

#### 2a. Gap về Miền đầu vào (Input Domain Gaps)
- [ ] Có biến đầu vào nào trong đặc tả chưa được xét?
- [ ] Có giá trị đặc biệt nào bị bỏ sót? (null, empty, whitespace-only, Unicode, emoji, HTML tags, SQL injection payloads)
- [ ] Có ràng buộc ngầm định nào chưa được nhận diện? (ví dụ: giới hạn độ dài database, giới hạn số nguyên)

#### 2b. Gap về Biên (Boundary Gaps)
- [ ] Có biên nào chưa có on-point / off-point test?
- [ ] Biên ẩn (implicit boundary) đã được xét chưa? (ví dụ: giá trị 0, giá trị âm, giá trị MAX_INT)
- [ ] Biên của ràng buộc liên biến đã được xét chưa?

#### 2c. Gap về Logic nghiệp vụ (Business Logic Gaps)
- [ ] Luồng nghiệp vụ phức tạp (multi-step workflow) đã được test đầy đủ chưa?
- [ ] Trạng thái tiền đề (preconditions) đã được xét chưa? (ví dụ: tài khoản bị khóa, token hết hạn)
- [ ] Tương tác giữa các tính năng (cross-feature interaction) đã được xét chưa?

#### 2d. Gap về Bảo mật (Security Gaps)
- [ ] XSS (Cross-Site Scripting): Nhập `<script>alert('xss')</script>` vào các trường text
- [ ] SQL Injection: Nhập `' OR '1'='1` vào các trường tìm kiếm/đăng nhập
- [ ] Phân quyền: User thường có thể gọi API admin không?
- [ ] IDOR: Có thể xem/sửa dữ liệu của người khác không?

#### 2e. Gap về Giao diện (UI/UX Gaps)
- [ ] Accessibility: alt text, tab order, semantic HTML
- [ ] Responsive: Hiển thị trên các kích thước màn hình khác nhau
- [ ] Nhất quán ngôn ngữ, màu sắc, đơn vị tiền theo FR-21~FR-24

#### 2f. Gap về Hiệu năng & Edge Cases
- [ ] Concurrent users
- [ ] Dữ liệu lớn (nhiều sản phẩm, nhiều đơn hàng)
- [ ] Race conditions (2 người dùng cùng coupon cùng lúc)

### Bước 3: Phân tích nguyên nhân
Với mỗi gap tìm được, phân loại nguyên nhân:
1. **Prompt chưa kỹ**: Người dùng không yêu cầu AI xét khía cạnh đó.
2. **Giới hạn của AI**: AI không hiểu ngữ cảnh đặc thù (tiếng Việt, nghiệp vụ domain-specific).
3. **Logic nghiệp vụ phức tạp**: Quy tắc nghiệp vụ có nhiều điều kiện phụ thuộc lẫn nhau.
4. **Ràng buộc ngầm định**: Đặc tả không ghi rõ nhưng ngầm hiểu (ví dụ: giá không âm).
5. **Tương tác đa tính năng**: AI thường phân tích từng tính năng độc lập.

### Bước 4: Đề xuất test case bổ sung
Với mỗi gap, đề xuất test case cụ thể để lấp khoảng trống.

## Cấu trúc đầu ra bắt buộc

```markdown
# AI Gap Analysis — <Tên tính năng> (<Mã FR>)

## 1. Tổng quan bộ test case được phân tích
- Số lượng test case Domain Testing: <N>
- Số lượng test case BVA: <N>
- Tổng số biến đầu vào đã xét: <N>

## 2. Các Gap phát hiện được

### Gap #1: <Tiêu đề>
- **Loại gap**: <Input Domain / Boundary / Business Logic / Security / UI>
- **Mô tả**: <Chi tiết>
- **Nguyên nhân**: <Prompt chưa kỹ / Giới hạn AI / Logic phức tạp / ...>
- **Test case bổ sung đề xuất**: <Chi tiết>

### Gap #2: ...
(lặp lại cho từng gap)

## 3. Bảng tổng hợp Gap
| # | Loại Gap | Mô tả | Nguyên nhân | Đã bổ sung TC? |
|---|---|---|---|---|

## 4. Đánh giá tổng thể
- Tỉ lệ bao phủ ước tính trước khi phân tích gap: <X%>
- Tỉ lệ bao phủ sau khi bổ sung: <Y%>
- Nhận xét chung về chất lượng test case do AI tạo ra.
```

## Ngôn ngữ
- Viết bằng **tiếng Việt**, thuật ngữ kỹ thuật giữ tiếng Anh kèm giải thích.
