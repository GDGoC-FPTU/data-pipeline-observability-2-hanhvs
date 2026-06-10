# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600722
**Name:** Vương Sỹ Hạnh
**Date:** 10/06/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 10 | Dữ liệu được chuẩn hóa, Agent tìm kiếm và tính toán chính xác sản phẩm đắt nhất thuộc ngành Electronics. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Agent bị nhiễu do dữ liệu chứa phần tử ngoại lai (outlier) "Nuclear Reactor" cực đoan, dẫn đến đề xuất sai mục tiêu mua sắm thông thường. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Khi chạy Agent với Garbage Data, hệ thống đã trả về kết quả sai lệch hoặc có nguy cơ bị lỗi. Cụ thể, khi truy vấn sản phẩm điện tử tốt nhất, Agent bị đầu độc bởi giá trị ngoại lai cực đoan (Extreme Outlier) "Nuclear Reactor" trị giá $999999 khiến kết quả đề xuất không thực tế. Đồng thời, sự hiện diện của dữ liệu không hợp lệ như chuỗi ký tự "ten dollars" trong cột giá (price) làm cho toàn bộ cột bị định nghĩa là kiểu đối tượng (object). Nếu truy vấn nhóm đồ nội thất (furniture), hàm so sánh `idxmax()` của Pandas sẽ bị lỗi so sánh kiểu dữ liệu (TypeError) dẫn đến crash hệ thống (choke). Ngoài ra, các lỗi trùng lặp khóa (Duplicate IDs) và bản ghi rỗng (null values) như "Ghost Item" cũng làm sai lệch nghiêm trọng cơ sở tri thức của AI Agent.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

Tôi hoàn toàn đồng ý với nhận định "Quality Data > Quality Prompt". Dù prompt có được thiết kế tối ưu hay chi tiết đến đâu, nếu dữ liệu nền tảng (knowledge base) bị ô nhiễm, sai lệch kiểu dữ liệu hoặc chứa quá nhiều giá trị rỗng, AI Agent vẫn sẽ tính toán sai lệch hoặc gặp lỗi crash hệ thống. Dữ liệu chất lượng cao là nền tảng cốt lõi cho sự chính xác của các ứng dụng AI Agent.
