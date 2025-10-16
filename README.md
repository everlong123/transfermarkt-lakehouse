# ⚽ Transfermarkt Lakehouse Project

## 🚀 Giới thiệu
Dự án **Transfermarkt Lakehouse** được xây dựng nhằm mô phỏng một hệ thống phân tích dữ liệu bóng đá hoàn chỉnh, từ thu thập – xử lý – phân tích – trực quan hóa.  
Dữ liệu được lấy từ **Transfermarkt (Kaggle)**, triển khai trên kiến trúc **Data Lakehouse 3 lớp (Bronze, Silver, Gold)** và chạy hoàn toàn bằng **Docker Compose**.

---

## 🏗️ Kiến trúc tổng thể

┌──────────────────────────┐
│ Data Source │
│ Kaggle - Transfermarkt │
└─────────────┬────────────┘
│
▼
┌──────────────────────────┐
│ MinIO (Data Lake) │
│ - Lưu dữ liệu Bronze/Silver/Gold │
│ - Giao tiếp qua S3 API │
└─────────────┬────────────┘
│
▼
┌──────────────────────────┐
│ Jupyter Notebook (PySpark) │
│ - ETL: Bronze → Silver → Gold │
│ - Phân tích & Machine Learning │
└─────────────┬────────────┘
│
▼
┌──────────────────────────┐
│ Apache Superset (BI) │
│ - Dashboard & Visualization │
└──────────────────────────┘

yaml
Copy code

---

## ⚙️ Công nghệ sử dụng

| Thành phần | Công nghệ | Vai trò |
|-------------|-----------|----------|
| 🐳 **Docker Compose** | 25.0+ | Quản lý & khởi động toàn bộ service |
| 🗄️ **MinIO** | latest | Lưu trữ dữ liệu dạng object (Data Lake) |
| 🧠 **Jupyter / PySpark** | latest | ETL, EDA, Machine Learning |
| 🧩 **PostgreSQL** | 15 | Metadata backend cho Superset |
| 📊 **Apache Superset** | latest | Business Intelligence & Dashboard |

---

## 📂 Cấu trúc thư mục

transfermarkt-lakehouse/
│
├── docker-compose.yml # Định nghĩa các service (MinIO, Postgres, Jupyter, Superset)
├── data_raw/ # Dữ liệu gốc từ Kaggle
├── notebooks/ # Notebook xử lý ETL & ML
├── docs/ # Hình ảnh, báo cáo, tài liệu minh họa
└── README.md # Hướng dẫn dự án

yaml
Copy code

---

## 🧱 Hướng dẫn cài đặt và chạy hệ thống

### 1️⃣ Clone repository
```bash
git clone https://github.com/everlong123/transfermarkt-lakehouse.git
cd transfermarkt-lakehouse
2️⃣ Cài đặt Git LFS (nếu chưa có)
bash
Copy code
git lfs install
git lfs pull
3️⃣ Tải dữ liệu Kaggle
Tải dataset tại:
👉 Transfermarkt Dataset on Kaggle
Giải nén và đặt file vào:

bash
Copy code
transfermarkt-lakehouse/data_raw/
4️⃣ Khởi động hệ thống
bash
Copy code
docker compose up -d
Kiểm tra các service:

Thành phần	URL	Ghi chú
🗄️ MinIO	http://localhost:9001	user: admin, pass: admin12345
📘 Jupyter Notebook	http://localhost:8888/?token=lab	Chạy ETL và ML
📊 Apache Superset	http://localhost:8088	user: admin, pass: admin12345

🔁 Quy trình xử lý dữ liệu
Lớp	Mục đích	Thành phần
Bronze	Lưu dữ liệu gốc từ Kaggle	MinIO
Silver	Làm sạch & chuẩn hóa	Jupyter (PySpark)
Gold	Mô hình hóa Dim/Fact phục vụ BI	Jupyter + Superset

Notebook chính:

etl_bronze_to_silver.ipynb

etl_silver_to_gold.ipynb

ml_player_value_prediction.ipynb

📊 Dashboard & Phân tích
Apache Superset hiển thị các chỉ số chính:

📈 Tổng giá trị chuyển nhượng theo mùa

⚽ Hiệu quả chi tiêu của các CLB

💰 Biến động giá trị cầu thủ theo thời gian

🧩 Dự đoán giá trị cầu thủ (Machine Learning)

Dashboard tổng hợp:
➡️ Transfermarkt Analytics Dashboard

👥 Phân công nhóm
Thành viên	Vai trò	Nhiệm vụ
SV1	Data Engineer	Xây dựng hạ tầng Docker, ETL Bronze → Silver
SV2	Data Modeler & BI	Thiết kế schema Gold, tạo dashboard
SV3	Data Scientist	Phân tích nâng cao, ML dự đoán giá cầu thủ

🧹 Quản lý hệ thống
Tác vụ	Lệnh
Dừng hệ thống	docker compose down
Khởi động lại	docker compose up -d
Xem log Superset	docker compose logs -f superset

📚 Tài liệu tham khảo
Transfermarkt Dataset – Kaggle

Apache Superset Docs

Apache Spark Docs

MinIO Documentation
