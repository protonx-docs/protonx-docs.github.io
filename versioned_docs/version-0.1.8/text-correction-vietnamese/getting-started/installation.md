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

### 1.1. Cách sử dụng

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
        'offline': [
            'protonx-models/distilled-protonx-legal-tc',
            'protonx-models/nano-protonx-legal-tc',
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

## 3. Liên hệ và hỗ trợ

* **Email:** [protonxai@gmail.com](mailto:protonxai@gmail.com)
* **Discord:** [https://discord.gg/p6sWYZVkvN](mailto:https://discord.gg/p6sWYZVkvN)
* **Fanpage:** [https://www.facebook.com/protonxai](https://www.facebook.com/protonxai)

---
