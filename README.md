[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112929&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** AI20K-2A202600722
**Name:** Vương Sỹ Hạnh

---

## Mo ta

Bài lab thực hiện xây dựng một ETL pipeline đơn giản bằng Python để chuẩn hóa dữ liệu mua sắm từ nguồn JSON thô. Chúng ta đã hoàn thiện các khâu: trích xuất (Extract), kiểm chuẩn dữ liệu (Validate) loại bỏ các bản ghi lỗi giá hoặc trống danh mục, biến đổi (Transform) tính giá sau chiết khấu 10% và chuyển tên danh mục thành dạng chữ viết hoa chữ cái đầu (Title Case), và cuối cùng là lưu trữ (Load) kết quả ra file CSV. Dự án cũng thực hiện thử nghiệm chạy Agent ảo (Stress Test) để so sánh tính chính xác của Agent khi đọc dữ liệu sạch (Clean) so với dữ liệu bẩn (Garbage) có chứa các giá trị không hợp lệ.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas pytest
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Đầu tiên cần sinh dữ liệu rác:
python generate_garbage.py

# Chạy mô phỏng để so sánh phản hồi của Agent giữa dữ liệu processed_data.csv và garbage_data.csv:
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── garbage_data.csv         # Dữ liệu rác phục vụ stress test
├── agent_simulation.py      # Script chạy mô phỏng AI Agent
├── generate_garbage.py      # Script sinh dữ liệu rác
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

- Trích xuất thành công 5 bản ghi thô từ raw_data.json.
- Khâu Validation giữ lại 3 bản ghi hợp lệ và loại bỏ đi 2 bản ghi không hợp lệ (1 bản ghi giá âm, 1 bản ghi trống danh mục).
- Đầu ra processed_data.csv chứa đầy đủ các thông tin chuẩn hóa cùng cột thời gian xử lý processed_at.
- AI Agent đạt độ chính xác 10/10 với dữ liệu Clean, nhưng bị lỗi sập hệ thống (choke) khi gặp dữ liệu Garbage do xung đột kiểu dữ liệu (TypeError).
