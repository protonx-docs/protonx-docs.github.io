---
sidebar_position: 2
title: Độ chính xác - Precision
---

# Độ chính xác - Precision

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1K--XnYyulT54Y_vlJkEytSplcSbYpbXq?usp=sharing)

Bao nhiêu trong số các phát biểu của chatbot là chính xác.

## Giải tích độ chính xác

### Bước 1: Chia câu trả lời của mô hình ngôn ngữ thành các phát biểu chính

![](/img/precision_step_1.png)

Phân tích câu trả lời của mô hình thành các phát biểu riêng biệt (atomic statements).
Mỗi phát biểu biểu diễn một đơn vị thông tin mà mô hình đã đưa ra — ví dụ như một khẳng định, một con số, hoặc một chi tiết mô tả.

Quy trình:

- Đầu vào là Câu trả lời của LLM.

- Mô hình ngôn ngữ (Language Model) sẽ tự động phân tách câu trả lời này thành nhiều phát biểu riêng lẻ (Phát biểu 1, Phát biểu 2, Phát biểu 3, ...).

- Các phát biểu này sẽ được đem đi so sánh với dữ liệu tham chiếu (ground truth) trong bước tính Precision.

### Bước 2: Đếm số lượng phát biểu chính xác với dữ liệu tham chiếu và tính chỉ số chính xác

![](/img/precision_step_2.png)

Sau khi các phát biểu của mô hình được tách riêng ở **Bước 1**, hệ thống sẽ **so sánh từng phát biểu** với **dữ liệu tham chiếu (ground truth)** để xác định mức độ **đúng/sai** của chúng.
Mục tiêu là xác định **bao nhiêu trong số các phát biểu của mô hình là chính xác**, từ đó tính ra **Precision** — tức **tỷ lệ phát biểu đúng trên tổng số phát biểu mà mô hình đã tạo ra**.

#### Quy trình:

* Đầu vào gồm:

  * Danh sách các phát biểu của mô hình (đã được tách từ bước 1).
  * Tập dữ liệu tham chiếu (ground truths) chứa câu trả lời đúng thực tế.

* Với mỗi phát biểu:

  * Mô hình ngôn ngữ sẽ so sánh xem nội dung có khớp, tương đương, hoặc được hỗ trợ bởi thông tin trong dữ liệu tham chiếu hay không.
  * Nếu phát biểu **phù hợp hoặc được xác nhận là đúng**, nó được tính là **“chính xác” (True Positive)**.
  * Nếu phát biểu **sai lệch hoặc không có trong dữ liệu tham chiếu**, nó được xem là **“không chính xác” (False Positive)**.

* Sau khi so sánh toàn bộ:

  * Hệ thống sẽ **đếm tổng số phát biểu chính xác**.
  * Áp dụng công thức tính Precision:

#### Ví dụ minh họa:

![](/img/precision_example.png)

Trong ví dụ này, hệ thống đánh giá độ chính xác của các phát biểu mà mô hình ngôn ngữ tạo ra so với dữ liệu tham chiếu:

* **Dữ liệu tham chiếu:**
  “Điện thoại iPhone bên em kinh doanh với giá 1 triệu ạ và giảm giá 50% ạ”

* **Các phát biểu mà mô hình tạo ra:**

  1. “Điện thoại iPhone bên em còn màu hồng” ❌ *(không có trong dữ liệu tham chiếu)*
  2. “Điện thoại iPhone bên em 6GB” ❌ *(sai thông tin)*
  3. “Điện thoại iPhone bên em giá 1 triệu” ✅ *(chính xác với dữ liệu tham chiếu)*

Hệ thống xác định rằng **chỉ có 1 phát biểu trong tổng số 3 là chính xác**, vì vậy chỉ số chính xác bằng 1/3.

Chỉ số **Precision** phản ánh **tỷ lệ các phát biểu mà mô hình đưa ra là đúng đắn**, giúp đánh giá mức độ **đáng tin cậy của câu trả lời** trong việc cung cấp thông tin chính xác.

## Cách sử dụng thư viện ProtonX để đánh giá độ chính xác của câu trả lời

