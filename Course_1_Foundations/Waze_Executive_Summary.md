# 📊 Bản Tóm tắt Điều hành: Khởi động Dự án Waze Churn Prediction

**Người lập:** Data Professional
**Ngày:** [Điền ngày hôm nay]
**Đơn vị:** Waze Data Team

## 1. Bối cảnh & Mục tiêu Dự án
Waze hướng tới việc cung cấp trải nghiệm điều hướng an toàn và hiệu quả cho tài xế toàn cầu. Gần đây, ban lãnh đạo đã đặt ưu tiên cho việc cải thiện tỷ lệ giữ chân người dùng (User Retention). 
Mục tiêu cốt lõi của dự án này là phát triển một **mô hình Machine Learning dự đoán tỷ lệ người dùng rời bỏ ứng dụng hàng tháng (Churn rate)**. Việc xác định sớm các phân khúc người dùng có nguy cơ rời bỏ cao sẽ giúp Waze chủ động triển khai các chiến dịch tương tác và ưu đãi đặc biệt để giữ chân họ.

## 2. Các bên liên quan (Stakeholders)
* **Harriet Hadzic** (Giám đốc Phân tích Dữ liệu) & **May Santner** (Quản lý Phân tích Dữ liệu): Phê duyệt kết quả định hướng và mô hình dự đoán.
* **Sylvester Esperanza** (Quản lý Dự án Cấp cao): Theo dõi tiến độ và các cột mốc dự án.
* **Chidi Ga** (Nhà phân tích dữ liệu cao cấp): Hỗ trợ kỹ thuật và đánh giá quy trình Phân tích Dữ liệu Khám phá (EDA).
* **Đội ngũ đa chức năng:** Emrick Larson (Tài chính) và Ursula Sayo (Vận hành).

## 3. Các bước triển khai ban đầu (Khóa 1)
Dựa trên cuộc họp khởi động dự án, nhóm dữ liệu sẽ thực hiện các bước chuẩn bị sau bằng ngôn ngữ **Python**:
1. Xây dựng Dataframe từ bộ dữ liệu Waze thô.
2. Kiểm tra và tóm tắt kiểu dữ liệu (`Dtypes`) của từng biến số.
3. Thu thập các số liệu thống kê mô tả ban đầu để chuẩn bị cho giai đoạn Khám phá Dữ liệu (EDA).

## 4. Rủi ro & Lưu ý
* Cần định nghĩa rõ ràng thế nào là "Churn" trong ngữ cảnh của Waze (ví dụ: không mở app trong 30 ngày hay đã gỡ cài đặt).
* Phải đảm bảo tính nhất quán của dữ liệu trước khi đưa vào mô hình học máy theo đúng yêu cầu từ đội ngũ phân tích cấp cao.