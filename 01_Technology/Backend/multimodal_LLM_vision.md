# BÁO CÁO KỸ THUẬT: Sử dụng Multimodal LLM VISION để bóc tách file và đọc bài viết

- **Ngày thực hiện:** 2026-11-13
- **Tác giả:** Dương Công Khoa
- **Phân loại:** Dự án thực tế, Học tập
- **Trạng thái:** Đang thực hiện 
- **Vai trò:** Người học và người làm dự án

---

## 1. BỐI CẢNH & MỤC TIÊU (CONTEXT & OBJECTIVES)

### 1.1. Bối cảnh
Khi đã thực hiện xong quá trình xây dựng API Upload tài liệu, bước tiếp theo trong quá trình xây dựng hệ thống AI Portfolio là đọc nội dung từ trong tài liệu đó.

### 1.2. Mục tiêu
- Hiểu và biết cách sử dụng multimodal LLM vision
- Bóc tách được nội dung từ trong file đã được upload
- Xây dựng và triển khai được API đọc dữ liệu

### 1.3. Phạm vi thực hiện
- **Tiếp nhận file:** Sử dụng API để truy xuất tài liệu đã được upload trước đó, hỗ trợ các định dạng PDF, DOCX và hình ảnh.
- **Trích xuất nội dung văn bản:** Sử dụng thư viện PyPDF để đọc nội dung văn bản từ file PDF và Python-docx để xử lý tài liệu Word.
- **Xử lý hình ảnh:** Tích hợp Google Gemini API để phân tích nội dung hình ảnh, nhận diện văn bản và mô tả các thành phần trực quan trong tài liệu.
- **Xử lý dữ liệu:** Chuẩn hóa và tổng hợp nội dung được trích xuất thành dữ liệu văn bản có cấu trúc.
- **Xây dựng API:** Phát triển API đọc và trích xuất nội dung tài liệu bằng FastAPI, kiểm tra dữ liệu đầu vào và xử lý các trường hợp lỗi.
- **Kiểm thử:** Sử dụng Swagger UI để kiểm tra API, đánh giá khả năng đọc và trích xuất nội dung từ các định dạng khác nhau.


---

## 2. CÔNG NGHỆ & CÔNG CỤ SỬ DỤNG (TECH STACK & SKILLS)

Liệt kê công nghệ, công cụ và vai trò cụ thể của từng thành phần.

| Công nghệ / Công cụ | Vai trò trong dự án | Mức độ sử dụng |
|---|---|---|
| python | Ngôn ngữ lập trình chính | 5.0 |
| FastAPI | Xây dựng API đọc và xử lý nội dung tài liệu | 3.5 |
| Google Gemini API | Sử dụng Multimodal LLM Vision để phân tích hình ảnh và nhận diện nội dung tài liệu | 3.0 |
| Google Gen AI SDK | Kết nối và gửi dữ liệu đến mô hình Gemini | 3.0 |
| PyPDF | Đọc và trích xuất văn bản từ file PDF | 2.0 |
| python-docx | Đọc và trích xuất văn bản từ file docx | 2.0 |
| Pillow | Mở, xử lý và chuyển đổi ảnh trước khi gửi đến mô hình kiểm tra | 2.0 |
| Pydantic | Kiểm tra, xác thực và định nghĩa cấu trúc dữ liệu đầu vào, đầu ra | 3.5 |
| uv | Quản lý môi trường ảo và các thư viện python | 4.0 |
| Swagger UI | Kiểm thử và kiểm tra hoạt động của API | 4.0 |

### 2.1. Công nghệ chính
- **FastAPI:** Sử dụng để xây dựng REST API tiếp nhận yêu cầu đọc file, xử lý file và trả về kết quả trích xuất dưới dạng JSON 
- **Google Gemini API:** Tích hợp mô hình Multimodal LLM có khả năng tiếp nhận và phân tích dữ liệu hình ảnh hỗ trợ nhận diện văn bản và hiểu nội dung trực quan trong tài liệu. 
- **PyPDF:** Sử dụng để đọc và trích xuất văn bản từ các tài liệu PDF có chứa lớp văn bản. 
- **python-docx:** Sử dụng để đọc nội dung văn bản, đoạn văn và bảng biểu trong tài liệu word. 
- **Pillow:** Hỗ trợ đọc, kiểm tra và xử lý hình ảnh trước khi đưa vào quá trình phân tích bằng mô hình Gemini.
- **Pydantic:** Định nghĩa Schema, kiểm tra dữ liệu đầu vào và chuẩn hóa cấu trúc phản hồi của API 

