# 🐼 PANDAS — NOTE DỄ NHỚ (LAB 1 & LAB 2)

> **Cách học:** Đọc yêu cầu → chọn đúng hàm → nhớ ví dụ → tránh lỗi thường gặp.
>
> **Câu thần chú:** **ĐỌC → XEM → SẠCH → ĐỔI → NHÓM → VẼ**.

## 1. 📥 ĐỌC VÀ XEM DỮ LIỆU

| Đề bài hỏi gì? | Nhớ hàm | Ý nghĩa |
|---|---|---|
| Mở file CSV | `pd.read_csv('file.csv')` | CSV → DataFrame |
| Xem 5 dòng | `df.head()` | Xem đầu bảng |
| Bao nhiêu dòng/cột? | `df.shape` | `(rows, columns)` |
| Bao nhiêu ô? | `df.size` | Dòng × cột |
| Kiểu dữ liệu? | `df.info()` | Dtype và non-null |
| Thống kê số | `df.describe()` | Mean, min, max, quartiles |

**Mẹo:** `shape` = hình dáng bảng; `size` = tổng ô; `info` = thông tin; `describe` = mô tả số liệu.

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px

df = pd.read_csv('Unicorn_Companies.csv')
print(df.shape)
df.head()
df.info()
df.describe()
```

## 2. 🕳️ MISSING DATA: TÌM → XỬ LÝ → KIỂM TRA

| Yêu cầu | Code | Nhớ nhanh |
|---|---|---|
| Đếm thiếu từng cột | `df.isna().sum()` | isna = thiếu; sum = đếm |
| Tìm hàng có ít nhất một ô thiếu | `df[df.isna().any(axis=1)]` | any theo hàng |
| Xóa hàng thiếu | `df.dropna()` | mặc định axis=0 |
| Xóa cột thiếu | `df.dropna(axis=1)` | axis=1 là cột |
| Điền từ hàng kế tiếp | `df.bfill()` | backfill = lấy bên dưới |
| Điền từ hàng trước | `df.ffill()` | forward fill = lấy bên trên |
| Điền số cố định | `df.fillna(0)` | thay NA bằng 0 |

**Câu nhớ:** `isna → any → lọc`.

```python
mask = df.isna().any(axis=1)
rows_missing = df[mask]

before = len(df)
after = len(df.dropna())
percent_lost = (before - after) / before * 100
```

⚠️ Không tự điền `City` bằng `.bfill()` nếu dòng kế tiếp là công ty ở nước khác. Điền missing phải đúng ngữ cảnh. Trong bài missing của bạn, dữ liệu thiếu theo nhóm địa lý là một dấu hiệu cần kiểm tra, không mặc định ngẫu nhiên.

## 3. 🔎 LỌC DỮ LIỆU: ĐIỀU KIỆN → MASK

| Dấu | Cách nhớ |
|---|---|
| `&` | AND = và |
| `\|` | OR = hoặc |
| `~` | NOT = phủ định |
| `.isin([...])` | Có trong danh sách |
| `==` | Bằng |
| `!=` | Khác |

```python
# Một điều kiện
df[df['Country'] == 'Singapore']

# Hai điều kiện — nhớ ngoặc cho từng điều kiện
df[(df['Year'] >= 2020) & (df['Country'] == 'Singapore')]

# Thuộc danh sách
df[df['Country'].isin(['Singapore', 'USA'])]
```

## 4. 📅 DATE: ĐỔI → TÁCH → TÍNH

**Mẹo nhớ:** Muốn lấy năm/tháng/ngày thì **chuyển sang datetime trước**.

```python
df['Date Joined'] = pd.to_datetime(df['Date Joined'])
df['Year Joined'] = df['Date Joined'].dt.year
df['Month Joined'] = df['Date Joined'].dt.month

df['Years To Unicorn'] = df['Year Joined'] - df['Year Founded']
```

| Muốn lấy | Viết |
|---|---|
| Năm | `.dt.year` |
| Tháng (số) | `.dt.month` |
| Ngày | `.dt.day` |
| Tên thứ | `.dt.day_name()` |
| Tên tháng | `.dt.month_name()` |
| Tuần ISO | `.dt.isocalendar().week` |
| Chuỗi `YYYY-MM` | `.dt.strftime('%Y-%m')` |
| Quý | `.dt.to_period('Q')` |

Trong notebook về chuỗi ngày, các cột `week`, `month`, `quarter`, `year` được tạo để thống kê số lần sét đánh theo tuần/quý/năm.

## 5. 🧹 CHUỖI VÀ KIỂU DỮ LIỆU

| Yêu cầu | Code mẫu |
|---|---|
| Xóa ký hiệu `$` | `df['Valuation'].str.replace('$', '', regex=False)` |
| Xóa `B` | `.str.replace('B', '', regex=False)` |
| Đổi sang số | `.astype(float)` |
| Xóa khoảng trắng đầu/cuối | `.str.strip()` |
| Áp dụng hàm cho từng phần tử | `.apply(func)` |

```python
df['Valuation_Billions'] = (df['Valuation']
    .str.replace('$', '', regex=False)
    .str.replace('B', '', regex=False)
    .astype(float))
