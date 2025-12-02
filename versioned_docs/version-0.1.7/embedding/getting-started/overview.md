---

sidebar_position: 1
title: Tổng quan
----------------

# ProtonX

## Giới thiệu

**ProtonX** là thư viện cung cấp các công cụ và mô hình cốt lõi giúp xây dựng chatbot có độ chính xác cao.
Thư viện này được thiết kế để dễ dàng tích hợp vào các ứng dụng AI, đặc biệt là những hệ thống cần khả năng **truy xuất thông tin** và **hiểu ngữ nghĩa sâu**.

---

## Trường hợp sử dụng

| Trường hợp sử dụng                         | Notebook                                                                                                                                                            |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Tìm kiếm vector (Vector Search)**        | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1t7Do6pj6lxUPxxwTyD_GtuNNNV6mtXLf?usp=sharing) |
| **Định tuyến ngữ nghĩa (Semantic Router)** | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1cZMAWdIhH5YcvFDR72xt3g5jHWCcWukI?usp=sharing) |

---

## Điểm mạnh nổi bật

* **Tốc độ cao**: được tối ưu cho xử lý hàng loạt, phù hợp với các ứng dụng lớn.
* **Dễ sử dụng**: API gọn nhẹ, dễ tích hợp vào các hệ thống sẵn có.
* **Dựa trên API**: chỉ cần một khóa API là có thể tạo embedding hoặc truy xuất dữ liệu dễ dàng.

---

## Cài đặt

### Yêu cầu hệ thống

* Python >= 3.8
* requests >= 2.31.0

### Cài đặt qua PyPI

```bash
pip install protonx
```

### Cài đặt qua npm

```bash
npm install protonx
```

---

ProtonX hiện hỗ trợ cả **Python** và **JavaScript**, giúp bạn dễ dàng tích hợp trong cả backend lẫn frontend chatbot.
Các phần tiếp theo sẽ hướng dẫn cách **đánh giá mô hình**, **sử dụng embeddings**, và **triển khai tìm kiếm ngữ nghĩa** với ProtonX.