### 2.2. Kiến thức và kỹ năng áp dụng
- Kiến thức chuyên môn:  
    * Hiểu khái niệm Multimodal Large Language Model
    * Hiểu cơ chế hoạt động cơ bản của Vision Model trong công việc phân tích hình ảnh 
    * Hiểu các phương pháp trích xuất văn bản từ PDF, DOCX và hình ảnh.
    * Phân biệt xử lý tài liệu có lớp văn bản và tài liệu scan cần OCD/Vision
- Kỹ năng lập trình:
    * Sử dụng Python để đọc, xử lý và trích xuất dữ liệu từ nhiều định dạng file.
    * Xây dựng REST API bằng FastAPI.
    * Tích hợp Google Gemini API thông qua Google Gen AI SDK.
    * Sử dụng Pydantic để kiểm tra và chuẩn hóa dữ liệu.
    * Xử lý ngoại lệ và quản lý luồng dữ liệu giữa các thành phần.
- Kỹ năng phân tích và giải quyết vấn đề:
    * Phân tích cấu trúc và đặc điểm của từng định dạng tài liệu.
    * Lựa chọn phương pháp trích xuất phù hợp với từng loại dữ liệu.
    * Xử lý các trường hợp file không hợp lệ, không đọc được hoặc không chứa văn bản.
    * Đánh giá độ chính xác của nội dung được trích xuất từ mô hình AI.

---

## 3. QUÁ TRÌNH TRIỂN KHAI & CHỨNG CỨ THỰC HÀNH (IMPLEMENTATION & EVIDENCE)

Mô tả những công việc thực tế đã thực hiện. Ưu tiên bằng chứng có thể kiểm chứng.

### 3.1. Các bước triển khai

**Bước 1: Thêm các thư viện**
- Mô tả: Sử dụng uv để thêm các thư viện của python: `google-genai`,  `pypdf`, `python-docx`, `pillow`
```text
uv add google-genai pypdf python-docx pillow
```
- Kết quả: Đã cài được các thư viện cần thiết
- Công nghệ sử dụng: uv

**Bước 2: Chuẩn bị API key**
- Mô tả: Vào google AI studio để tạo API key, sau đó để vào file .env
- Kết quả: Đã tạo API_key vào file env
- Công nghệ sử dụng: 

**Bước 3: Viết module bóc tách**
- Mô tả: Viết Module Bóc Tách Văn Bản Bằng LLM Vision
- Kết quả: Đã tạp file extractor đọc các file văn bản số.
- Công nghệ sử dụng: python, pypdf, python-docx, google-genai

**Bước 3: Viết và bổ sung endpoint kích hoạt bóc tách**
- Mô tả: Bổ sung API endpoint bóc tách ở file reports.py
- Kết quả: Đã có endpoint bóc tách nội dung file
- Công nghệ sử dụng: FastAPI, python

### 3.2. Kiến trúc và thiết kế kỹ thuật
[Mô tả kiến trúc hệ thống, luồng dữ liệu, cấu trúc database hoặc thuật toán.]

### 3.3. Chứng cứ thực hành (Evidence)

| Loại bằng chứng | Mô tả | Đường dẫn / Link |
|---|---|---|
| Source code | [File hoặc module đã thực hiện] | [GitHub URL] |
| Screenshot | [Ảnh minh họa kết quả] | [File path] |
| Database | [Bảng hoặc dữ liệu đã tạo] | [Mô tả] |
| API / Demo | [Endpoint hoặc bản demo] | [URL] |
| Log / Test | [Kết quả kiểm thử] | [File path] |

