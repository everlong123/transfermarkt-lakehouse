# ⚽ Transfermarkt Data Lakehouse

## 🧩 Giới thiệu
Dự án xây dựng **nền tảng Data Lakehouse** phục vụ phân tích dữ liệu bóng đá từ bộ dữ liệu **Transfermarkt (Kaggle)**.  
Hệ thống triển khai bằng **Docker Compose**, mô phỏng mô hình thực tế gồm ba lớp dữ liệu:
- **Bronze:** Lưu dữ liệu gốc (raw)
- **Silver:** Làm sạch & chuẩn hóa
- **Gold:** Mô hình hóa phục vụ BI & Machine Learning

---

## 🏗️ Kiến trúc hệ thống

```
Kaggle → MinIO (Bronze) → Jupyter/Spark (ETL, ML) → Superset (Dashboard)
```

| Thành phần | Công nghệ | Vai trò |
|-------------|------------|----------|
| Docker Desktop | 25.0+ | Môi trường triển khai |
| MinIO | latest | Data Lake (S3) |
| PostgreSQL | 15 | Metadata cho Superset |
| Jupyter + PySpark | latest | ETL & ML |
| Apache Superset | latest | BI & Dashboard |

---

## 📂 Cấu trúc dự án

```
transfermarkt-lakehouse/
├── docker-compose.yml     # Cấu hình hệ thống
├── data_raw/              # Dữ liệu gốc từ Kaggle
├── notebooks/             # ETL & Machine Learning
├── docs/                  # Báo cáo & hình ảnh minh họa
└── README.md              # Tài liệu dự án
```

---

## 🚀 Triển khai nhanh

### 1️⃣ Chuẩn bị
```bash
mkdir -p data_raw notebooks docs
# Copy dữ liệu từ Kaggle vào data_raw/
```

### 2️⃣ Khởi chạy hệ thống
```bash
docker compose up -d
```

### 3️⃣ Truy cập giao diện
| Thành phần | URL | Tài khoản |
|-------------|-----|------------|
| **MinIO** | [http://localhost:9001](http://localhost:9001) | admin / admin12345 |
| **Jupyter** | [http://localhost:8888/?token=lab](http://localhost:8888/?token=lab) | lab |
| **Superset** | [http://localhost:8088](http://localhost:8088) | admin / admin12345 |

---

## 🔄 Quy trình dữ liệu

| Lớp | Mô tả | Công cụ |
|------|-------|---------|
| **Bronze** | Lưu dữ liệu gốc từ Kaggle | MinIO |
| **Silver** | Làm sạch, chuẩn hóa | PySpark |
| **Gold** | Mô hình hóa Dim/Fact, phục vụ BI | PySpark + Superset |

---

## 📊 Dashboard & Machine Learning

- **Dashboard Superset:** Phân tích chuyển nhượng, hiệu quả chi tiêu, biến động giá trị cầu thủ.  
- **Machine Learning:** Mô hình Linear Regression dự đoán giá trị cầu thủ (`R² ≈ 0.82`).

---

## 👥 Phân công nhóm

| Thành viên | Vai trò | Nhiệm vụ chính |
|-------------|----------|----------------|
| **SV1** | Data Engineer | Thiết lập Docker, ETL, MinIO |
| **SV2** | Data Modeler & BI | Thiết kế Dim/Fact, Dashboard |
| **SV3** | Data Scientist | Phân tích chuyên sâu, Machine Learning |

---

## 📚 Tài liệu tham khảo
- [Transfermarkt Dataset – Kaggle](https://www.kaggle.com/)
- [Apache Superset Docs](https://superset.apache.org)
- [MinIO Docs](https://min.io/docs)
- [Apache Spark Docs](https://spark.apache.org/docs/latest)
