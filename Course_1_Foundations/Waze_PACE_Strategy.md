# 🚗 Waze Project: PACE Strategy Document

**Dự án:** Dự đoán tỷ lệ người dùng rời bỏ ứng dụng (User Churn Prediction)
**Khách hàng:** Ban lãnh đạo Waze
**Vai trò:** Data Analyst / Data Scientist

---

## 1. Plan (Lên kế hoạch)
**Mục tiêu kinh doanh:** 
Phát triển một mô hình Machine Learning dự đoán tỷ lệ người dùng rời bỏ ứng dụng (churn) hàng tháng. Mô hình chính xác sẽ giúp Waze ngăn chặn việc mất người dùng, cải thiện tỷ lệ giữ chân (retention) và phát triển kinh doanh.

**Các bên liên quan (Stakeholders):**
* Lãnh đạo Waze (Khách hàng nội bộ)
* Đội ngũ Waze Data Team (Quản lý dự án, Data Engineer, Data Scientist)

**Câu hỏi khởi động:**
1. Ai là những người dùng thường xuyên xóa ứng dụng nhất?
2. Dữ liệu hiện tại có đủ các biến số (features) để mô tả hành vi lái xe của người dùng không?
3. Cột mốc thời gian nào được định nghĩa là "churn" (ví dụ: không dùng app trong 30 ngày)?

## 2. Analyze (Phân tích)
**Mục tiêu giai đoạn này:** Khám phá, làm sạch và tổ chức dữ liệu TLC.
* **Nhiệm vụ:** Nhập (import) dữ liệu vào Python, tạo Dataframe, kiểm tra các kiểu dữ liệu, xử lý giá trị bị thiếu (missing values) và các điểm bất thường (outliers).
* **Đầu ra:** Các thống kê mô tả (Descriptive statistics) và biểu đồ khám phá dữ liệu (EDA) để tìm ra các yếu tố ảnh hưởng đến Churn.

## 3. Construct (Xây dựng)
**Mục tiêu giai đoạn này:** Xây dựng mô hình học máy.
* **Nhiệm vụ:** Lựa chọn thuật toán phân loại (Classification) phù hợp (ví dụ: Logistic Regression, Random Forest, XGBoost). Huấn luyện (Train) và kiểm tra (Test) mô hình.
* **Đầu ra:** Mô hình dự đoán Churn với các chỉ số đánh giá độ chính xác như Accuracy, Precision, Recall và F1-Score.

## 4. Execute (Thực thi)
**Mục tiêu giai đoạn này:** Trình bày kết quả và đưa ra khuyến nghị.
* **Nhiệm vụ:** Dịch các kết quả kỹ thuật thành ngôn ngữ kinh doanh. Trình bày những hiểu biết sâu sắc (insights) cho ban lãnh đạo Waze.
* **Đầu ra:** Bản tóm tắt điều hành (Executive Summary) và các đề xuất chiến lược giữ chân người dùng.