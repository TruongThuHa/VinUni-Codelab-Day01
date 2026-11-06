# Day 01 — Bài tập & Phản ánh: Nền tảng LLM API

## Bài tập 2.1 — Độ nhạy của Temperature
Prompt: **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."** với temperature 0.0, 0.5, 1.0, 1.5.

**Quy luật qua bốn phản hồi:**
> Temperature càng thấp thì câu trả lời càng ổn định và an toàn: ở 0.0 model gần như luôn chọn từ có xác suất cao nhất nên chạy lại vẫn ra cùng một "sự thật" quen thuộc. Khi tăng lên 1.0–1.5, model chọn cả những từ ít khả năng hơn, nên câu trả lời đa dạng và sáng tạo hơn, nhưng cũng dễ lan man hoặc đưa ra chi tiết thiếu chính xác.

**Temperature cho chatbot hỗ trợ khách hàng:**
> Khoảng 0.2–0.3. Chatbot hỗ trợ khách hàng cần trả lời nhất quán, đúng chính sách và ít "bịa"; vẫn giữ một chút ngẫu nhiên để câu trả lời không quá máy móc.

---

## Bài tập 2.2 — Đánh đổi chi phí
Kịch bản: 10.000 người dùng/ngày × 3 lần gọi × ~350 token = **10,5 triệu token/ngày**.

**`gpt-4o` đắt hơn `gpt-4o-mini` bao nhiêu lần?**
> Theo bảng giá trong template: gpt-4o $5.00 / $20.00, gpt-4o-mini $0.15 / $0.60 mỗi 1M token (input / output). Tỉ lệ giá input là 5 / 0.15 ≈ 33,3 lần và tỉ lệ giá output là 20 / 0.6 ≈ 33,3 lần, nên dù chia input/output thế nào thì **gpt-4o đắt hơn khoảng 33 lần**. Ví dụ nếu cả 350 token là input: gpt-4o ≈ 10,5 × $5 = $52,5/ngày, gpt-4o-mini ≈ 10,5 × $0.15 ≈ $1,58/ngày.

**Khi nào gpt-4o xứng đáng, khi nào gpt-4o-mini tốt hơn:**
> gpt-4o xứng đáng với tác vụ ít lượt nhưng cần chất lượng cao, sai thì tốn kém: phân tích hợp đồng, suy luận nhiều bước, viết code phức tạp. gpt-4o-mini tốt hơn cho tác vụ đơn giản và số lượng lớn như phân loại tin nhắn, trích xuất thông tin, trả lời FAQ — chất lượng đủ dùng mà chi phí rẻ hơn khoảng 33 lần.

---

## Bài tập 2.3 — Trải nghiệm người dùng với Streaming
> Streaming quan trọng nhất khi người dùng đang chờ trực tiếp một câu trả lời dài, như chatbot hay trợ lý viết: chữ hiện ra dần giúp người dùng thấy phản hồi gần như ngay lập tức thay vì nhìn màn hình trống vài giây, nên cảm giác nhanh hơn dù tổng thời gian không đổi. Non-streaming phù hợp hơn khi kết quả được xử lý tiếp bằng code chứ không cho người đọc ngay — ví dụ cần JSON hoàn chỉnh để parse, phân loại hàng loạt, chạy batch hay job nền — vì lúc đó phải có toàn bộ câu trả lời mới dùng được, và code cũng đơn giản hơn.
