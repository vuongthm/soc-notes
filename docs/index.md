# SOC / Blue Team Notes

<a href="https://vuongthm.github.io" class="back-banner">← Trang chủ chính</a>

Đây là tập hợp ghi chép của tôi về **Security Operations Center (SOC)** và Blue Team — cách phát hiện, phân tích và phản ứng trước các mối đe dọa mạng.

!!! info "Ghi chú"
    Tất cả nội dung ở đây là ghi chép học tập cá nhân. Nếu bạn tìm thấy sai sót, vui lòng [mở issue trên GitHub](https://github.com/vuongthm/soc-notes/issues).

## Chủ đề chính

<div class="grid cards" markdown>

-   🔍 **Phân tích (Analysis)**

    ---

    Quy trình triage alert, phân tích log, và nhận diện dấu hiệu tấn công (IoC).

    [:octicons-arrow-right-24: Xem ngay](analysis/index.md)

-   🛠️ **Công cụ (Tools)**

    ---

    Splunk, Elastic Stack, Wazuh và các công cụ SIEM thực tế.

    [:octicons-arrow-right-24: Xem ngay](tools/index.md)

-   📋 **Playbooks**

    ---

    Quy trình xử lý từng loại sự cố: phishing, malware, brute force...

    [:octicons-arrow-right-24: Xem ngay](playbooks/index.md)

</div>

## Tại sao học SOC?

SOC là "trái tim" của bảo mật doanh nghiệp — nơi mọi cảnh báo được xem xét, phân loại và phản ứng. Dù tôi thiên về networking, hiểu SOC giúp tôi:

- Biết **traffic bất thường** trông như thế nào từ góc nhìn security
- Kết hợp kiến thức network để **trace attack path**
- Hiểu tại sao cần **phân đoạn mạng** (segmentation) để giới hạn lateral movement