---

## 4. THÁCH THỨC & BÀI HỌC KINH NGHIỆM (CHALLENGES & KEY LEARNINGS)

### 4.1. Thách thức gặp phải

- **Vấn đề 1: Gemini API không nhận diện được Model.**
  - **Nguyên nhân:** Sử dụng `gemini-1.5-flash` không còn khả dụng với API version và phương thức `generateContent` đang sử dụng.
  - **Ảnh hưởng:** API bóc tách tài liệu trả về HTTP 500, khiến quá trình xử lý ảnh không thể tiếp tục.

- **Vấn đề 2: Không thể lưu kết quả Gemini vào Database.**
  - **Nguyên nhân:** Hàm `process_report_with_llm()` trả về toàn bộ đối tượng `GenerateContentResponse` thay vì chuỗi văn bản Markdown. SQLAlchemy không thể chuyển đổi đối tượng này để lưu vào cột `raw_content` của PostgreSQL.
  - **Ảnh hưởng:** Database phát sinh lỗi `psycopg.ProgrammingError`, khiến thao tác cập nhật dữ liệu thất bại.

- **Vấn đề 3: Gemini API gặp lỗi quá tải.**
  - **Nguyên nhân:** Model Gemini tạm thời không thể xử lý yêu cầu do lưu lượng truy cập cao, trả về HTTP 503 (`UNAVAILABLE`).
  - **Ảnh hưởng:** Quá trình bóc tách tài liệu bị gián đoạn và không thể lưu kết quả vào Database.

### 4.2. Giải pháp xử lý

- **Phương pháp:** Kiểm tra Response body và log lỗi từ Uvicorn để xác định nguyên nhân tại từng công đoạn. Tiến hành sửa lỗi ở tầng tích hợp Google Gemini, xử lý dữ liệu trả về và kiểm tra lại quá trình lưu trữ bằng SQLAlchemy.

- **Các bước thực hiện:**
  1. Kiểm tra lỗi `404 NOT_FOUND`, xác định Model `gemini-1.5-flash` không khả dụng và thay thế bằng Model tương thích.
  2. Xử lý lỗi `GenerateContentResponse` bằng cách sử dụng thuộc tính `response.text` để lấy nội dung văn bản từ Gemini thay vì trả về toàn bộ đối tượng phản hồi.
  3. Kiểm tra lỗi `503 UNAVAILABLE`, xác định đây là sự cố quá tải tạm thời từ phía dịch vụ Google Gemini và thực hiện gọi lại API sau một khoảng thời gian.
  4. Kiểm thử lại API `POST /api/reports/{report_id}/process` thông qua Swagger UI.
  5. Kiểm tra kết quả bóc tách và xác nhận nội dung Markdown được cập nhật vào trường `raw_content` trong Database.

- **Kết quả:**
  - Khắc phục được các lỗi trong quá trình tích hợp Google Gemini API.
  - Hoàn thiện luồng xử lý từ upload tài liệu, gửi dữ liệu đến Gemini Vision, nhận kết quả Markdown đến cập nhật Database.
  - Kiểm thử thành công chức năng bóc tách nội dung từ hình ảnh tài liệu và lưu kết quả vào PostgreSQL/Supabase.

### 4.3. Bài học kinh nghiệm

- **Kiến thức kỹ thuật mới tiếp thu:**
  - Hiểu cách tích hợp Google Gemini API thông qua thư viện `google-genai` để xử lý hình ảnh và trích xuất văn bản bằng LLM Vision.
  - Hiểu cách sử dụng `response.text` để lấy nội dung văn bản từ đối tượng `GenerateContentResponse`.
  - Nắm được cách xử lý và phân biệt các mã lỗi HTTP phổ biến khi tích hợp dịch vụ AI như `404 NOT_FOUND`, `500` và `503 UNAVAILABLE`.
  - Hiểu cách kết hợp FastAPI, SQLAlchemy và PostgreSQL để xây dựng quy trình tiếp nhận, xử lý và lưu trữ tài liệu.

