# BÁO CÁO KỸ THUẬT: THIẾT KẾ DATABASE CHO DỰ ÁN AI - PORTFOLIO

- **Ngày thực hiện:** 2026-11-09
- **Tác giả:** DƯƠNG CÔNG KHOA
- **Phân loại:** Dự án thực tế
- **Trạng thái:** Hoàn thành
- **Vai trò:** Người làm dự án

---

## 1. BỐI CẢNH & MỤC TIÊU (CONTEXT & OBJECTIVES)  

Xây dựng hệ thống AI PORTFOLIO cho phép lưu trữ thông tin cá nhân, dự án, kĩ năng và tài liệu minh chứng. Mục tiêu là tạo nền tảng dữ liệu phục vụ truy vấn ngữ nghĩa và phát triển chatbot RAG giúp nhà tuyển dụng tìm hiểu năng lực của ứng viên

## 2. CÔNG NGHỆ & CÔNG CỤ SỬ DỤNG (TECH STACK & SKILLS)

Liệt kê công nghệ, công cụ và vai trò cụ thể của từng thành phần.

| Công nghệ / Công cụ | Vai trò trong dự án | Mức độ sử dụng |
| --- | --- | --- |
| python | Ngôn ngữ lập trình backend | 5.0/5.0 |
| FastAPI | Xây dựng REST API | 4.0/5.0 |
| SQLAlchemy | ORM, ánh xạ python model với database | 5.0/5.0 |
| Supabase | Cung cấp dịch vụ PostgreSQL trên cloud | 4.0/5.0 |
| python-dotenv | Quản lý biến môi trường từ file env | 5.0/5.0 |

---

## 3. QUÁ TRÌNH TRIỂN KHAI & CHỨNG CỨ THỰC HÀNH (IMPLEMENTATION & EVIDENCE)

Mô tả những công việc thực tế đã thực hiện. Ưu tiên bằng chứng có thể kiểm chứng.

### 3.1. Các bước triển khai

**Bước 1: Thiết kế các bảng dữ liệu**  

- Mô tả: Thiết kế 6 bảng dữ liệu bao gồm: *users*, *projects*, *skills*, *reports*, *skill_evidences*, *contacts*.  

- Kết quả: 6 bảng dữ liệu có các thuộc tính
- Công nghệ sử dụng: *SQLAlchemy*

**Bước 2: Thiết kế khóa cho các bảng dữ liệu**  

- Mô tả: Tôi xác định các khóa bao gồm khóa chính và khóa ngoại của các bảng
- Kết quả: Cụ thể ở các bảng như sau: *users*, *projects*, *skills*, *reports*, *contacts*, *skill_evidences* đều có khóa chính là **id**, riêng bảng *skill_evidences* có thêm các khóa ngoại được tham chiếu từ bảng *skills*, *reports*, và *projects*
- Công nghệ sử dụng: *SQLAlchemy*

**Bước 3: Thiết lập mối quan hệ giữa các bảng**  

- Mô tả:  
Một kĩ năng (*skills*) có thể được được thể hiện trong nhiều dự án, một dự án (*projects*) có thể thể hiện được nhiều kĩ năng.  
Một kĩ năng có thể xuất hiện nhiều trong báo cáo (*reports*), và một báo cáo có thể xuất hiện nhiều kĩ năng (*skills*).  
Mỗi kĩ năng có 0 hoặc nhiều bằng chứng nhưng mỗi bằng chứng (*skills_evidences*) chỉ thuộc về đúng 1 kĩ năng.  
Một dự án có 0 hoặc nhiều bằng chứng, mỗi bằng chứng thuộc về 0 hoặc 1 dự án.   
Một bản báo cáo có 0 hoặc nhiều bằng chứng, mỗi bằng chứng thuộc về 0 hoặc 1 báo cáo. 

- Kết quả:  
    *skills* - *projects*: quan hệ N - N thông qua bảng *skill_evidences*

    *skills* - *reports*: quan hệ N - N thông qua bảng *skill_evidences*

    *skills* - *skill_evidences*: quan hệ 1 - N

    *reports* - *skill_evidences*: quan hệ 1 - N

    *projects* - *skill_evidences*: quan hệ 1 - N


**Bước 4: Sử dụng SQLAlchemy ORM để ánh xạ**
- Mô tả: Sử dụng thư viện SQLAlchemy của python để ánh xạ các bảng sang python model, sau đó cấu hình kết nối PostgresSQL với supabase

---

## 4. THÁCH THỨC & BÀI HỌC KINH NGHIỆM (CHALLENGES & KEY LEARNINGS)

### 4.1. Thách thức gặp phải
- **Vấn đề:** Thiếu postgresql driver psycopg khi chạy ứng dụng
- **Nguyên nhân:** *skills* bị thiếu primary key nên SQLAlchemy không nhận diện được. Khai báo nhầm tham số default cho trường created_at trong model SkillEvidence

### 4.2. Giải pháp xử lý
- **Các bước thực hiện:** Cài đặt PostgreSQL driver phù hợp với phiên bản đang sử dụng. Kiểm tra quá trình import Model và đăng kí metadata để SQLAlchemy nhận diện đầy đủ các bảng. Kiểm tra cấu hình Base và khai báo khóa chính cho từng model. Điều chỉnh tham số khai báo giá trị mặc định cho trường created_at của bảng *skill_evidences* là default.
- **Kết quả:** Đã chạy không còn lỗi, các bảng đã được tạo thành công trên supabase.

### 4.3. Bài học kinh nghiệm
- Hiểu được cách thiết kế database quan hệ bằng SQLAlchemy ORM.
- Hiểu cách khai báo Primary key, Foreign key và relationship.
- Biết cách tổ chức các model trong dự án FastAPI.
- Hiểu cách cấu hình kết nối PostgreSQL thông qua Supabase.
- Biết cách quản lý thông tin kết nối bằng biến môi trường.  

---

## 5. KẾT QUẢ & ĐÁNH GIÁ (RESULTS & EVALUATION)

### 5.1. Kết quả đạt được
- Hoàn thành việc xây dựng 6 SQLAlchemy Model.
- Thiết lập được cấu trúc khóa chính, khóa ngoại và các quan hệ dữ liệu.
- Kết nối được ứng dụng FastAPI với PostSQL trên supabase 
- Ứng dụng có thể khởi chạy mà không còn các lỗi đã đề cập 

### 5.2. Đánh giá mức độ thành thạo

| Công nghệ / Kỹ năng | Điểm tự đánh giá (1.0 - 5.0) |
|---|---|
| python | 3 |
| FastAPI | 2 |
| SQLAlchemy | 3 |
| Supabase | 3 |
| database design | 3 |


## 6. ĐỊNH HƯỚNG PHÁT TRIỂN (FUTURE IMPROVEMENTS)

- Xây API CRUD và bảo mật JWT

