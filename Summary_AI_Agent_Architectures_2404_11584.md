# Tóm tắt bài báo: The Landscape of Emerging AI Agent Architectures

## Thông tin trích dẫn
Masterman, T., Besen, S., Sawtell, M., & Chao, A. (2024). *The Landscape of Emerging AI Agent Architectures for Reasoning, Planning, and Tool Calling: A Survey*. arXiv preprint arXiv:2404.11584. [https://arxiv.org/abs/2404.11584](https://arxiv.org/abs/2404.11584)

## 1. Câu hỏi nghiên cứu & Mục tiêu
Nghiên cứu khảo sát bối cảnh hiện tại của các triển khai tác tử AI (AI agent), tập trung vào cách các kiến trúc khác nhau (đơn tác tử so với đa tác tử) đạt được các mục tiêu phức tạp thông qua suy luận, lập kế hoạch và thực thi công cụ. Mục tiêu là xác định các khả năng cốt lõi, hạn chế và các mẫu thiết kế chính cho các hệ thống tự trị mạnh mẽ.

## 2. Phương pháp nghiên cứu
- **Thiết kế**: Khảo sát và phân tích toàn diện các tài liệu và khung (framework) hiện có.
- **Dữ liệu/Khung được phân tích**:
  - **Đơn tác tử (Single-Agent)**: ReAct, RAISE, Reflexion, AutoGPT+P, LATS.
  - **Đa tác tử (Multi-Agent)**: Embodied LLM Agents, DyLAN, AgentVerse, MetaGPT.
- **Phân tích**: Xác định các chủ đề chính trong lựa chọn kiến trúc, phong cách giao tiếp, cấu trúc lãnh đạo và tác động của chúng đối với thành công của nhiệm vụ.

## 3. Kết quả chính
1. **Đơn tác tử vs. Đa tác tử**: Đơn tác tử tốt nhất cho các nhiệm vụ xác định rõ với tập công cụ hạn chế. Hệ thống đa tác tử vượt trội trong các kịch bản cần cộng tác, thực thi song song và nhiều vai trò (persona), nhưng dễ gặp vấn đề "giao tiếp thừa" (superfluous chatter).
2. **Tác động của Lãnh đạo**: Các "tác tử dẫn dắt" (lead agents) trong cấu trúc đa tác tử cải thiện hiệu quả thêm 10% bằng cách hợp nhất giao tiếp (dành 60% thời gian đưa ra chỉ dẫn thay vì chỉ chia sẻ thông tin).
3. **Lập kế hoạch & Phản hồi**: Các tác tử thành công sử dụng vòng lặp "Lập kế hoạch - Thực thi - Đánh giá". Các kỹ thuật như LATS và Reflexion giúp giảm đáng kể ảo tưởng và cải thiện quỹ đạo giải quyết vấn đề.
4. **Quản lý giao tiếp**: Kiến trúc ngang hàng có thể bị nhiễu; kiến trúc dọc và cơ chế như "publish-subscribe" (MetaGPT) cải thiện luồng thông tin bằng cách lọc dữ liệu không liên quan.

## 4. Ý nghĩa nghiên cứu
Khảo sát này cung cấp một hệ thống phân loại (taxonomy) quan trọng cho thế hệ ứng dụng AI tiếp theo, tiến xa hơn mô hình RAG đơn giản. Nó phác thảo các nguyên tắc nền tảng để người phát triển quyết định giữa các mẫu kiến trúc dựa trên yêu cầu nhiệm vụ.

## 5. Hạn chế
- **Bộ dữ liệu đánh giá (Benchmarks)**: Hầu hết các bộ đánh giá hiện tại là tĩnh, không theo kịp khả năng tiến hóa của tác tử và có nguy cơ nhiễm dữ liệu huấn luyện.
- **Độ tin cậy & Định kiến**: Tác tử thường biểu hiện hành vi "nịnh nọt" (sycophancy) và kế thừa/khuếch đại các định kiến xã hội từ mô hình ngôn ngữ gốc (LLM).
- **Khả năng chuyển đổi thực tế**: Thành công trên các câu đố logic hoặc trò chơi điện tử không phải lúc nào cũng chuyển thành hiệu suất trên dữ liệu thực tế bị nhiễu.

## 6. Hướng nghiên cứu tương lai
- Phát triển các **benchmark động** có khả năng chống ghi nhớ.
- Triển khai **kiểm chứng có con người tham gia (human-in-the-loop)** mạnh mẽ hơn để giảm thiểu định kiến.
- Khám phá các **kiến trúc lai (hybrid architectures)** kết hợp giữa sự tập trung của đơn tác tử và sức mạnh cộng tác của đa tác tử.

## Ghi chú cá nhân
Bài báo này đặc biệt hữu ích cho việc chuyển đổi từ kỹ thuật nhắc (prompt engineering) sang **quy trình làm việc theo hướng tác tử (agentic workflows)**. Sự phân biệt giữa cấu trúc lãnh đạo dọc và ngang là bài học then chốt để thiết kế các hệ thống tác tử doanh nghiệp có khả năng mở rộng.
