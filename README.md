# ⚙️Lightweight Data Platform on SharePoint
## 1. 📖 Tổng quan

Dự án này tập trung vào việc xây dựng một **Lightweight Data Platform** sử dụng SharePoint làm nền tảng lưu trữ và Power Query làm công cụ xử lý dữ liệu.

Mục tiêu là chuyển từ cách làm báo cáo phụ thuộc vào dữ liệu local sang một hệ thống dữ liệu online, có cấu trúc rõ ràng, hỗ trợ tốt cho việc mở rộng và tối ưu hiệu suất.

---
## 2. 🚨 Vấn đề

Trước khi triển khai:

- Dữ liệu:
    - Lưu trữ local (máy cá nhân)
    - Kết hợp OneDrive nhưng vẫn hoạt động theo kiểu local
- Report:
    - Lưu trên SharePoint
    - Nhưng refresh bằng cách mở file local

Điều này dẫn đến:

### 2.1 Nhập nhằng giữa Online & Offline

- Power Query trên SharePoint không hoạt động đúng do:
    - Source là local
- Không thể refresh trực tiếp trên môi trường online
### 2.2 Hiệu suất kém

- Dữ liệu:
    - Từ nhiều nguồn
    - Chưa được làm sạch
    - Không đúng grain cần thiết
- Thời gian refresh:
    - ~45 phút / report
### 2.3 Thiếu data layer chuẩn

- Không có:
    - Data structure rõ ràng
    - Phân tầng dữ liệu
    - Chuẩn ETL
---
## 3. 🎯 Mục tiêu

- 100% dữ liệu nằm trên **online (SharePoint)**
- Xây dựng **data layer có cấu trúc**
- Chuẩn bị dữ liệu:
    - Sạch
    - Đúng độ chi tiết (grain)
- Tối ưu hiệu suất:
    - Giảm thời gian refresh report
---
## 4. 🛠️ Giải pháp

### 4.1 Centralized Data Source

- Di chuyển toàn bộ dữ liệu lên **SharePoint**
- Power Query đọc trực tiếp từ:
    - SharePoint Files
    - SharePoint Lists
### 4.2 Tối ưu định dạng dữ liệu

- Chuyển đổi:
    - Excel → CSV (đối với file phù hợp)
- Mục tiêu:
    - Tăng tốc độ đọc dữ liệu
    - Giảm overhead
### 4.3 Thiết kế Data Layer

Tổ chức dữ liệu theo các lớp:

- **Raw**: dữ liệu gốc
- **Curated**: dữ liệu đã làm sạch
- **Reference**: dữ liệu tham chiếu
- **Aggregated**: dữ liệu tổng hợp phục vụ report
### 4.4 Chuẩn hóa Grain dữ liệu

- Chuẩn bị sẵn dữ liệu theo các cấp độ:
    - Daily
    - Monthly
    - SKU level
    - Store level

→ Giảm tải xử lý cho report
### 4.5 Data Lifecycle Management

- Phân loại:
    - File cần update
    - File đã **historical freeze**
- Tránh xử lý lại dữ liệu không cần thiết
### 4.6 ETL Workbooks

- Tạo các file ETL riêng:
    - Xử lý dữ liệu đầu vào
    - Chuẩn hóa trước khi đưa vào data layer
### 4.7 Reusable M Code Functions

- Lưu trữ các function Power Query (M Code) dưới dạng `.txt`
- Mục tiêu:
    - Tái sử dụng
    - Giảm thời gian viết lại logic
### 4.8 Data Documentation

- Sử dụng Obsidian để:
    - Lưu cấu trúc dữ liệu
    - Mapping quan hệ giữa các table
- Áp dụng cho:
    - Report
    - ETL pipelines
---
## 5. 📊 Kết quả đạt được

- 100% dữ liệu được:
    - Lưu trên SharePoint Online
    - Truy cập từ bất kỳ đâu
- Data layer:
    - Có cấu trúc rõ ràng
    - Có ETL pipeline hỗ trợ
- Workflow cập nhật dữ liệu:
    - Rõ ràng
    - Có hệ thống
- Hiệu suất cải thiện đáng kể:
    - ⏱️ Refresh time: ~45 phút → ~5 phút
---
## 6. 🔧 Công cụ sử dụng

- SharePoint (Document Library, Lists)
- Power Query (Excel)
- CSV / Excel
- Obsidian (documentation)
---
## 7. 👤 Vai trò của tôi

- Tự thiết kế và triển khai toàn bộ hệ thống
- Xây dựng:
    - Data structure
    - Data layer
    - ETL workflow
- Tối ưu:
    - Performance
    - Data refresh process
- Chuẩn hóa cách làm báo cáo cho bản thân

---

## ✉️ Tác giả
**Tram Dang Tai**  
📍 Merchandise Data Analyst  
📧 [Liên hệ qua LinkedIn](https://www.linkedin.com/in/tramdangtai)


