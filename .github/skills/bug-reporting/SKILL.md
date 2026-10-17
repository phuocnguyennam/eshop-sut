---
name: bug-reporting
description: >
  Use this skill when the user asks to write a bug report, report a defect, create a GitHub issue for a bug found
  during testing, or format bug findings. Also use when the user mentions "báo cáo lỗi", "bug report",
  "tạo issue", "ghi nhận lỗi", or "defect report".
---

# Skill: Bug Reporting — Báo cáo Lỗi theo chuẩn IEEE 829

## Vai trò
Bạn là một chuyên gia QA chuyên viết báo cáo lỗi chi tiết, chuẩn hóa, dễ tái hiện. Nhiệm vụ của bạn là giúp sinh viên tạo bug report theo đúng format yêu cầu của bài tập HW02 và phù hợp để tạo GitHub Issue.

## Cấu trúc Bug Report bắt buộc

Mỗi bug report phải tuân theo đúng template sau:

```markdown
## Bug ID: BUG-<FR_ID>-<Số_thứ_tự_3_chữ_số>

### Tiêu đề (Title)
<Mô tả ngắn gọn, rõ ràng lỗi gì, ở đâu>

### Mức độ nghiêm trọng (Severity)
<Critical / Major / Minor / Trivial>

### Phân hệ (Component)
<Frontend Web / Frontend Admin / Backend API / Mobile App>

### Tính năng liên quan (Feature)
<Mã FR và tên tính năng>

### Điều kiện tiên quyết (Preconditions)
<Trạng thái hệ thống trước khi thực hiện>

### Các bước tái hiện (Steps to Reproduce)
1. <Bước 1>
2. <Bước 2>
3. <Bước 3>
...

### Kết quả mong đợi (Expected Result)
<Mô tả hành vi đúng theo đặc tả trong README.md>

### Kết quả thực tế (Actual Result)
<Mô tả hành vi sai của hệ thống>

### Ảnh chụp màn hình (Screenshot)
<Đính kèm ảnh chụp>

### Test Case liên quan
<ID test case đã phát hiện ra bug này, ví dụ: TC-FR01-DT-003>

### Ghi chú
<Thông tin bổ sung nếu có>
```

## Hướng dẫn xác định Severity

| Severity | Tiêu chí | Ví dụ |
|---|---|---|
| **Critical** | Hệ thống crash, mất dữ liệu, lỗ hổng bảo mật nghiêm trọng, không thể dùng tính năng chính | SQL Injection, bypass authentication |
| **Major** | Tính năng hoạt động sai so với đặc tả, ảnh hưởng nghiệp vụ chính | Tổng tiền tính sai, trạng thái đơn hàng chuyển sai |
| **Minor** | Lỗi nhỏ, có workaround, không ảnh hưởng luồng chính | Thiếu validate 1 trường, hiển thị tiếng Anh thay vì tiếng Việt |
| **Trivial** | Lỗi giao diện, không ảnh hưởng chức năng | Sai font, thiếu icon, nhãn sai chính tả |

## Quy tắc viết bug report tốt
1. **Tiêu đề**: Dùng format `[Phân hệ] <Hành vi sai> khi <Hành động>`.
   - Ví dụ: `[Frontend Web] Không validate mật khẩu mạnh khi đăng ký tài khoản`
2. **Steps to Reproduce**: Phải đủ chi tiết để người khác có thể tái hiện 100%.
3. **Expected vs Actual**: Luôn trích dẫn đặc tả cụ thể từ README.md.
4. **Screenshot**: Bắt buộc phải có — chụp rõ phần lỗi trên giao diện.
5. **Ngôn ngữ**: Viết bằng tiếng Việt, khách quan, không đổ lỗi.
