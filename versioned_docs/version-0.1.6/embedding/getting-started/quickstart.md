---

id: quickstart
title: Bắt đầu nhanh
--------------------

# Bắt đầu nhanh với ProtonX

Tài liệu này hướng dẫn bạn cách thiết lập và sử dụng **ProtonX** để tạo **text embeddings** — một bước quan trọng trong việc xây dựng hệ thống tìm kiếm ngữ nghĩa hoặc chatbot thông minh.

---

## Lấy API Key

1. Truy cập [ProtonX Platform](https://platform.protonx.io/) để đăng ký tài khoản.
2. Sau khi đăng nhập, bạn có thể **tạo khóa API (API Key)** từ trang quản lý cá nhân.
3. Sao lưu và giữ khóa này cẩn thận để sử dụng trong ứng dụng của bạn.

---

## Ví dụ: Tạo Embedding bằng Python

Sử dụng thư viện **ProtonX** trong Python.

```python
from protonx import ProtonX

# Khởi tạo client ProtonX với API Key của bạn
client = ProtonX(api_key="your_api_key")

# Tạo embedding cho đoạn văn bản
text = "Tôi yêu Việt Nam"
result = client.embeddings.create(text)
```

---

## Ví dụ: Tạo Embedding bằng JavaScript

Sử dụng thư viện **ProtonX** cho JavaScript hoặc TypeScript.

```javascript
import { ProtonX } from "protonx";

const client = new ProtonX({
  apiKey: "your_api_key_here"
});

const run = async () => {
  const res = await client.embeddings.create({
    input: "Tôi yêu Việt Nam",
  });
  console.log(res);
};

run();
```

---

## Ví dụ: Kết quả trả về

Khi chạy thành công, bạn sẽ nhận được một phản hồi chứa **vector embedding** của văn bản:

```python
{
  'data': [
    {
      'index': 0,
      'embedding': [-0.0289, 0.0718, -0.0745, ...]
    }
  ],
  'usage': {
    'prompt_tokens': 4,
    'total_tokens': 4,
    'processing_time': 0.13,
    'num_texts': 1,
    'average_tokens_per_text': 4.0,
    'max_length': 4096
  }
}
```

Embedding là một mảng số thực biểu diễn ngữ nghĩa của câu — giúp mô hình có thể **so sánh độ tương đồng giữa các câu** hoặc **tìm kiếm nội dung liên quan** hiệu quả hơn.

---

## Tiếp theo

Trong các phần sau, bạn sẽ học cách:

* Sử dụng embeddings để xây dựng hệ thống tìm kiếm ngữ nghĩa.
* Kết hợp ProtonX với các công cụ RAG và chatbot.
* Đánh giá độ chính xác của mô hình bằng bộ **ProtonX Evaluation Framework**.
