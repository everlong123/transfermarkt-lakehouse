# ⚽ Transfermarkt Data Lakehouse

## 🧩 Giới thiệu
Dự án xây dựng **nền tảng Data Lakehouse** phục vụ phân tích dữ liệu bóng đá từ bộ dữ liệu **Transfermarkt (Kaggle)**.  
Hệ thống được triển khai bằng **Docker Compose**, mô phỏng kiến trúc thực tế gồm các lớp dữ liệu:
- **Bronze:** Lưu dữ liệu gốc (raw)
- **Silver:** Làm sạch & chuẩn hóa
- **Gold:** Mô hình hóa phục vụ BI & Machine Learning

---

## 🏗️ Kiến trúc hệ thống

```text
Kaggle → MinIO (Bronze) → Jupyter/Spark (ETL, ML) → Superset (Dashboard)
```
THÀNH PHẦN CHÍNH
| Thành phần        | Công nghệ | Vai trò               |
| ----------------- | --------- | --------------------- |
| Docker Desktop    | 25.0+     | Môi trường triển khai |
| MinIO             | latest    | Data Lake (S3)        |
| PostgreSQL        | 15        | Metadata cho Superset |
| Jupyter + PySpark | latest    | ETL & ML              |
| Apache Superset   | latest    | BI & Dashboard        |

Cấu trúc dự án
transfermarkt-lakehouse/
├── docker-compose.yml     # Cấu hình hệ thống
├── data_raw/              # Dữ liệu gốc từ Kaggle
├── notebooks/             # ETL & Machine Learning
├── docs/                  # Báo cáo & hình ảnh minh họa
└── README.md              # Tài liệu dự án

🚀 Triển khai nhanh
1️⃣ Chuẩn bị
mkdir -p data_raw notebooks docs
# Copy dữ liệu từ Kaggle vào data_raw/



