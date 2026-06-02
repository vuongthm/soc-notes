# Quy trình triage alert

**Tags:** `#soc` `#triage` `#alert`

## Triage là gì?

Triage (phân loại) là bước đầu tiên khi nhận một alert từ SIEM — quyết định xem đây là **true positive**, **false positive**, hay cần điều tra thêm.

## Quy trình 5 bước

### 1. Đọc alert và hiểu context

```
Alert: Possible brute force login
Source IP: 192.168.10.55
Target: FILESERVER-01
Attempts: 47 in 2 minutes
```

Câu hỏi đặt ra ngay:

- IP này là ai? (nội bộ hay bên ngoài?)
- Giờ này có bình thường không? (giờ làm việc hay 3 giờ sáng?)
- Tài khoản nào bị target?

### 2. Tra cứu IP và tài khoản

=== "Splunk"

    ```spl
    index=main sourcetype=WinEventLog:Security
    EventCode=4625 src_ip="192.168.10.55"
    | stats count by user, dest, src_ip
    | sort -count
    ```

=== "Elastic (KQL)"

    ```
    event.code: "4625" AND source.ip: "192.168.10.55"
    ```

### 3. Phân loại mức độ

| Mức | Tiêu chí | Hành động |
|-----|----------|-----------|
| **Critical** | Tài khoản admin, giờ lạ, IP nước ngoài | Cô lập ngay |
| **High** | User thường, nhiều attempt | Điều tra, hỏi user |
| **Medium** | Vài attempt, giờ làm việc | Theo dõi thêm |
| **Low** | 1-2 attempt, user tự nhập sai | Ghi nhận, close |

### 4. Kiểm tra lateral movement

Nếu có attempt thành công, kiểm tra xem account đó có đăng nhập đi đâu không:

```spl
index=main sourcetype=WinEventLog:Security
EventCode=4624 user="john.doe"
| table _time, src_ip, dest, LogonType
| sort _time
```

### 5. Quyết định và ghi chép

!!! tip "Luôn ghi lại quyết định"
    Dù là false positive hay true positive, ghi lại **lý do** quyết định. Điều này giúp cải thiện rule sau này.

## False Positive phổ biến

- **IT scan nội bộ**: Nessus/OpenVAS chạy scheduled scan → tạo ra nhiều "brute force" alert
- **Password reset sau kỳ nghỉ**: User nhập sai password cũ nhiều lần
- **Service account misconfigured**: Chạy với credential cũ sau khi đổi password
