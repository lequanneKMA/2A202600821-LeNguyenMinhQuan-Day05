# Tech Spec & Execution Plan (Day 06)

**Dự án:** Smart Bill Splitting (Prototype)
**Mục tiêu:** Code siêu tốc, phân công rõ ràng cho 5 người để có sản phẩm chạy mượt trong 1 buổi sáng.

## 1. Tech Stack (Fullstack cơ bản)
- **Frontend (Web):** HTML/CSS/JS thuần hoặc React (Vite/Next.js).
- **Backend:** Node.js (Express) hoặc Next.js API Routes (hoặc Python FastAPI). Xử lý logic chia tiền, nhận request từ Web và gọi sang AI.
- **AI Layer:** Gọi API của Vision LLM (Gemini 1.5 Pro hoặc GPT-4o).

---

## 2. Phân công Task Code & Chạy dự án (5 Thành Viên)

### 👨‍💻 1. Đoàn Minh Hiếu (Dev AI)
- [ ] **Task 1:** Tinh chỉnh System Prompt cho Vision LLM. Ép LLM luôn trả về đúng format mảng `items` và `shared_fees` (thuế, khăn lạnh...).
- [ ] **Task 2:** Viết hàm call API gửi ảnh lên LLM và nhận kết quả JSON trả về.
- **Verify:** Chạy script với 1 ảnh hóa đơn, in ra đúng cục JSON hợp lệ không bị dính text thừa. Chuyển code hàm API cho Backend tích hợp.

### ⚙️ 2. Lê Nguyễn Minh Quân (Backend)
- [ ] **Task 1:** Viết API Endpoint nhận file ảnh từ Frontend, ném sang hàm của Dev AI để lấy JSON.
- [ ] **Task 2:** Viết logic tính toán chia tiền (Cộng dồn tiền món ăn cá nhân + chia đều `shared_fees`).
- [ ] **Task 3:** Tạo Endpoint trả dữ liệu hóa đơn về cho Frontend hiển thị.
- **Verify:** Frontend gọi API `/upload-bill` và nhận về JSON danh sách món thành công.

### 🎨 3. Phạm Hoàng Anh (Dev Web / Frontend)
- [ ] **Task 1:** Code UI Màn hình 1 (Upload Bill & Loading).
- [ ] **Task 2:** Code UI Màn hình 2 (Danh sách món trả về từ Backend).
- [ ] **Task 3:** Code UI Màn hình 3 (Luồng Crowdsourcing: Bạn bè click tick chọn món, tính tổng tiền hiển thị trên giao diện).
- **Verify:** 2 người cùng click vào 1 món trên Màn hình 3 thì giao diện báo số tiền tự chia đôi.

### 🕵️‍♂️ 4. Nguyễn Dương Hiếu (Research & Test)
- [ ] **Task 1:** Thu thập Evidence, hoàn thiện Slide Deck và các file Spec nộp bài.
- [ ] **Task 2:** Chuẩn bị Data hóa đơn thực tế (Bill mờ, bill nhăn, bill có Discount).
- [ ] **Task 3:** Test độ khôn của Prompt AI (Đoàn Minh Hiếu) bằng các ảnh hóa đơn khó.
- **Verify:** Slide nộp bài hoàn chỉnh, Prompt AI vượt qua được bài test hóa đơn mờ.

### 🕵️‍♂️ 5. Nguyễn Văn Minh (Research & Test)
- [ ] **Task 1:** Đóng vai User (Bạn bè) để test chéo luồng UI của Hoàng Anh và logic tính toán của Quân (Backend).
- [ ] **Task 2:** Test các Failure Mode: Click nhầm món, bỏ chọn món, tổng tiền chia ra bị lẻ.
- [ ] **Task 3:** Hỗ trợ chuẩn bị kịch bản Q&A (Nghiên cứu đối thủ Splitwise) để phản biện.
- **Verify:** Giao diện Web không bị crash khi user spam click chọn món, Backend tính tiền chuẩn từng đồng.

---

## 3. Quy trình ráp nối (Integration Pipeline)
1. **8h00 - 9h30:** Minh Hiếu chốt Prompt AI. Hoàng Anh lên khung Web tĩnh. Quân dựng xong sườn Backend.
2. **9h30 - 10h30:** Ráp nối 3 bên: Web (Hoàng Anh) gửi ảnh -> Backend (Quân) -> AI (Minh Hiếu).
3. **10h30 - 11h00:** Dương Hiếu và Văn Minh cầm Data vào test toàn bộ hệ thống, báo Bug cho 3 Dev sửa gấp.
4. **11h00 - 11h30:** Chốt code, hoàn thiện Slide và chuẩn bị nộp bài.

## ✅ Done When
- [ ] Tích xanh tất cả các checklist phía trên.
- [ ] Prototype chạy thông suốt từ lúc upload ảnh đến lúc ra màn hình chia tiền tổng.
