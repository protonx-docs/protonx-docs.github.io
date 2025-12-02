---
sidebar_position: 1
title: Tổng quan
---

# Đánh giá mô hình ngôn ngữ trả lời

Xác định xem mô hình ngôn ngữ có tạo ra câu trả lời vừa chính xác vừa đầy đủ, dựa trên các tài liệu đã được truy xuất hay không.

| Metric                | Description                                                                                          |
| :-------------------- | :--------------------------------------------------------------------------------------------------- |
| **[Độ chính xác (Precision)](./precision.md)**         | Bao nhiêu trong số các phát biểu của chatbot là chính xác.                                                    |
| **[Độ phủ (Recall)](./recall.md)**            | Bao nhiêu thông tin liên quan trong dữ liệu tham chiếu (ground truth) được chatbot đề cập đến..                                         |
| **[Điểm F1](./f1_score.md)**          | Trung bình giữa Precision và Recall, thể hiện sự cân bằng giữa độ chính xác và mức độ đầy đủ.                      |
| **[Độ bám ngữ cảnh (Groundedness)](./groundedness.md)**      | Đo lường mức độ mà câu trả lời của mô hình dựa trên ngữ cảnh được truy xuất. |
| **[Độ nhạy nhiễu (Noise Sensitivity)](./noise_sensitivity.md)** | Kiểm tra khả năng chống chịu của mô hình khi trong ngữ cảnh có thông tin nhiễu hoặc gây xao lạc.    |
