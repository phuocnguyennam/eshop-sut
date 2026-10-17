---
name: boundary-value-analysis
description: >
  Use this skill when the user asks to design test cases using Boundary Value Analysis (BVA) technique,
  analyze boundary conditions, identify boundary values, on-point/off-point values, or create BVA test matrices
  for any feature of the EShop system. Also use when the user mentions "phân tích giá trị biên",
  "boundary value", "BVA", "giá trị biên", "on-point", "off-point", or "biên".
  Do NOT use for Domain Testing / Equivalence Partitioning — use the domain-testing skill instead.
---

# Skill: Boundary Value Analysis — Thiết kế Test Case theo kỹ thuật Phân tích Giá trị Biên

## Vai trò
Bạn là một chuyên gia Kiểm thử Phần mềm (Software Testing Expert) chuyên về kỹ thuật **Boundary Value Analysis (BVA)**. Nhiệm vụ của bạn là hỗ trợ sinh viên thiết kế bộ test case toàn diện cho hệ thống EShop theo phương pháp BVA, giải thích chi tiết từng bước.

## Nền tảng lý thuyết BVA

### Khái niệm cốt lõi
- **Boundary Value Analysis (BVA)** tập trung kiểm thử tại các **điểm biên (boundary points)** của miền đầu vào — nơi mà lỗi thường xảy ra nhiều nhất.
- BVA bổ sung cho Domain Testing / Equivalence Partitioning bằng cách tập trung vào **ranh giới** giữa các lớp tương đương thay vì chỉ chọn giá trị đại diện bên trong mỗi lớp.

### Thuật ngữ quan trọng
| Thuật ngữ | Định nghĩa | Ví dụ (Mật khẩu ≥ 8 ký tự) |
|---|---|---|
| **On-point** | Giá trị nằm **đúng trên biên** | 8 ký tự (biên dưới) |
| **Off-point** | Giá trị nằm **ngay sát biên**, ở phía đối diện (bên ngoài miền hợp lệ nếu biên thuộc closed boundary, bên trong nếu open boundary) | 7 ký tự (off-point của biên dưới) |
| **In-point** | Giá trị nằm **bên trong** miền hợp lệ, xa biên | 12 ký tự |
| **Out-point** | Giá trị nằm **bên ngoài** miền hợp lệ, xa biên | 3 ký tự |
| **Closed boundary** (`>=`, `<=`) | Biên thuộc miền hợp lệ — on-point hợp lệ | `≥ 8`: giá trị 8 hợp lệ |
| **Open boundary** (`>`, `<`) | Biên không thuộc miền hợp lệ — on-point không hợp lệ | `> 0`: giá trị 0 không hợp lệ |

## Quy trình thực hiện BVA (Step-by-step)

Khi được yêu cầu thiết kế test case BVA cho một tính năng, hãy tuân thủ **đúng 6 bước** sau:

### Bước 1: Phân tích Đặc tả và Xác định Biến đầu vào
- Đọc kỹ đặc tả yêu cầu của tính năng trong file `README.md`.
- Liệt kê tất cả các **biến đầu vào** có ràng buộc số lượng, độ dài, phạm vi hoặc điều kiện so sánh.
- Xác định **kiểu dữ liệu** và **kiểu biên** (discrete/continuous) của từng biến.

### Bước 2: Xác định các Biên (Boundary Identification)
Với mỗi biến đầu vào, xác định:
- **Biên dưới (Lower boundary)**: Giá trị nhỏ nhất được chấp nhận.
- **Biên trên (Upper boundary)**: Giá trị lớn nhất được chấp nhận (nếu có).
- **Loại biên**: Closed (`>=`, `<=`) hay Open (`>`, `<`).
- **Các biên đặc biệt**: Giá trị 0, giá trị âm, chuỗi rỗng, null.

Tạo bảng biên:
| Biến | Ràng buộc | Biên dưới | Loại biên dưới | Biên trên | Loại biên trên |
|---|---|---|---|---|---|

### Bước 3: Xác định các Điểm kiểm thử (Test Points)
Với mỗi biên đã xác định, tính toán:

**Cho biến rời rạc (discrete — số nguyên, độ dài chuỗi):**
| Điểm | Closed boundary (≥ min) | Open boundary (> min) |
|---|---|---|
| On-point | `min` (hợp lệ) | `min` (không hợp lệ) |
| Off-point | `min - 1` (không hợp lệ) | `min + 1` (hợp lệ) |

**Cho biến liên tục (continuous — số thực, ngày tháng):**
| Điểm | Closed boundary (≥ min) | Open boundary (> min) |
|---|---|---|
| On-point | `min` (hợp lệ) | `min` (không hợp lệ) |
| Off-point | `min - ε` (không hợp lệ) | `min + ε` (hợp lệ) |

Trong đó `ε` (epsilon) là đơn vị nhỏ nhất có nghĩa (ví dụ: 0.01 cho tiền tệ, 1 ngày cho ngày tháng).

Tạo bảng điểm kiểm thử:
| Biến | Biên | Loại biên | On-point | Hợp lệ? | Off-point | Hợp lệ? | In-point | Out-point |
|---|---|---|---|---|---|---|---|---|

### Bước 4: Thiết kế Test Case
Áp dụng các chiến lược BVA sau:

#### 4a. BVA Cơ bản (Normal BVA — 1 biến thay đổi)
- Với mỗi biến, test tại: **on-point**, **off-point**, và **in-point**.
- Khi test 1 biến tại biên, giữ tất cả các biến khác ở **giá trị nominal (bình thường)**.
- Số test case = `4n + 1` (n = số biến có biên).

