# Individual Reflection — 2A202600035 — Đinh Văn Thư

## 1. Role

UX Researcher + Data Crawler. Phụ trách thiết kế use case và user flow cho chatbot hỗ trợ tài xế/khách hàng trên XanhSM, đồng thời thu thập dữ liệu chính sách và điều khoản thực tế từ nền tảng.

---

## 2. Đóng góp cụ thể

- **Crawl và xử lý dữ liệu:** Thu thập nội dung điều khoản, chính sách và quy trình từ trang XanhSM, làm sạch và chuẩn hóa thành file `ĐIỀU KHOẢN CHUNG HỢP ĐỒNG DỊCH VỤ.txt` — đây là nguồn knowledge base chính cho chatbot.
- **Thiết kế user flow:** Xây dựng file `user-flow-prompt.md` mô tả các luồng tương tác chính của tài xế và khách hàng với chatbot (đăng ký tài xế, tra cứu chính sách, hỗ trợ chuyến đi...), bao gồm cả happy path và edge case.
- **Phân tích use case:** Xác định 3–4 tình huống người dùng thực tế (tài xế hỏi về quy trình đăng ký, khách hàng hỏi về giá, tài xế hỏi chính sách thưởng phạt) để làm nền cho user stories trong SPEC.

---

## 3. SPEC mạnh/yếu

**Mạnh nhất: User Stories 4 paths** — Vì đã có user flow cụ thể từ trước, phần này xây dựng được scenario thực tế, không bị chung chung. Đặc biệt path "failure" và "low-confidence" được mô tả rõ: chatbot không tìm thấy câu trả lời trong điều khoản → fallback hướng dẫn gọi hotline.

**Yếu nhất: Problem-solution fit** — Nhóm ban đầu định cover cả vấn đề tài xế lẫn khách hàng trong cùng một chatbot, khiến bài toán quá rộng. Phản hồi từ demo cũng chỉ ra đúng điểm này. Nên chọn một persona chính ngay từ đầu thay vì để scope mở.

---

## 4. Đóng góp khác

- Hỗ trợ nhóm kiểm tra lại tính nhất quán giữa data crawl và câu trả lời của chatbot — phát hiện 2 trường hợp chatbot trả lời không khớp với điều khoản thực tế trong file `.txt`.
- Đề xuất cấu trúc prompt system theo từng persona (tài xế / khách hàng) thay vì dùng chung một prompt, giúp câu trả lời cụ thể và đúng ngữ cảnh hơn.

---

## 5. Điều học được

Trước hackathon, tôi nghĩ crawl dữ liệu chỉ là bước kỹ thuật — lấy được text là xong. Sau khi làm thực tế mới hiểu: **chất lượng dữ liệu quyết định chất lượng câu trả lời của AI**. Điều khoản XanhSM viết theo văn phong pháp lý, dài và lặp — nếu đưa thẳng vào mà không làm sạch, chatbot sẽ trả lời vòng vo hoặc lấy sai đoạn. Xử lý dữ liệu đầu vào là product decision, không chỉ là data engineering.

---

## 6. Nếu làm lại

Sẽ xác định **một bài toán duy nhất và một persona duy nhất** ngay từ buổi sáng — ví dụ chỉ tập trung vào tài xế mới đăng ký. Thay vì crawl toàn bộ trang, sẽ chọn lọc đúng 3–5 chủ đề trọng tâm (đăng ký, chính sách thưởng, xử lý khiếu nại) rồi test chatbot ngay trên tập nhỏ đó. Việc scope rộng từ đầu khiến cả nhóm mất nhiều thời gian xử lý data và thiết kế flow mà không đủ thời gian iterate prompt.

---

## 7. AI giúp gì / AI sai gì

**Giúp:**

- Dùng Claude để đọc và tóm tắt điều khoản dài, trích xuất các điểm chính theo từng chủ đề (quyền lợi, nghĩa vụ, chấm dứt hợp đồng...) — tiết kiệm được khoảng 1–2 giờ đọc thủ công.
- Dùng AI để generate draft user flow từ mô tả bài toán, sau đó chỉnh tay lại — nhanh hơn làm từ đầu khoảng 3 lần.

**Sai/mislead:**

- Claude đôi khi "sáng tạo" thêm các bước trong user flow mà thực tế app XanhSM không có (ví dụ: bước "xác nhận OTP 2 lần"), khiến flow không khớp với sản phẩm thực. Phải kiểm tra lại từng bước với app thật.
- Khi hỏi AI về cách tổ chức knowledge base, nó gợi ý dùng vector database và RAG pipeline — đúng về mặt kỹ thuật nhưng quá phức tạp cho hackathon 1 ngày. Bài học: AI không tự biết giới hạn thời gian và resource của bạn, cần tự filter gợi ý theo context thực tế.
