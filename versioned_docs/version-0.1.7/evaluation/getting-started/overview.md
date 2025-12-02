---

sidebar_position: 1
title: Tổng quan
----------------

# Tổng quan thư viện đánh giá

![](https://storage.googleapis.com/mle-courses-prod/users/61b6fa1ba83a7e37c8309756/private-files/b905f980-57e1-11f0-84e4-0f8a7a754383-Screenshot_2025_07_03_144533.png)

**Khung đánh giá ProtonX (ProtonX Evaluation Framework)** cung cấp một phương pháp có hệ thống để đánh giá hiệu suất của hệ thống **RAG (Retrieval-Augmented Generation)** thông qua **ba giai đoạn chính** — từ việc truy xuất tài liệu đến đánh giá câu trả lời cuối cùng của mô hình ngôn ngữ.

Mỗi giai đoạn tập trung vào một năng lực riêng của pipeline RAG, giúp đảm bảo rằng cả **độ chính xác truy xuất** và **chất lượng câu trả lời** đều được đo lường một cách khách quan.

---

## 1. Truy xuất thông tin (Retrieval)

**Mục tiêu:** Đánh giá hệ thống có truy xuất đúng và đủ các **tài liệu liên quan** chứa thông tin cần thiết để trả lời truy vấn hay không.

* Sử dụng mô hình embedding để tìm các đoạn văn tương đồng về ngữ nghĩa từ cơ sở dữ liệu vector hoặc đồ thị.
* Đánh giá các chỉ số như **Context Recall** và **Context Relevance** — đo mức độ hệ thống tìm được bằng chứng phù hợp.

---

## 2. Sắp xếp lại mức độ liên quan (Rerank)

**Mục tiêu:** Đánh giá mức độ hiệu quả của mô hình sắp xếp lại trong việc **ưu tiên các tài liệu liên quan nhất** cho mô hình ngôn ngữ.

* Mô hình xếp hạng lại các kết quả truy xuất để làm nổi bật nội dung có giá trị nhất.
* Các chỉ số có thể bao gồm **Relevance@K**, **MRR (Mean Reciprocal Rank)**, hoặc mức độ chồng lấp ngữ nghĩa giữa ngữ cảnh được sắp xếp lại và dữ liệu tham chiếu.

---

## 3. Câu trả lời của mô hình ngôn ngữ (LLM Answer)

**Mục tiêu:** Xác định xem mô hình ngôn ngữ có tạo ra **câu trả lời chính xác và đầy đủ**, dựa trên các tài liệu đã truy xuất hay không.

Hiện tại, **phiên bản này của thư viện ProtonX** mới chỉ hỗ trợ **đánh giá câu trả lời của LLM (giai đoạn 3)**.
Hai bước đầu tiên — *Truy xuất (Retrieval)* và *Sắp xếp lại (Rerank)* — sẽ được cập nhật và tích hợp trong **các phiên bản sắp tới**.