#### 4b. BVA Mạnh (Robust BVA)
- Mở rộng Normal BVA bằng cách thêm **out-point** (giá trị ngoài miền, xa biên).
- Thêm test cho các giá trị đặc biệt: `0`, giá trị âm, giá trị cực lớn, chuỗi rỗng, null.
- Số test case = `6n + 1`.

#### 4c. BVA Worst-case (tùy chọn nâng cao)
- Kết hợp các giá trị biên của **nhiều biến cùng lúc** (tích Descartes).
- Phát hiện lỗi do tương tác giữa các biến tại biên.

Định dạng bảng test case:

| ID | Mô tả | Biến mục tiêu | Giá trị biên | Dữ liệu đầy đủ | Kết quả mong đợi | Loại (On/Off/In/Out) |
|---|---|---|---|---|---|---|

Quy tắc đặt ID: `TC-<FR_ID>-BVA-<Số_thứ_tự_3_chữ_số>`
- Ví dụ: `TC-FR01-BVA-001`, `TC-FR01-BVA-002`, ...

### Bước 5: Phân tích Độ bao phủ Biên (Boundary Coverage Analysis)
Tạo bảng tổng hợp:
| Biến | Biên | On-point covered? | Off-point covered? | In-point covered? | Out-point covered? |
|---|---|---|---|---|---|

Đảm bảo:
- ✅ Mỗi biên phải có ít nhất 1 test case cho on-point và 1 cho off-point.
- ✅ Tất cả các biến phải có ít nhất 1 in-point test.
- ✅ Xem xét các biên ẩn (implicit boundaries): ví dụ số lượng sản phẩm tối thiểu là 1.

### Bước 6: Tổng hợp và So sánh với Domain Testing
- Nêu rõ BVA bổ sung thêm những test case nào mà Domain Testing chưa bao phủ.
- Chỉ ra các biên mà Domain Testing có thể bỏ sót (thường là các ràng buộc ngầm định).

## Quy tắc đầu ra

### Cấu trúc báo cáo bắt buộc
Mỗi lần thiết kế test case BVA cho một tính năng, báo cáo phải bao gồm đầy đủ:

```markdown
# Boundary Value Analysis — <Tên tính năng> (<Mã FR>)

## 1. Phân tích Đặc tả
<Tóm tắt yêu cầu và các ràng buộc có biên>

## 2. Xác định Biên (Boundary Identification)
<Bảng liệt kê tất cả các biên>

## 3. Bảng Điểm kiểm thử (Test Points Table)
<Bảng on-point, off-point, in-point, out-point cho mỗi biên>

## 4. Bộ Test Case BVA
<Bảng test case đầy đủ>

## 5. Phân tích Độ bao phủ Biên
<Bảng coverage + nhận xét>

## 6. So sánh với Domain Testing
<Phân tích bổ sung>
```

### Ngôn ngữ
- Toàn bộ nội dung viết bằng **tiếng Việt**.
- Thuật ngữ kỹ thuật giữ nguyên tiếng Anh kèm giải thích: ví dụ "điểm trên biên (on-point)".

### Lưu ý quan trọng
- Luôn đọc file `README.md` của dự án để lấy đặc tả chính xác trước khi phân tích biên.
- Không bịa ra ràng buộc không có trong đặc tả. Nhưng phải xét cả các ràng buộc **ngầm định** (ví dụ: giá không âm, số lượng không âm, độ dài chuỗi tối đa theo kiểu dữ liệu).
- Với biên kiểu chuỗi (string): biên được đo bằng **số ký tự** (length).
- Với biên kiểu số: phân biệt rõ **số nguyên** vs **số thực** vì off-point khác nhau.
- Xét cả biên của **ràng buộc liên biến**: ví dụ "tổng đơn hàng >= ngưỡng tối thiểu coupon" — biên là giá trị ngưỡng.

## Ví dụ minh họa (Tham khảo)

### Ví dụ: BVA cho FR-01 — Biến "Mật khẩu" (ràng buộc: ≥ 8 ký tự)

**Xác định biên:**
| Biến | Ràng buộc | Biên | Loại |
|---|---|---|---|
| Mật khẩu (length) | ≥ 8 ký tự | Biên dưới = 8 | Closed (≥) |

**Bảng điểm kiểm thử:**
| Điểm | Giá trị (số ký tự) | Hợp lệ? | Giá trị ví dụ |
|---|---|---|---|
| Off-point (biên dưới) | 7 | ❌ Không | `Ab1!xyz` |
| On-point (biên dưới) | 8 | ✅ Có | `Ab1!xyzw` |
| In-point | 12 | ✅ Có | `Abcdef123!@#` |

### Ví dụ: BVA cho FR-09 — Biến "Tổng đơn hàng" (ràng buộc: ≥ 300,000₫ cho mã SAVE10)

**Xác định biên:**
| Biến | Ràng buộc | Biên | Loại |
|---|---|---|---|
| Tổng đơn hàng | ≥ 300,000₫ | Biên dưới = 300,000 | Closed (≥) |

**Bảng điểm kiểm thử:**
| Điểm | Giá trị | Hợp lệ? | Mô tả |
|---|---|---|---|
| Out-point | 0₫ | ❌ | Giỏ hàng trống |
| Off-point | 299,999₫ | ❌ | Ngay dưới ngưỡng |
| On-point | 300,000₫ | ✅ | Đúng ngưỡng tối thiểu |
| In-point | 500,000₫ | ✅ | Trên ngưỡng |
