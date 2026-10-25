# 📚 Khóa 2: Chuyển đổi Dữ liệu thành Thông tin chi tiết (Translate Data into Insights)

Tài liệu này tổng hợp toàn bộ kiến thức trọng tâm, kỹ thuật xử lý dữ liệu và phương pháp trực quan hóa dữ liệu với **Python** (Pandas, Matplotlib) trong Khóa 2 của chứng chỉ *Google Advanced Data Analytics*.

---

## 1. Vai trò của Khám phá Dữ liệu (Exploratory Data Analysis - EDA)

Trong vòng đời dự án dữ liệu (đặc biệt ở giai đoạn **Analyze** của khung làm việc PACE), **EDA** là quy trình bắt buộc giúp nhà khoa học dữ liệu:
* Hiểu rõ cấu trúc, quy mô và đặc điểm các biến số trong tập dữ liệu.
* Phát hiện sớm dữ liệu thiếu (*missing values*), dữ liệu dị biệt (*outliers*), và lỗi định dạng kiểu dữ liệu.
* Phát hiện các mối quan hệ, quy luật tiềm ẩn và kiểm chứng các giả thuyết ban đầu trước khi xây dựng mô hình Machine Learning.
* Chuẩn bị câu chuyện dữ liệu (*data story*) để giải quyết bài toán kinh doanh cụ thể.

---

## 2. Kỹ thuật Thao tác Dữ liệu Cốt lõi với Pandas

Pandas là thư viện nền tảng cho việc thao tác dữ liệu dạng bảng (*tabular data*):

### 2.1. Đánh giá Cấu trúc Ban đầu
* `df.head(n)` / `df.tail(n)`: Xem nhanh $n$ dòng đầu tiên hoặc cuối cùng của DataFrame.
* `df.shape`: Trả về tuple `(số_dòng, số_cột)` để biết kích thước tổng thể.
* `df.size`: Tổng số ô phần tử trong bảng (`số_dòng * số_cột`).
* `df.info()`: Cung cấp tổng quan về tên cột, số lượng giá trị phi null (*non-null count*), và kiểu dữ liệu (*Dtype*) của từng cột.
* `df.describe()`: Bảng tóm tắt các chỉ số thống kê mô tả (count, mean, std, min, 25%, 50%, 75%, max) cho các biến định lượng.

### 2.2. Làm sạch & Biến đổi Dữ liệu (Data Cleaning & Transformation)
* **Xử lý chuỗi văn bản sang số:** Khi dữ liệu tiền tệ được lưu dưới dạng chuỗi (ví dụ: `"$180B"`), ta cần loại bỏ các ký tự đặc biệt và ép kiểu số:
  ```python
  df['Valuation_Billions'] = df['Valuation'].str.replace('$', '', regex=False) \
                                            .str.replace('B', '', regex=False) \
                                            .astype(float)
  ```
* **Lấy mẫu đại diện:** Dùng `df.sample(n=50, random_state=42)` khi cần thăm dò trực quan hoặc kiểm thử nhanh logic phân tích.

---

## 3. Thao tác với Dữ liệu Ngày & Giờ (Datetime Manipulation)

*(Tham khảo chi tiết từ tài liệu kỹ thuật: `Tai_Lieu/Course2/Datetime manipulation.docx`)*

Dữ liệu thời gian ban đầu thường được nạp vào dưới dạng chuỗi văn bản (`object`). Để phân tích xu hướng hoặc tính toán khoảng cách thời gian, việc chuyển đổi sang kiểu `datetime` là bắt buộc.

### 3.1. Chuyển đổi và Trích xuất Thuộc tính
* **Chuyển đổi kiểu dữ liệu:**
  ```python
  df['Date Joined'] = pd.to_datetime(df['Date Joined'])
  ```
* **Trích xuất thông qua accessor `.dt`:**
  * Năm: `df['Year Joined'] = df['Date Joined'].dt.year`
  * Tháng: `df['Month Joined'] = df['Date Joined'].dt.month`
  * Tên thứ trong tuần: `df['Day_Name'] = df['Date Joined'].dt.day_name()`