- **Sai lầm cần tránh trong tương lai:**
  - Không nên mặc định tên Model AI luôn khả dụng; cần kiểm tra danh sách Model và khả năng hỗ trợ phương thức API trước khi tích hợp.
  - Cần kiểm tra kiểu dữ liệu trả về từ các thư viện bên ngoài trước khi đưa vào Database.
  - Không nên xem mọi lỗi HTTP 500 là lỗi Database hoặc lỗi code; cần phân tích Response body và traceback để xác định đúng tầng phát sinh lỗi.

- **Kinh nghiệm về thiết kế, triển khai và tối ưu hệ thống:**
  - Nên tách biệt trách nhiệm giữa Router, Service và Database để dễ kiểm thử và bảo trì.
  - Cần thiết kế cơ chế xử lý lỗi và Retry đối với các dịch vụ AI bên ngoài nhằm tăng độ ổn định của hệ thống.
  - Nên lưu trữ riêng đường dẫn file gốc và nội dung Markdown đã trích xuất để hỗ trợ xử lý lại tài liệu khi cần thiết.
  - Cần kiểm thử từng công đoạn độc lập trước khi kiểm thử toàn bộ quy trình tích hợp.

---



## 5. KẾT QUẢ & ĐÁNH GIÁ (RESULTS & EVALUATION)

### 5.1. Kết quả đạt được

- Xây dựng thành công API Upload tài liệu bằng FastAPI, hỗ trợ các định dạng PDF, DOCX, PNG, JPG, JPEG và Markdown. File được lưu trữ trong thư mục `uploads/` và thông tin tài liệu được ghi nhận vào PostgreSQL thông qua SQLAlchemy.
- Tích hợp thành công Google Gemini Vision thông qua thư viện `google-genai`, cho phép gửi hình ảnh tài liệu đến mô hình AI để nhận diện và trích xuất nội dung văn bản dưới định dạng Markdown.
- Xây dựng API `POST /api/reports/{report_id}/process` để kích hoạt quá trình bóc tách tài liệu, xử lý kết quả trả về và cập nhật nội dung Markdown vào trường `raw_content` trong Database.
- Hoàn thành kiểm thử thực tế hai API Upload và Process thông qua Swagger UI, xác nhận quy trình tiếp nhận, xử lý bằng AI và lưu trữ kết quả hoạt động thành công.
- Xử lý được các lỗi phát sinh trong quá trình tích hợp Gemini API, chuyển đổi kiểu dữ liệu phản hồi và thao tác cập nhật dữ liệu bằng SQLAlchemy.

### 5.2. Đánh giá mức độ thành thạo

| Công nghệ / Kỹ năng | Điểm tự đánh giá (1.0 - 5.0) | Cơ sở đánh giá |
|---|---:|---|
| Python | 3.5 | Sử dụng hàm, xử lý ngoại lệ, thao tác file và tổ chức logic xử lý dữ liệu. |
| FastAPI | 3.5 | Xây dựng API Upload và Process, sử dụng Router, Dependency Injection và HTTPException. |
| SQLAlchemy | 3.0 | Truy vấn, tạo bản ghi, cập nhật dữ liệu và quản lý transaction với Database. |
| PostgreSQL / Supabase | 3.0 | Thiết kế và thao tác với bảng Report, lưu trữ thông tin tài liệu và nội dung trích xuất. |
| Google Gemini API | 3.0 | Tích hợp Google GenAI SDK, gửi hình ảnh đến Gemini Vision và xử lý kết quả Markdown. |
| Pydantic | 3.0 | Sử dụng Schema để định nghĩa và kiểm soát dữ liệu đầu vào, đầu ra của API. |
| REST API & Swagger UI | 3.5 | Thiết kế endpoint và kiểm thử API thực tế thông qua giao diện Swagger UI. |
| Debugging & Error Handling | 3.5 | Phân tích HTTP 404, 500, 503 và lỗi kiểu dữ liệu từ SQLAlchemy để tìm nguyên nhân và khắc phục. |

