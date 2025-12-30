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

## 2. Cách sử dụng

Khởi tạo thư viện ProtonX

```python
import os
import unittest
import torch
import torchvision
from protonx import ProtonX

client = ProtonX(
    mode="offline"
)
```

Sử dụng model

```python
prediction = client.ocr.detect_table(image_path="/content/image_has_no_table.png")
```

---
### Kết quả trả về
Chuỗi xác định là ảnh có bảng hay không

- table: Ảnh có một/nhiều bảng
- no_table: Ảnh không có bảng



## 3. Liên hệ và hỗ trợ

* **Email:** [protonxai@gmail.com](mailto:protonxai@gmail.com)
* **Discord:** [https://discord.gg/p6sWYZVkvN](mailto:https://discord.gg/p6sWYZVkvN)
* **Fanpage:** [https://www.facebook.com/protonxai](https://www.facebook.com/protonxai)

---