### 3.2. Bảng Tra cứu Mã Định dạng Datetime Thường Gặp (Format Codes)

| Mã Code | Định dạng | Ví dụ minh họa |
| :--- | :--- | :--- |
| `%Y` | Năm đầy đủ 4 chữ số | `2024`, `2026` |
| `%y` | Năm viết tắt 2 chữ số | `24`, `26` |
| `%m` | Tháng dạng 2 chữ số (01-12) | `01`, `12` |
| `%B` | Tên đầy đủ của tháng | `January`, `October` |
| `%b` | Tên viết tắt của tháng | `Jan`, `Oct` |
| `%d` | Ngày trong tháng (01-31) | `05`, `25` |
| `%A` | Tên đầy đủ ngày trong tuần | `Monday`, `Sunday` |
| `%a` | Tên viết tắt ngày trong tuần | `Mon`, `Sun` |
| `%H` | Giờ theo định dạng 24h (00-23) | `14`, `09` |
| `%M` | Phút (00-59) | `30`, `45` |
| `%S` | Giây (00-59) | `00`, `59` |

### 3.3. Tính toán Khoảng cách Thời gian (Time Intervals)
Tính toán thời gian từ khi thành lập đến khi đạt mốc kỳ lân:
```python
df['Years To Unicorn'] = df['Year Joined'] - df['Year Founded']
```

---

## 4. Trực quan hóa Dữ liệu EDA với Matplotlib

Biểu đồ là công cụ giao tiếp hữu hiệu nhất giữa chuyên gia dữ liệu và ban lãnh đạo:
* **Khởi tạo và cấu hình biểu đồ thanh (`plt.bar`):**
  ```python
  import matplotlib.pyplot as plt

  plt.figure(figsize=(10, 6))
  plt.bar(grouped['Industry'], grouped['Years To Unicorn'], color='royalblue')
  plt.title('Max Years to Reach Unicorn Status by Industry (Sample)', fontsize=14, fontweight='bold')
  plt.xlabel('Industry', fontsize=12)
  plt.ylabel('Years', fontsize=12)
  plt.xticks(rotation=45, horizontalalignment='right')
  plt.tight_layout()
  plt.show()
  ```
* **Nguyên tắc trình bày trực quan:**
  * Tiêu đề biểu đồ phải trực tiếp, nêu bật câu hỏi cần trả lời.
  * Luôn ghi rõ đơn vị đo lường trên các trục tọa độ (ví dụ: `Years`, `Max Valuation ($B)`).
  * Xoay nhãn trục hoành (`rotation=45`) để tránh hiện tượng chữ chồng chéo khi có nhiều danh mục ngành.

---

## 5. Dự án Thực hành: Phân tích Doanh nghiệp Kỳ lân (Unicorn Companies)

* **Tập dữ liệu:** `Unicorn_Companies.csv` gồm 1,074 doanh nghiệp kỳ lân trên toàn thế giới với 10 cột đặc trưng.
* **Mục tiêu:** Cung cấp thông tin chi tiết cho một quỹ đầu tư mạo hiểm (*Investing Firm*) để xây dựng chiến lược rót vốn.
* **Những phát hiện chính:**
  1. **Tốc độ bứt phá:** Ngành *Artificial Intelligence* và *Consumer & Retail* có thời gian đạt trạng thái kỳ lân nhanh nhất (1 - 5 năm). Trong khi đó, các ngành *Fintech* và *Health* cần thời gian tích lũy dài hơn (lên tới 21 năm ở mức tối đa trong mẫu).
  2. **Trần định giá:** *Artificial Intelligence* dẫn đầu với định giá tối đa đạt $12B, theo sau là *Fintech* đạt $10B.
  3. **Lịch sử bùng nổ:** Đa số các kỳ lân tập trung thành lập trong khoảng 2011 - 2016, phản ánh kỷ nguyên số và dòng vốn mạo hiểm bùng nổ mạnh mẽ.
