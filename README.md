# sleep-quality-prediction
# 😴 Dự đoán Chất lượng Giấc ngủ (Sleep Quality Prediction)

## 1. Giới thiệu đề tài
**Bài toán:** Chất lượng giấc ngủ đóng vai trò quan trọng đối với sức khỏe thể chất và tinh thần. Dự án này xây dựng một hệ thống Machine Learning để dự đoán chất lượng giấc ngủ của người dùng dựa trên các chỉ số sức khỏe và thói quen sinh hoạt.

**Mục tiêu:**
* Phân tích các yếu tố ảnh hưởng đến giấc ngủ (Stress, BMI, Hoạt động thể chất...).
* Xây dựng mô hình phân lớp để dự đoán chất lượng giấc ngủ theo 3 mức độ: **Kém, Trung bình, Tốt**.
* Xây dựng ứng dụng Web giúp người dùng tự kiểm tra và nhận lời khuyên cải thiện.

## 2. Dataset
* **Nguồn dữ liệu:** Tập dữ liệu `Sleep_health_and_lifestyle_dataset.csv` (đã bao gồm trong thư mục `data/`).
* **Kích thước:** ~374 bản ghi.
* **Mô tả các đặc trưng (Features):**
    * `Gender`: Giới tính.
    * `Age`: Tuổi.
    * `Occupation`: Nghề nghiệp.
    * `Sleep Duration`: Thời gian ngủ (giờ/ngày).
    * `Quality of Sleep`: Điểm chất lượng giấc ngủ (Target gốc: thang 1-10).
    * `Physical Activity Level`: Mức độ hoạt động thể chất (phút/ngày).
    * `Stress Level`: Mức độ căng thẳng (thang 1-10).
    * `BMI Category`: Chỉ số khối cơ thể (Normal, Overweight, Obese).
    * `Blood Pressure`: Huyết áp (dạng chuỗi "126/83").
    * `Heart Rate`: Nhịp tim (bpm).
    * `Daily Steps`: Số bước chân hàng ngày.
    * `Sleep Disorder`: Rối loạn giấc ngủ (None, Insomnia, Sleep Apnea).

## 3. Pipeline (Quy trình thực hiện)
Quy trình xử lý từ dữ liệu thô đến ứng dụng thực tế:

1.  **Tiền xử lý (Preprocessing):**
    * Xử lý giá trị thiếu (Missing Values) ở cột `Sleep Disorder` (điền "None").
    * Feature Engineering: Tách cột `Blood Pressure` thành 2 cột số `Systolic` (Tâm thu) và `Diastolic` (Tâm trương).
    * Label Encoding: Mã hóa dữ liệu phân loại (`Gender`, `Occupation`, `BMI`, `Sleep Disorder`).
    * Target Binning: Gom nhóm `Quality of Sleep` thành 3 nhãn: **0 (Kém)**, **1 (Trung bình)**, **2 (Tốt)**.
2.  **Huấn luyện (Training):** Chia tập dữ liệu Train/Test (tỷ lệ 80/20) và huấn luyện mô hình.
3.  **Đánh giá (Evaluation):** Kiểm tra độ chính xác (Accuracy), Confusion Matrix và vẽ Learning Curve.
4.  **Triển khai (Inference):** Tích hợp mô hình vào ứng dụng web bằng Streamlit.

## 4. Mô hình sử dụng
Nhóm nghiên cứu và áp dụng hai thuật toán:

* **Decision Tree (Cây quyết định):**
    * *Lý do chọn:* Mô hình đơn giản, dễ giải thích, giúp trực quan hóa quy trình ra quyết định.
    * *Cấu hình:* `criterion='entropy'`, `max_depth=3`.
* **Random Forest (Rừng ngẫu nhiên):**
    * *Lý do chọn:* Khắc phục nhược điểm Overfitting của Decision Tree, cho độ chính xác cao hơn và ổn định hơn trên tập dữ liệu nhỏ.
    * *Kết quả:* Được chọn làm mô hình chính cho ứng dụng Demo.

## 5. Kết quả thực nghiệm
Đánh giá trên tập kiểm thử (Test set):

| Metric | Decision Tree | Random Forest |
| :--- | :--- | :--- |
| **Accuracy** | ~ 89% | **~ 93% - 97%** |
| **Precision** | Cao | Cao hơn |
| **Stability** | Trung bình | Tốt (dựa trên Learning Curve) |

## 6. Hướng dẫn chạy dự án

### Bước 1: Cài đặt môi trường (Khuyên dùng Virtual Environment)

Mở Terminal (hoặc CMD/PowerShell) tại thư mục gốc của dự án và thực hiện các lệnh sau:

**1. Tạo môi trường ảo:**
* *Windows:*
    ```bash
    python -m venv venv
    ```
* *macOS/Linux:*
    ```bash
    python3 -m venv venv
    ```

**2. Kích hoạt môi trường ảo:**
* *Windows:*
    ```bash
    .\venv\Scripts\activate
    ```
* *macOS/Linux:*
    ```bash
    source venv/bin/activate
    ```

**3. Cài đặt các thư viện cần thiết:**
```bash
pip install -r requirements.txt
