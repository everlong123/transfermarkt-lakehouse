
# ⚽ TRANSFERMARKT DATA LAKEHOUSE

## 🧠 Giới thiệu

Đề tài **Xây dựng Data Lakehouse cho phân tích dữ liệu bóng đá từ Transfermarkt** nhằm minh họa mô hình kiến trúc dữ liệu hiện đại kết hợp giữa **Data Lake** và **Data Warehouse** bằng hệ sinh thái mã nguồn mở.

Dự án sử dụng các công cụ chính sau:
- **Docker Compose**: triển khai toàn bộ hệ thống container.
- **MinIO (S3)**: lưu trữ dữ liệu theo ba lớp chuẩn **Bronze – Silver – Gold**.
- **Apache Spark (PySpark)**: xử lý, làm sạch và mô hình hóa dữ liệu.
- **PostgreSQL**: kho dữ liệu phân tích và nguồn cho trực quan hóa.
- **Apache Superset**: tạo dashboard phân tích và trình bày insight.

Dữ liệu được thu thập từ **Transfermarkt / Kaggle**, bao gồm thông tin cầu thủ, câu lạc bộ, chuyển nhượng và hiệu suất thi đấu. Mục tiêu là xây dựng quy trình phân tích dữ liệu toàn diện, từ thu thập – xử lý – mô hình hóa – trực quan hóa.

---

## 🎯 Mục tiêu chính

- Thiết kế kiến trúc **Data Lakehouse end-to-end** có thể tái sử dụng.  
- Triển khai pipeline **ETL/ELT** từ dữ liệu thô đến mô hình phân tích.  
- Tổ chức dữ liệu theo **Star Schema (Dim–Fact)** cho BI và ML.  
- Tạo **dashboard Superset** phân tích chuyển nhượng, giá trị cầu thủ và hành vi câu lạc bộ.  
- Huấn luyện mô hình **Machine Learning (Spark MLlib)** để **dự đoán giá trị cầu thủ**.

---

## 🧩 Kiến trúc tổng thể

```
Transfermarkt Data Lakehouse
├── data_raw/              # Dữ liệu thô (từ Kaggle/Transfermarkt)
├── notebooks/             # Notebook ETL & ML (Bronze → Silver → Gold)
├── docker-compose.yml     # Cấu hình MinIO, PostgreSQL, Jupyter, Superset
└── README.md
```

Quy trình xử lý dữ liệu được chia làm 3 lớp:
| Lớp | Mô tả | Công cụ |
|------|--------|----------|
| **Bronze** | Dữ liệu gốc từ Kaggle, lưu trên MinIO | MinIO |
| **Silver** | Làm sạch và chuẩn hóa | PySpark |
| **Gold** | Mô hình hóa (Dim/Fact), phục vụ BI và ML | Spark + PostgreSQL |

---

## 📊 Trực quan hóa & Phân tích

Dashboard trong Superset minh họa:
- **Age vs Market Value**: xu hướng giá trị cầu thủ theo độ tuổi.  
- **Performance Impact**: mối liên hệ giữa hiệu suất (goals/assists per90) và giá trị chuyển nhượng.  
- **Position vs Value**: so sánh giá trị trung bình theo vị trí thi đấu.  
- **Club Spending & Prestige**: phân tích hành vi mua – bán cầu thủ của các CLB lớn.

---

## 🤖 Machine Learning

Mô hình **Linear Regression** và **Random Forest** được huấn luyện trên tập dữ liệu đã chuẩn hóa để dự đoán **latest_fee (giá trị cầu thủ)**.  
Các đặc trưng chính gồm:  
`age, goals_per90, assists_per90, minutes_played, position, prestige_overall, age², age × goals_per90`.

Kết quả mô hình minh họa:
- **R² (log scale)** ≈ 0.31  
- **RMSE (fee)** ≈ 12–14 triệu EUR  
→ Mức chính xác phù hợp với dữ liệu công khai, thể hiện khả năng mô hình nắm bắt được xu hướng định giá cầu thủ thực tế.

---

## 🚀 Cách chạy nhanh

```bash
# Khởi động toàn bộ stack
docker compose up -d

# Truy cập giao diện
MinIO:     http://localhost:9001
Jupyter:   http://localhost:8888/?token=lab
Superset:  http://localhost:8088
```

---

## 📚 Tham khảo

- Transfermarkt Dataset (Kaggle)  
- Apache Spark & Delta Lake Documentation  
- Apache Superset Docs  
- MinIO Object Storage Docs  
- Docker Compose Guide  
- Medium: “Build a Data Lakehouse with Docker”

---

> Dự án minh họa kiến trúc Data Lakehouse phục vụ học tập và nghiên cứu trong lĩnh vực phân tích dữ liệu và khoa học dữ liệu.
