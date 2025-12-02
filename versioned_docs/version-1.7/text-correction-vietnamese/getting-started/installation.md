---

sidebar_position: 2
title: Cài đặt thư viện và đánh giá
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

### 1.1. Sử dụng Online qua API

Để sử dụng được các chức năng sửa lỗi chính tả online, bạn cần có **ProtonX API Key**.

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

Sau khi đã cấu hình xong, khởi tạo client ProtonX bằng đoạn code mẫu dưới đây:

```python
from protonx import ProtonX

client = ProtonX(mode = "online") 

# Hoặc chỉ cần client = ProtonX() mặc định mode là "online"
```

### 1.2. Sử dụng Offline qua HuggingFace

Để sử dụng được các chức năng sửa lỗi chính tả offline, bạn cần khởi tạo client ProtonX bằng đoạn code mẫu dưới đây:

```python
from protonx import ProtonX

client = ProtonX(mode = "offline") 
```

## 2. Sử dụng mô hình sửa chính tả Tiếng Việt

Sau khi đã cấu hình và thiết lập xong client ProtonX, bạn có thể xem danh sách những mô hình đang được thư viện hỗ trợ thông qua đoạn code mẫu dưới đây:

```python
list_models = client.text.list_model()
```

Đoạn mã trên sẽ trả về danh sách các mô hình hiện đang được thư viện hỗ trợ

### Liệt kê danh sách các mô hình

```python
{
    'models': 
    {
        'online':  [ 
            'distilled-protonx-legal-tc'
            ],
        'offline': [
            'protonx-models/distilled-protonx-legal-tc',
            'protonx-models/protonx-legal-tc'
            ]
    }
}
```

Bạn có thể lựa chọn mô hình mong muốn để đánh giá chất lượng sửa chính tả Tiếng Việt bằng đoạn code mẫu dưới đây:

```python
correct_text = client.text.correct(
    input="Toi di hoc",               # Văn bản đầu vào cần sửa lỗi
    top_k=3,                           # Lấy ra 3 phương án sửa lỗi tốt nhất
    model='protonx-models/distilled-protonx-legal-tc'  # Mô hình sửa lỗi (bản distill tối ưu tốc độ)
)

#Lưu ý, cần lựa chọn mô hình theo đúng mode đã thiết lập client (online/offline)
```

Đoạn mã trên sẽ:
1. Download trực tiếp mô hình từ HuggingFace về nếu bạn thiết lập mode offline
1. Gửi yêu cầu chỉnh sửa câu **Toi di hoc** thành câu Tiếng Việt đúng.
3. Trả về kết quả sau khi chỉnh sửa.

### Kết quả trả về

```python
{
    "model": "protonx-models/distilled-protonx-legal-tc",
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

## 3. Giới hạn và liên hệ hỗ trợ

Dịch vụ sửa chính tả Tiếng Việt ProtonX có giới hạn số lượng yêu cầu mỗi ngày đối với tài khoản miễn phí.
Nếu bạn muốn **mở rộng giới hạn sử dụng**, xin vui lòng liên hệ:

* **Email:** [protonxai@gmail.com](mailto:protonxai@gmail.com)
* **Fanpage:** [https://www.facebook.com/protonxai](https://www.facebook.com/protonxai)

---