*Thang điểm: 1.0 – 2.0: Cơ bản; 2.1 – 3.0: Đang phát triển; 3.1 – 4.0: Khá; 4.1 – 5.0: Thành thạo.*

### 5.3. Hạn chế hiện tại

- **Khả năng xử lý tài liệu:** Chưa tối ưu việc xử lý PDF nhiều trang, tài liệu dung lượng lớn và các hình ảnh có chất lượng thấp hoặc chữ viết tay khó nhận diện.
- **Quản lý file:** File gốc hiện được lưu trong thư mục `uploads/` trên máy chủ, chưa có giải pháp lưu trữ tập trung như Supabase Storage hoặc Amazon S3.
- **Khả năng phục hồi lỗi:** Chưa hoàn thiện cơ chế Retry tự động, quản lý trạng thái xử lý và ghi log chi tiết khi Gemini API gặp sự cố.
- **Hiệu năng hệ thống:** Quá trình gọi Gemini hiện được thực hiện đồng bộ trong API Request, có thể làm tăng thời gian phản hồi khi xử lý tài liệu lớn.
- **Kiểm soát kết quả AI:** Chưa xây dựng cơ chế đánh giá độ chính xác của nội dung Markdown được trích xuất và đối chiếu tự động với tài liệu gốc.


---

## 6. ĐỊNH HƯỚNG PHÁT TRIỂN (FUTURE IMPROVEMENTS)

- **Mở rộng khả năng xử lý tài liệu:** Bổ sung khả năng bóc tách nội dung từ PDF nhiều trang, tài liệu có bảng biểu, hình ảnh scan và chữ viết tay phức tạp. Nghiên cứu tích hợp các công cụ OCR chuyên dụng để cải thiện độ chính xác khi nhận diện văn bản.

- **Tối ưu hệ thống lưu trữ:** Chuyển việc lưu trữ file từ thư mục cục bộ `uploads/` sang Supabase Storage hoặc Amazon S3 nhằm tăng khả năng quản lý, bảo mật và mở rộng dung lượng lưu trữ.

- **Cải thiện độ ổn định của Gemini API:** Xây dựng cơ chế Retry tự động với Exponential Backoff, quản lý lỗi và ghi log chi tiết khi dịch vụ AI gặp sự cố. Bổ sung cơ chế quản lý trạng thái xử lý tài liệu như `PENDING`, `PROCESSING`, `COMPLETED` và `FAILED`.

- **Tối ưu hiệu năng xử lý:** Nghiên cứu triển khai tác vụ nền (Background Tasks) hoặc hàng đợi xử lý (Task Queue) như Celery và Redis để xử lý tài liệu không đồng bộ, tránh làm API Request phải chờ quá lâu khi tài liệu có dung lượng lớn.

- **Phát triển hệ thống RAG:** Sử dụng nội dung Markdown đã bóc tách để chia nhỏ văn bản (Text Chunking), tạo Embedding và lưu trữ Vector vào PostgreSQL thông qua Supabase Vector. Từ đó xây dựng hệ thống truy vấn ngữ nghĩa (Semantic Search) và chatbot RAG có khả năng trả lời câu hỏi dựa trên tài liệu đã lưu trữ.

- **Nâng cao khả năng đánh giá chất lượng AI:** Xây dựng bộ dữ liệu kiểm thử để so sánh nội dung trích xuất với tài liệu gốc, đánh giá độ chính xác nhận diện văn bản và khả năng giữ nguyên cấu trúc Markdown.

- **Tăng cường bảo mật:** Bổ sung giới hạn dung lượng upload, kiểm tra nội dung file, kiểm soát quyền truy cập tài liệu và bảo vệ API Key thông qua biến môi trường.

- **Hướng nghiên cứu tiếp theo:** Nghiên cứu quy trình kết hợp LLM Vision, OCR, Embedding và Retrieval-Augmented Generation (RAG) để xây dựng hệ thống quản lý tri thức cá nhân, hỗ trợ tìm kiếm và khai thác thông tin từ CV, báo cáo kỹ thuật, tài liệu học tập và các dự án đã thực hiện.
---
