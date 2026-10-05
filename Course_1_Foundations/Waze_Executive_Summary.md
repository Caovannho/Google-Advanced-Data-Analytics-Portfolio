# 📊 Bản Tóm tắt Điều hành: Khởi động Dự án Waze Churn Prediction

**Người lập:** Data Professional
**Ngày:** [Điền ngày hôm nay]
**Đơn vị:** Waze Data Team

## 1. Bối cảnh & Mục tiêu Dự án
Mục tiêu cốt lõi của dự án là phát triển mô hình Machine Learning dự đoán tỷ lệ người dùng rời bỏ ứng dụng hàng tháng (Churn rate). Việc này giúp Waze chủ động giữ chân người dùng và thúc đẩy tăng trưởng doanh nghiệp.

## 2. Tóm tắt Nhiệm vụ Giai đoạn Đầu
Theo yêu cầu từ May Santner (Quản lý) và Chidi Ga (Senior Data Analyst), nhiệm vụ ưu tiên là kiểm tra, tổ chức và tóm tắt bộ dữ liệu ban đầu bằng Python.
* **Bộ dữ liệu:** `waze_dataset.csv`
* **Kích thước:** 14.999 dòng (người dùng duy nhất) và 13 cột (biến số).

## 3. Đánh giá Biến Dữ liệu (Sơ bộ)
Dữ liệu bao gồm các nhóm biến chính:
* **Biến mục tiêu (Target):** `label` (Phân loại nhị phân: "retained" - giữ lại, hoặc "churned" - rời bỏ).
* **Biến hành vi (Behavioral):** Số phiên truy cập (`sessions`), số lần lái xe (`drives`), số ngày hoạt động (`activity_days`), số ngày lái xe (`driving_days`).
* **Biến cường độ (Intensity):** Tổng số km (`driven_km_drives`), tổng thời lượng (`duration_minutes_drives`).
* **Biến loại hình:** Loại thiết bị (`device`).

## 4. Các bước tiếp theo được khuyến nghị
1. **Tiến hành EDA:** Khám phá sâu hơn dữ liệu người dùng mới thông qua Jupyter Notebook theo đề xuất của Chidi Ga.
2. **Kiểm tra Dữ liệu:** Xác định và xử lý các giá trị bị thiếu (missing values) và các ngoại lệ (outliers) trong các biến định lượng.
3. **Phân tích Tương quan:** Tìm hiểu mối quan hệ giữa biến mục tiêu `label` và các biến hành vi (như `driven_km_drives` hay `activity_days`).