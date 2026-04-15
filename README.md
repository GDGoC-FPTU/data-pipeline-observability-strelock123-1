[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574109&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** chithanhbachkhoa@gmail.com
**Name:** Dương Chí Thành
---

## Mô tả

Bài lab xây dựng một ETL pipeline đơn giản để:
- Extract dữ liệu từ file `raw_data.json`
- Validate và loại bỏ các bản ghi không hợp lệ
- Transform dữ liệu: chuẩn hóa category, tính giá giảm 10%, thêm timestamp
- Load kết quả ra file CSV `processed_data.csv`

Ngoài ra, bài tập cũng chú trọng quan sát (observability) bằng cách in ra số bản ghi đã giữ và đã loại.

---

## Cách chạy

### Prerequisites
```bash
pip install pandas
```

### Chạy ETL Pipeline
```bash
python solution.py
```

### Chạy Agent Simulation (Stress Test)
```bash
python agent_simulation.py
```

---

## Cấu trúc thư mục

```
├── raw_data.json            # Dữ liệu đầu vào chưa xử lý
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output của pipeline
├── experiment_report.md     # Báo cáo thí nghiệm quan sát dữ liệu
├── README.md                # File này
└── agent_simulation.py      # Script mô phỏng agent với dữ liệu sạch và rác
```

---

## Kết quả

- Script `solution.py` chạy thành công và tạo file `processed_data.csv`.
- Dữ liệu đầu vào có 5 bản ghi.
- Có 3 bản ghi hợp lệ được giữ lại.
- 2 bản ghi bị loại: 
  - id 3: `price <= 0`
  - id 4: `category` trống
- File đầu ra chứa các cột: `id`, `product`, `price`, `category`, `discounted_price`, `processed_at`.

---

## Ghi chú

- `discounted_price` được tính bằng `price * 0.9`.
- `category` được chuẩn hóa sang Title Case.
- `processed_at` là thời điểm pipeline chạy, lưu dưới dạng ISO timestamp.
