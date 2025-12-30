---

sidebar_position: 1
title: Tổng quan
----------------

---

**Mục tiêu:** Phát hiện bảng trong ảnh

**Cách ứng dụng:**

Bạn có thể xây dựng giải pháp OCR có độ chính xác cao và tiết kiệm chi phí thông qua dùng model này.

Những model Open Source OCR mặc dù đã tốt hơn trước nhiều nhưng vẫn có những điểm hạn chế khi gặp văn bản dài + bảng biểu phức tạp tuy nhiên các mô hình giờ đã rất tốt trên các văn bản không bảng hoặc bảng đơn giản.
Gemini OCR có độ chính xác tốt hơn các Open Source trên những văn bản có bảng biểu phức tạp.

Dưới đây là một luồng đề xuất cho bạn:
- Văn bản được tách thành các ảnh
- Lặp qua các ảnh, anh đưa qua model phân loại bảng dùng thư viện ProtonX, nếu chứa bảng thì chuyển cho Gemini OCR, nếu không chứa bảng thì chuyển cho Deep Seek
- Kết quả được tổng hợp lại thành file docx, excels, markdown, vv

![](https://storage.googleapis.com/mle-courses-prod/users/61b6fa1ba83a7e37c8309756/private-files/ac4488e0-e537-11f0-869a-d35990beaaa0-Screenshot_2025-12-26_084841.png)


[Video giải thích và tính toán chi phí chi tiết](https://www.facebook.com/reel/26362489256674612)

---