```

**Nhớ:** `str.replace` = dọn chữ; `astype` = đổi kiểu. Chỉ dùng ví dụ trên khi các giá trị đúng định dạng như `$12B`.

## 6. 🧮 TỔNG HỢP: NHÓM → TÍNH → XẾP

| Hàm | Mẹo nhớ |
|---|---|
| `.groupby('col')` | Chia nhóm |
| `.sum()` | Cộng |
| `.mean()` | Trung bình |
| `.max()` | Lớn nhất |
| `.agg()` | Nhiều phép tổng hợp |
| `.sort_values(ascending=False)` | Lớn → nhỏ |
| `.reset_index()` | Đưa index thành cột |
| `.value_counts()` | Đếm số lần xuất hiện |
| `.drop_duplicates()` | Loại dòng trùng |

```python
top = (df.groupby('Industry')['Valuation_Billions']
       .sum()
       .sort_values(ascending=False)
       .head(10))
```

Ví dụ từ notebook **EDA structuring**: dùng `value_counts()` tìm vị trí xuất hiện nhiều ngày có sét; dùng `groupby()` để tính số lần sét đánh theo thứ và theo tháng; dùng `pd.concat()` để nối dữ liệu 2016–2017 với 2018; dùng `merge()` để ghép bảng tổng theo tháng và năm.

## 7. 📊 TRỰC QUAN HÓA: CHỌN ĐÚNG BIỂU ĐỒ

| Mục đích | Hàm |
|---|---|
| Vẽ cột cơ bản | `plt.bar(x, y)` |
| So sánh nhóm bằng cột | `sns.barplot(data=df, x='Industry', y='Value')` |
| Xem phân bố/outlier | `sns.boxplot(data=df, y='Value')` |
| Bản đồ vị trí | `px.scatter_geo(df, lat='latitude', lon='longitude')` |
| Biểu đồ heatmap | `sns.heatmap(matrix)` |

```python
plt.figure(figsize=(10, 5))
sns.barplot(data=summary, x='Industry', y='Total')
plt.title('Total by industry')
plt.xticks(rotation=45)
plt.show()
```

**Nhớ:** `figure` = khổ giấy; `barplot` = vẽ; `title` = tiêu đề; `xticks` = chỉnh trục X; `show` = hiển thị.

## 8. 🧠 THÊM TỪ CÁC NOTEBOOK: DỄ RA CÂU HỎI

| Kiến thức | Nhớ ngắn |
|---|---|
| `.sample(n=50, random_state=42)` | Lấy ngẫu nhiên 50 dòng, có thể lặp lại |
| `pd.concat([df1, df2], ignore_index=True)` | Ghép dữ liệu theo chiều dòng |
| `.merge(other, on='year')` | Nối bảng theo khóa chung |
| `df['col'].value_counts()` | Đếm tần suất giá trị |
| `df.duplicated().sum()` | Đếm dòng trùng (sau dòng xuất hiện đầu tiên) |
| `.drop_duplicates()` | Xóa trùng |
| `.dt.strftime('%Y')` | Định dạng ngày thành chuỗi năm |
| `pd.qcut(series, 4)` | Chia thành 4 nhóm theo phân vị |
| `.cat.codes` | Mã hóa category thành số |
| `pd.get_dummies(...)` | Mã hóa thành các cột chỉ báo |
| `.pivot(index=..., columns=..., values=...)` | Đổi bảng để vẽ heatmap |

## 9. ⚠️ BỐN CẶP RẤT DỄ NHẦM

1. `shape` trả `(hàng, cột)`; `size` trả **số ô**.
2. `axis=0` là xử lý theo **hàng** trong `dropna`; `axis=1` là **cột**. Với `any(axis=1)`, phép gộp chạy **ngang qua các cột** để trả kết quả cho từng hàng.
3. `sum()` = tổng; `value_counts()` = đếm tần suất; `count()` = đếm phần tử không NA.
4. `.dt.year` cho giá trị năm; `.dt.strftime('%Y')` cho **chuỗi ký tự** năm.

## 10. ✅ TỰ KIỂM TRA (CHE ĐÁP ÁN)

1. Muốn biết dữ liệu có bao nhiêu hàng, cột? → `df.shape`
2. Muốn đếm missing từng cột? → `df.isna().sum()`
3. Muốn lấy các hàng có ít nhất một missing? → `df[df.isna().any(axis=1)]`
4. Muốn xóa cột có missing? → `df.dropna(axis=1)`
5. Muốn lấy năm từ cột ngày? → `pd.to_datetime(...)` rồi `.dt.year`
6. Muốn tổng doanh thu theo ngành? → `groupby('Industry')['Revenue'].sum()`
7. Muốn sắp xếp giảm dần? → `.sort_values(ascending=False)`
8. Muốn dữ liệu mẫu lặp lại được? → `.sample(..., random_state=42)`
9. Muốn bỏ hàng trùng? → `.drop_duplicates()`
10. Muốn vẽ bản đồ theo kinh/vĩ độ? → `px.scatter_geo(...)`

---

### 🎯 Câu chốt trước khi thi

**XEM:** `head, shape, size, info, describe`  
**THIẾU:** `isna, any, dropna, fillna/bfill`  
**LỌC:** `&, |, ~, isin`  
**ĐỔI:** `to_datetime, dt, str.replace, astype`  
**NHÓM:** `groupby, sum, mean, agg, sort_values`  
**VẼ:** `bar, barplot, boxplot, scatter_geo`.
