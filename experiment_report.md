# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600047
**Name:** Dương Chí Thành
**Date:** 15/4/2026

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với hai bộ dữ liệu và ghi lại phản hồi của agent:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 9 | Dữ liệu sạch, đủ thông tin, category electronics đúng. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 4 | Dữ liệu rác có giá trị outlier và mục category không hợp lệ. |

---

## 2. Phân tích & nhận xét

### Tại sao Agent trả lời sai khi dùng Garbage Data?

Bộ dữ liệu rác chứa nhiều vấn đề chất lượng và điều này ảnh hưởng trực tiếp đến kết quả agent. Cụ thể:

- Duplicate IDs: `garbage_data.csv` có hai dòng cùng `id=1`, khiến mô hình không rõ bản ghi nào là đúng khi truy vấn.
- Wrong data types: có giá trị `price` là chuỗi `"ten dollars"`, khiến bất kỳ logic tính toán nào đều khó xử lý hoặc gây lỗi nếu không kiểm tra.
- Outliers: giá trị `price=999999` cho `Nuclear Reactor` quá lớn và làm cho sản phẩm này luôn được chọn khi tìm sản phẩm điện tử.
- Missing/null values: một dòng thiếu cả `id` và `category`, điều này khiến dữ liệu không đầy đủ và tạo ra dữ liệu vô nghĩa.

Do logic agent simulation chỉ tìm sản phẩm `electronics` theo giá cao nhất, dữ liệu rác đã khiến nó chọn `Nuclear Reactor` thay vì `Laptop`. Như vậy, agent không “sai” do prompt, mà do đầu vào không đáng tin cậy.

### Tác động của dữ liệu xấu lên AI Agent

Dữ liệu xấu làm giảm độ chính xác và độ tin cậy của agent ngay cả khi prompt rõ ràng. Trong trường hợp này, agent vẫn trả lời một câu có cấu trúc hợp lệ, nhưng nội dung không phản ánh đúng mục tiêu vì dữ liệu đã bị nhiễu. Điều này cho thấy rằng một agent phụ thuộc nhiều vào chất lượng dữ liệu cơ sở để đưa ra kết quả đúng.

---

## 3. Kết luận

**Quality Data > Quality Prompt?**

Đồng ý. Chất lượng dữ liệu quan trọng hơn chất lượng prompt trong trường hợp này, vì một prompt tốt vẫn không thể cứu được khi dữ liệu đầu vào bị rác. Với dữ liệu sạch (`processed_data.csv`), agent đưa ra lựa chọn hợp lý. Với dữ liệu rác (`garbage_data.csv`), agent vẫn trả lời nhưng kết quả bị sai do outlier và dữ liệu không chuẩn.

Kết luận: Data quality là yếu tố then chốt để đảm bảo người dùng nhận được kết quả chính xác và hữu ích từ một AI agent.
