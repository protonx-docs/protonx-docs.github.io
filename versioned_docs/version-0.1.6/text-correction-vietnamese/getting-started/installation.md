---

sidebar_position: 2
title: Cài đặt thư viện và sửa Tiếng Việt
-----------------------------------

---

## 1. Cài đặt thư viện

Bạn có thể cài đặt thư viện **ProtonX** trực tiếp bằng lệnh:

```bash
!pip install --upgrade protonx
```

Lệnh trên sẽ tự động tải và cài đặt phiên bản mới nhất của thư viện từ **PyPI**.
Nếu bạn đang dùng **Google Colab**, có thể chạy ngay trong ô lệnh đầu tiên của notebook.

---

## 2. Cấu hình API Key

Để sử dụng được các chức năng đánh giá, bạn cần có **ProtonX API Key**.

* Truy cập trang: [https://platform.protonx.io/login](https://platform.protonx.io/login)
* Đăng nhập và lấy khóa API cá nhân của bạn.
* Sau đó thiết lập biến môi trường trong Python như ví dụ dưới đây:

```python
import os
from google.colab import userdata

# Thiết lập khóa API ProtonX
os.environ["PROTONX_API_KEY"] = userdata.get("PROTONX_API_KEY")
```

Nếu bạn không dùng Colab, có thể thiết lập trực tiếp như sau:

```python
import os
os.environ["PROTONX_API_KEY"] = "your_api_key_here"
```

---

## 3. Đánh giá nhanh mô hình sửa chính tả Tiếng Việt

Sau khi đã cấu hình xong, bạn có thể thử đánh giá nhanh chất lượng sửa chính tả Tiếng Việt bằng đoạn code mẫu dưới đây:

```python
from protonx import ProtonX

client = ProtonX()

correct_text = client.text.correct(input = "Toi di hoc", top_k=3)
```

Đoạn mã trên sẽ:

1. Khởi tạo client ProtonX.
2. Gửi yêu cầu chỉnh sửa câu **Toi di hoc** thành câu Tiếng Việt đúng.
3. Trả về kết quả sau khi chỉnh sửa.

### Ví dụ: Kết quả trả về

```python
{
    "model": "protonx-text-correction-v1",
    "data": [
        {
            "input": "Toi di hoc",
            "candidates": [
                {
                    "output": "Tôi đi học",
                    "score": 0.5
                },
                {
                    "output": "Thôi đi học",
                    "score": 0.18
                },
                {
                    "output": "tôi đi học",
                    "score": 0.18
                }
            ]
        }
    ]
}
```
---

## 4. Giới hạn và liên hệ hỗ trợ

Dịch vụ sửa chính tả Tiếng Việt ProtonX có giới hạn số lượng yêu cầu mỗi ngày đối với tài khoản miễn phí.
Nếu bạn muốn **mở rộng giới hạn sử dụng**, xin vui lòng liên hệ:

* **Email:** [protonxai@gmail.com](mailto:protonxai@gmail.com)
* **Fanpage:** [https://www.facebook.com/protonxai](https://www.facebook.com/protonxai)

---
