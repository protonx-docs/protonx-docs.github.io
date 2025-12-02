---
sidebar_position: 4
title: Điểm F1
---

# Điểm F1
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1ZdwpzIDw6JSkwDm62pHsmbjgC6s6TDIh?usp=sharing)


**F1-score** là thước đo tổng hợp giữa **Precision** (độ chính xác) và **Recall** (độ bao phủ).  
Chỉ số này giúp đánh giá **mức độ cân bằng** giữa việc chatbot **nói đúng** và **nói đủ** thông tin.

> Nói cách khác, F1-score trả lời cho câu hỏi:  
> *Chatbot có vừa chính xác, vừa đầy đủ khi trả lời hay không?*

---

## Công thức tính F1


Công thức chuẩn:

$$
F1 = 2 \times \frac{Precision \times Recall}{Precision + Recall}
$$

Trong đó:

- **Precision:** Tỷ lệ các phát biểu đúng trên tổng số phát biểu mà mô hình đưa ra.  
- **Recall:** Tỷ lệ các phát biểu trong dữ liệu tham chiếu được mô hình đề cập đến.

---

## Ý nghĩa của F1-score

- **Precision cao, Recall thấp:** Chatbot nói đúng nhưng thiếu thông tin.  
- **Recall cao, Precision thấp:** Chatbot nói nhiều nhưng có thể sai.  
- **F1-score cao:** Chatbot vừa nói đúng, vừa nói đủ — thể hiện sự **cân bằng tối ưu** giữa hai tiêu chí.

F1 thường được dùng như **thước đo tổng hợp** để đánh giá chất lượng trả lời của mô hình ngôn ngữ, nhất là trong các bài toán RAG (Retrieval-Augmented Generation).

---

## Ví dụ minh họa

#### Dữ liệu tham chiếu:
> "Điện thoại iPhone bên em kinh doanh với **giá 1 triệu** ạ và **giảm giá 50%** ạ."

#### Câu trả lời của chatbot:
> "Điện thoại iPhone bên em giá 1 triệu ạ."

#### Phân tích:

- **Precision:**  
  Chatbot chỉ đưa ra 1 phát biểu "Giá 1 triệu" → đúng 100%  
  → Precision = 1 / 1 = **1.0**

- **Recall:**  
  Trong dữ liệu tham chiếu có 2 phát biểu ("Giá 1 triệu", "Giảm giá 50%"), chatbot chỉ bao phủ 1.  
  → Recall = 1 / 2 = **0.5**

- **F1-score:**  
  
$$
F1 = 2 \times \frac{1.0 \times 0.5}{1.0 + 0.5} = 0.67
$$

> ✅ **Kết quả:** Chatbot đạt F1 = **0.67**, thể hiện rằng câu trả lời **chính xác nhưng chưa đầy đủ**.

---

## Cách sử dụng thư viện ProtonX để đánh giá F1-score

```python
from protonx import ProtonX

client = ProtonX()

metrics = ["f1"]
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
```

---

### Giải thích chi tiết các tham số đầu vào

| Tham số           | Kiểu dữ liệu | Mô tả                                                                                                                                |
| ----------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| **metrics**       | `list[str]`  | Danh sách các chỉ số cần tính. Ở đây là `["f1"]`. Có thể kết hợp với `["precision", "recall", "f1"]` để tính đồng thời cả ba chỉ số. |
| **questions**     | `list[str]`  | Danh sách câu hỏi gốc mà người dùng đã hỏi chatbot. Dùng để cung cấp ngữ cảnh khi đánh giá.                                          |
| **response_llms** | `list[str]`  | Danh sách câu trả lời của mô hình ngôn ngữ (LLM). Đây là nội dung cần được đánh giá.                                                 |
| **ground_truths** | `list[str]`  | Danh sách dữ liệu tham chiếu chuẩn (ground truth) chứa thông tin đúng mà chatbot cần dựa vào.                                        |

> ⚙️ **Nguyên tắc:** Các phần tử trong 4 danh sách này tương ứng theo chỉ mục.
> Ví dụ: `response_llms[0]` sẽ được so sánh với `ground_truths[0]` cho câu hỏi `questions[0]`.

---

### Cơ chế hoạt động bên trong

1. **Tính Precision và Recall nội bộ:**

   * Hàm `eval_llm_answer()` tự động gọi quy trình tính Precision và Recall dựa trên nội dung câu trả lời và dữ liệu tham chiếu.

2. **Kết hợp thành F1-score:**

   * Sau khi có hai giá trị trên, hệ thống áp dụng công thức:
   
   $$
   F1 = 2 \times \frac{Precision \times Recall}{Precision + Recall}
   $$

3. **Trả về kết quả:**

   * Kết quả cuối cùng được tổng hợp trong cấu trúc dictionary như sau:

---

### Đầu ra của hàm

```python
{'results': [{'precision': 1.0, 'recall': 0.5, 'f1': 0.67}]}
```

**Giải thích:**

* Precision = 1.0 → chatbot nói đúng tất cả những gì đã nói.
* Recall = 0.5 → chatbot bỏ sót một phần thông tin.
* F1 = 0.67 → thể hiện cân bằng giữa hai chỉ số trên.

---

## Tổng kết quy trình đánh giá F1-score

| Bước | Mô tả                                     | Kết quả trung gian                           |
| ---- | ----------------------------------------- | -------------------------------------------- |
| 1️⃣  | Chuẩn hóa dữ liệu                         | "Điện thoại iPhone … giá 1 triệu"            |
| 2️⃣  | Tách phát biểu từ response & ground truth | ["Giá 1 triệu"], ["Giá 1 triệu", "Giảm 50%"] |
| 3️⃣  | So khớp từng phát biểu                    | Precision = 1.0, Recall = 0.5                |
| 4️⃣  | Tính F1 = 2 × (1×0.5) / (1+0.5)           | 0.67                                         |

---

###  Ý nghĩa thực tiễn

* **F1-score** giúp tránh việc đánh giá thiên lệch khi chỉ nhìn vào Precision hoặc Recall.
* Nó đặc biệt hữu ích trong các hệ thống **đánh giá câu trả lời của chatbot**, **RAG**, **QA**, hoặc **tóm tắt tự động**, nơi cần cân bằng giữa **độ chính xác** và **độ đầy đủ**.

> F1 = 1.0 → Câu trả lời hoàn hảo (vừa đúng, vừa đủ).  
> F1 = 0 → Câu trả lời hoàn toàn sai hoặc không liên quan.

---

### Mẹo mở rộng

Khi cần đánh giá toàn diện mô hình, bạn nên dùng:

```python
metrics = ["precision", "recall", "f1"]
```

Kết quả trả về sẽ giúp bạn hiểu rõ mô hình:

```python
{'results': [{'precision': 0.9, 'recall': 0.8, 'f1': 0.85}]}
```

---

### Kết luận

| Chỉ số        | Ý nghĩa chính               | Câu hỏi trả lời được                      |
| ------------- | --------------------------- | ----------------------------------------- |
| **Precision** | Chatbot nói đúng bao nhiêu? | "Tỷ lệ câu nói đúng là bao nhiêu?"        |
| **Recall**    | Chatbot nói đủ bao nhiêu?   | "Bao nhiêu thông tin thật được nhắc tới?" |
| **F1-score**  | Cân bằng giữa đúng và đủ    | "Câu trả lời có vừa đúng vừa đủ không?"   |