```python
from protonx import ProtonX

client = ProtonX()

metrics = ["precision"]
response_llms = ["Giá 1 triệu"]
ground_truths = ["Điện thoại Iphone bên em kinh doanh với giá 1 triệu ạ và giảm giá 50% ạ"]
questions = ["Điện thoại Iphone này giá bao nhiêu"]

evaluator = client.evals()
evaluator.eval_llm_answer(
    metrics=metrics,
    questions=questions,
    response_llms=response_llms,
    ground_truths=ground_truths
)
````

---

### 🔹 Giải thích chi tiết các tham số đầu vào

| Tham số           | Kiểu dữ liệu | Mô tả                                                                                                                      |
| ----------------- | ------------ | -------------------------------------------------------------------------------------------------------------------------- |
| **metrics**       | `list[str]`  | Danh sách các chỉ số cần tính. Ở đây là `["precision"]`. Có thể truyền nhiều chỉ số như `["precision", "recall", "f1"]`.   |
| **questions**     | `list[str]`  | Danh sách các câu hỏi gốc mà người dùng đã hỏi chatbot. Dùng để cung cấp ngữ cảnh cho việc đánh giá câu trả lời.           |
| **response_llms** | `list[str]`  | Danh sách câu trả lời do mô hình ngôn ngữ (LLM hoặc chatbot) sinh ra. Đây là nội dung cần được đánh giá độ chính xác.      |
| **ground_truths** | `list[str]`  | Danh sách câu trả lời đúng hoặc dữ liệu tham chiếu chuẩn (ground truth) mà chatbot nên dựa vào. Đây là cơ sở để đối chiếu. |

> ⚙️ **Nguyên tắc:** Các phần tử trong 4 danh sách này tương ứng theo chỉ mục.
> Ví dụ: `response_llms[0]` sẽ được so sánh với `ground_truths[0]` cho câu hỏi `questions[0]`.

---

### Cơ chế hoạt động bên trong

1. **Chuẩn hóa dữ liệu đầu vào:**
   Mỗi cặp `(response_llm, ground_truth)` được xử lý và chuẩn hóa ngôn ngữ — loại bỏ dấu câu, ký tự đặc biệt, từ dừng và chữ hoa/thường — giúp việc so sánh ngữ nghĩa chính xác hơn.

2. **Tách phát biểu (Atomic Segmentation):**
   Câu trả lời của mô hình (`response_llm`) được chia thành **các phát biểu nhỏ (atomic statements)** — mỗi phát biểu chứa một thông tin độc lập mà chatbot đã nói ra.
   Ví dụ:

   ```
   Response: "Giá 1 triệu và giảm 50%"
   → ["Giá 1 triệu", "Giảm 50%"]
   ```

3. **So khớp ngữ nghĩa:**
   Với từng phát biểu, hệ thống sẽ so sánh với dữ liệu tham chiếu (`ground_truth`) để xác định:

   * **Phát biểu chính xác** — khớp hoặc được xác nhận bởi dữ liệu tham chiếu → ✅ True Positive
   * **Phát biểu sai hoặc không có trong dữ liệu tham chiếu** → ❌ False Positive

4. **Tính chỉ số Precision:**
   Sau khi đánh nhãn từng phát biểu, hệ thống tính tỷ lệ phát biểu đúng trên tổng số phát biểu mà mô hình tạo ra

---

### Đầu ra của hàm

Hàm `eval_llm_answer()` trả về một **dictionary** chứa kết quả của các chỉ số được yêu cầu:

```python
{'results': [{'precision': 0.33333333333333}]}
```

**Giải thích:**

* `results` là danh sách chứa kết quả tương ứng với từng cặp `(question, response, ground_truth)`.
* Trong ví dụ trên:

  * Mô hình đưa ra **3 phát biểu**, nhưng chỉ **1 phát biểu đúng** theo dữ liệu tham chiếu →
    ( Precision = \frac{1}{3} = 0.3333 )
* Vì vậy, kết quả trả về là `{ 'precision': 0.3333 }`.

---

### Tổng kết quy trình đánh giá

| Bước | Mô tả                      | Kết quả trung gian                |
| ---- | -------------------------- | --------------------------------- |
| 1️⃣  | Chuẩn hóa dữ liệu          | “Điện thoại iPhone … giá 1 triệu” |
| 2️⃣  | Tách phát biểu từ response | ["Giá 1 triệu", "Giảm 50%"]       |
| 3️⃣  | So khớp từng phát biểu     | [True, False, False]              |
| 4️⃣  | Tính Precision = 1 / 3     | 0.3333                            |

---

### Mẹo mở rộng

Bạn có thể kết hợp nhiều chỉ số trong cùng một lệnh để đánh giá toàn diện hơn:

```python
metrics = ["precision", "recall", "f1"]
```

Khi đó kết quả có thể như sau:

```python
{'results': [{'precision': 0.33, 'recall': 0.5, 'f1': 0.4}]}
```

---

### 🔍 Ý nghĩa của Precision

* **Precision** đo lường **tỷ lệ các phát biểu mà chatbot đưa ra là đúng đắn**.
* Chỉ số này phản ánh **mức độ đáng tin cậy của câu trả lời** — chatbot càng ít nói sai, Precision càng cao.
* Precision cao → mô hình nói đúng nhiều, ít “bịa” thông tin.
* Precision thấp → mô hình nói nhiều nhưng phần lớn là thông tin sai hoặc không có trong dữ liệu chuẩn.
```
