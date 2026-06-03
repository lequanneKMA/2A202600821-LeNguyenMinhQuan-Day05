# Khung Thuyết Trình & Kịch Bản Demo (Dành cho PO/Presenter)

**Dự án:** Smart Bill Splitting (Chia tiền nhóm)  
**Người trình bày:** Lê Nguyễn Minh Quân  
**Thời gian dự kiến:** 3 - 5 phút  

---

## 1. Mở đầu: Bối cảnh & Nỗi đau (1 phút)
*(Mục tiêu: Đánh trúng tim đen của khán giả trong lớp)*

- **Hook (Câu mở màn):** "Ở đây có bao nhiêu bạn từng đi ăn lẩu, ăn nướng đông người, rồi lúc về phải cầm tờ hóa đơn dài ngoằng bấm máy tính chia tiền, cộng thêm cả tiền VAT và phí phục vụ?"
- **Pain Point:** Việc chia tiền thủ công hiện nay bắt người trả tiền (Host) phải làm mọi việc: Gõ lại từng món -> Chụp bill gửi group Zalo -> Gào thét hỏi xem ai ăn gì -> Tính toán rắc rối dễ mất lòng.
- **Evidence:** Bằng chứng là mọi người thà chịu thiệt vài chục nghìn hoặc chia đều (gây bất công cho người ăn ít) chứ lười xài tính năng chia tiền nhập tay hiện tại của MoMo.

## 2. Giải pháp: Build Slice (1 phút)
*(Mục tiêu: Giới thiệu giải pháp Smart Bill Splitting)*

- **Concept:** Nhóm mang đến giải pháp **Crowdsourcing Bill Splitting** (Chia tiền tương tác) bằng sức mạnh của AI.
- **AI đóng vai trò gì?** Thay vì bắt user gõ tay, AI (Vision LLM) sẽ tự động **bóc tách** tờ hóa đơn nhàu nát thành một danh sách số hóa chuẩn xác 100%.
- **Human đóng vai trò gì?** Quyền quyết định thuộc về tập thể. Host chỉ cần quăng cái Link vào group, ai ăn gì tự vào **click chọn món đó**. 

## 3. Demo Prototype (2 phút)
*(Mục tiêu: Chạy thử luồng Happy Path và xử lý Failure Path)*

### Cảnh 1: Happy Path (Mượt mà)
- **Hành động:** Demo màn hình Host chụp một tờ hóa đơn.
- **Kết quả:** Hiện ra danh sách món ăn đã được AI bóc tách (Kèm theo tiền VAT đã được tự động tách riêng).
- **Hành động:** Demo màn hình bạn bè mở Link -> Click tranh nhau nhận món -> MoMo tự tính ra số tiền mỗi người cần trả.

### Cảnh 2: Low-confidence & Failure Path (Cách AI sửa sai)
- **Tình huống:** Trong bill có món "Khăn lạnh/Gửi xe" bị AI nhận nhầm thành món ăn riêng lẻ. Hoặc có món "Combo Lẩu 4 Người".
- **Cách xử lý:** Demo việc Host có quyền **Admin (Override)**: Click vào món đó và chuyển nó thành "Phí chung chia đều" chỉ bằng 1 thao tác vuốt. 

## 4. Chốt lại (30 giây)
*(Mục tiêu: Khẳng định tính khả thi và giá trị sản phẩm)*

- **Tóm tắt giá trị:** Tính năng này giải phóng gánh nặng cho Host, biến việc đòi tiền nợ thành một trải nghiệm vui vẻ, minh bạch và không cãi vã.
- **Công nghệ cốt lõi:** Bằng việc dùng Vision LLM làm Middleware (Bóc tách) và Frontend UI làm Frontend (Tương tác), nhóm đã hoàn thiện trọn vẹn luồng Prototype chỉ trong 1 buổi sáng Hackathon!
- **Call to Action:** "Cảm ơn mọi người đã lắng nghe. Có nhóm nào muốn đi ăn lẩu để test thử App của nhóm mình ngay bây giờ không?"

---
**Ghi chú cho Quân:** Khi lên thuyết trình, hãy nói thật tự tin và mang giọng điệu của một Product Owner đang bán giải pháp (Pitching). Đừng nói quá sâu về code, hãy tập trung vào trải nghiệm người dùng (UX) và cách AI giải quyết nỗi đau đó!
