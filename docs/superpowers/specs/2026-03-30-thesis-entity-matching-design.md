# Đặc tả Thiết kế Luận văn: Entity Matching với AI Agents và SLMs

## 1. Tổng quan Đề tài
**Tên đề tài (Gợi ý):** Nghiên cứu khung kiến trúc Multi-Agent kết hợp Small Language Models (SLMs) cho bài toán Đối soát Thực thể (Entity Matching) trên dữ liệu Thương mại điện tử không đồng nhất.

**Mục tiêu:** Xây dựng một hệ thống Entity Matching đạt độ chính xác tương đương các mô hình ngôn ngữ lớn (LLM) nhưng vận hành hiệu quả trên tài nguyên phần cứng hạn chế (PC cá nhân) bằng cách sử dụng các mô hình nhỏ (Small Language Models) và kiến trúc đa tác tử (Multi-Agent).

---

## 2. Kiến trúc Hệ thống (Tri-Agentic Framework)

Hệ thống được thiết kế theo cấu trúc lãnh đạo dọc (Vertical Leadership) gồm 3 tác tử cốt lõi:

### A. Manager-Decomposer Agent (Tác tử Điều phối & Phân rã)
- **Model:** Phi-3-mini (3.8B) hoặc Llama-3-3B.
- **Nhiệm vụ:**
    - Lên kế hoạch xử lý thực thể mới.
    - Phân tách dữ liệu thô (Unstructured) thành các cặp `Attribute: Value` chuẩn.
    - Thực hiện **Semantic Schema Alignment**: Tự động ánh xạ các tên trường khác nhau (ví dụ: "Color" và "Màu sắc") về một lược đồ chung.
- **Output:** JSON chuẩn hóa của thực thể.

### B. Retriever-Matcher Agent (Tác tử Truy vấn & So khớp)
- **Model:** Llama-3-8B (hoặc model 7B-8B tương đương).
- **Nhiệm vụ:**
    - **Retrieval:** Sử dụng Vector Search (ChromaDB) để tìm danh sách ứng viên tiềm năng (Candidate Set).
    - **Reasoning Match:** Thực hiện so khớp logic 1:1 giữa thực thể đầu vào và các ứng viên.
    - **Logic:** Sử dụng trọng số thuộc tính (Attribute Weighting) để ưu tiên các thông số kỹ thuật (Model, SKU, Specs).
- **Output:** Danh sách các cặp Match tiềm năng kèm `Confidence Score` (0-1) và lý giải (Reasoning).

### C. Verifier-Critic Agent (Tác tử Kiểm chứng)
- **Model:** Llama-3-8B hoặc Mistral-7B.
- **Nhiệm vụ:**
    - **Trigger:** Kích hoạt khi `Confidence Score` nằm trong vùng nghi ngờ (ví dụ: 0.5 - 0.85).
    - **Logic:** Áp dụng mẫu thiết kế **Reflexion**. Kiểm tra các lỗi phổ biến (nhầm lẫn phiên bản đời máy, dung lượng bộ nhớ, đơn vị đo lường).
    - **Output:** Quyết định cuối cùng (Match/Non-match) hoặc yêu cầu Retriever Agent tìm kiếm lại với từ khóa khác.

---

## 3. Luồng dữ liệu (Data Flow)

1. **Input:** Một bản ghi sản phẩm mới từ Web/File.
2. **Step 1:** Manager-Decomposer chuẩn hóa dữ liệu và xác định các thuộc tính quan trọng.
3. **Step 2:** Retriever-Matcher thực hiện Vector Search tìm Top-K ứng viên.
4. **Step 3:** Retriever-Matcher thực hiện so khớp từng cặp và trả về điểm số.
5. **Step 4:** Nếu điểm thấp, Verifier-Critic tham gia phản biện để sửa lỗi.
6. **Output:** Kết quả cuối cùng được cập nhật vào Database "Golden Record".

---

## 4. Logic & Thuật toán Cốt lõi

### Cơ chế Căn chỉnh Lược đồ (Semantic Alignment)
- Sử dụng khả năng hiểu ngữ nghĩa của SLM để map dữ liệu:
    - `"0.5 TB"` &harr; `"512 GB"`
    - `"Màn hình Retina"` &harr; `"Display Type"`
    - `"prop_idx_12"` &harr; `"Brand Name"` (Dựa trên nội dung mẫu).

### Cơ chế Confidence Scoring
- **Match Tuyệt đối:** CS > 0.9 (Dựa trên SKU/Model Name chính xác).
- **Vùng Nghi ngờ:** 0.5 < CS < 0.9 (Cần Verifier can thiệp).
- **Non-match:** CS < 0.5.

---

## 5. Tính khả thi & Đánh giá (Feasibility & Evaluation)

### Tài nguyên Phần cứng (PC local)
- Sử dụng kỹ thuật **Quantization (GGUF/AWQ)** để chạy các model 8B trong khoảng 6-8GB VRAM.
- Quản lý bộ nhớ bằng cách nạp/xả model luân phiên hoặc sử dụng các framework hỗ trợ suy luận nhẹ (như Ollama, vLLM).

### Dữ liệu thử nghiệm
- Sử dụng các Benchmark nổi tiếng: **WDC Product Data**, **Magellan Datasets** (Beer Advo, iTunes-Amazon, Walmart-Amazon).

### Chỉ số đánh giá (Metrics)
- Precision, Recall, F1-Score.
- Chi phí xử lý (Token cost) và Thời gian đáp ứng (Latency) so với việc dùng GPT-4.

---

## 6. Kết luận & Đóng góp học thuật
Luận văn sẽ đóng góp một giải pháp Multi-Agent hiệu quả, thực tế, cho phép các doanh nghiệp vừa và nhỏ triển khai hệ thống Entity Matching chất lượng cao trên hạ tầng tại chỗ (On-premise) mà không phụ thuộc vào các API LLM đắt đỏ.
