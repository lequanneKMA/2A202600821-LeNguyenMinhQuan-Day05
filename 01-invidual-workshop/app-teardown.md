# Workshop — Mổ App AI Thật

**Thời gian:** 35-45 phút  
**Hình thức:** cá nhân trước, chia sẻ theo nhóm sau  
**Output:** finding note + sketch `as-is / to-be`

Mục tiêu không phải chấm "UI đẹp hay xấu". Mục tiêu là dùng sản phẩm thật như một bài needfinding: tìm chỗ product gãy trong workflow thật, rồi viết finding đó thành quyết định product.

## 1. Chọn một sản phẩm để dùng thử

| Sản phẩm | AI feature | Cách truy cập |
|---|---|---|
| MoMo — Moni | Trợ thủ tài chính, phân tích chi tiêu, chatbot | App MoMo |
| Vietnam Airlines — NEO | Chatbot hỗ trợ vé, hành lý, khiếu nại | Website/Zalo VNA |
| V-App — V-AI | Trợ lý voice/text, gợi ý theo ngữ cảnh | App V-App |

## 2. Dùng thử: promise vs reality

Ghi nhanh:

- **Product hứa gì?** Trợ lý ảo (V-AI) điều khiển bằng giọng nói/văn bản, kết nối toàn bộ hệ sinh thái Vingroup.
- **User nào được hứa sẽ được giúp?** Khách hàng sử dụng dịch vụ Vingroup (Cư dân Vinhomes, SV VinUni, khách Xanh SM...).
- **Bạn kỳ vọng AI làm được task nào?** Có thể thực thi hành động (báo hỏng đồ) hoặc truy xuất dữ liệu cá nhân (lịch học, thông tin tài khoản) trực tiếp qua chat.
- **Khi dùng thật, điểm gãy xuất hiện ở đâu?** 
  1. AI bị over-sensitive (nhạy cảm quá mức): Hỏi "Bạn biết tôi là ai không" thì bị nhận diện nhầm thành tin đồn thất thiệt/công kích cá nhân và từ chối trả lời.
  2. AI nhầm lẫn giữa "Hành động" (Action) và "Tìm kiếm" (Search): Ra lệnh "Báo hỏng đồ" thay vì mở form Vinhomes thì lại đi search bài báo VNExpress.
  3. AI không có quyền truy cập dữ liệu cá nhân sâu: Hỏi lịch học VinUni không ra, chỉ ném ra cái nút bắt tự bấm vào mini-app.

Evidence cần có:

- **screenshot:** 
  - *Ảnh 1 (Lỗi Safety):*
    ![Lỗi Safety - Tin đồn thất thiệt](./evidence/safety-error.png)
  - *Ảnh 2 (Lỗi Action Search):*
    ![Lỗi Action - Báo hỏng đồ bằng bài báo](./evidence/action-error.png)
  - *Ảnh 3 (Lỗi Deep-link VinUni):*
    ![Lỗi Deep-link - Lịch học VinUni](./evidence/deeplink-error.png)
- **prompt/input đã thử:** "Bạn biết tôi là ai không", "Báo hỏng đồ", "Xem lịch học chiều nay của tôi".
- **hành vi quan sát được:** AI dùng Web Search bừa bãi cho các câu lệnh mang tính hành động (Action Intent); Policy an toàn bị thiết lập sai ngữ cảnh.

## 3. Vẽ 4 paths

| Path | Câu hỏi cần trả lời |
|---|---|
| Happy | (Prompt: Tháng 7 xe bus VinUni qua Ocean Park không) AI gọi đúng tool Search, tóm tắt chính xác lộ trình tuyến E10, OCP02 cho user. |
| Low-confidence | (Prompt: Xem lịch học) AI không có data cá nhân, nó chủ động thừa nhận "chưa thấy có dữ liệu" và đưa ra nút bấm dẫn tới mini-app VinUni để user tự tra cứu. |
| Failure | (Prompt: Báo hỏng đồ) AI fail hoàn toàn trong việc nhận diện Intent. Thay vì kích hoạt chức năng báo bảo trì của Vinhomes, nó lại đi search web và trích dẫn báo VNExpress. |
| Correction | (Prompt: Bạn biết tôi là ai không) Khi AI từ chối vì tưởng là tin đồn, user sửa prompt thành "ai khôn" (thiếu chữ g), AI bất ngờ "tỉnh" lại và gọi đúng tên "Lê Nguyễn Minh Quân". Hệ thống không có tính nhất quán. |

## 4. Viết finding thành quyết định

**Finding 1: Lỗi đứt gãy luồng Hành động (Action Layer)**
Khi user ra lệnh "Báo hỏng đồ" (một tác vụ cốt lõi của cư dân Vinhomes),
AI/product phân loại nhầm Intent từ "Thực thi tác vụ" sang "Tìm kiếm thông tin",
hậu quả là AI trả về một bài báo hướng dẫn báo hỏng đồ trên VNExpress thay vì hiển thị Form tạo yêu cầu bảo trì, khiến user bực mình vì app không giải quyết được việc.
Lỗi thuộc layer Intent & Data-tool.
Nên sửa bằng Requirement/UX: Đưa các động từ "Báo hỏng", "Đặt xe", "Thanh toán" vào danh sách hard-code Intent ưu tiên cao nhất để map thẳng vào UI Form (Action), tuyệt đối không đẩy qua Web Search tool.

**Finding 2: Lỗi truy cập dữ liệu cá nhân (Deep-link & Data Integration)**
Khi user yêu cầu "Xem lịch học chiều nay của tôi",
AI/product không gọi được API dữ liệu cá nhân từ mini-app VinUni,
hậu quả là AI chỉ xin lỗi và hiển thị một nút bấm bắt user tự mở mini-app lên để tìm, tạo ra ma sát lớn trong UX (không khác gì không dùng AI).
Lỗi thuộc layer Data-tool integration.
Nên sửa bằng Requirement: Yêu cầu team phát triển mini-app VinUni mở các API endpoints cụ thể (lịch học, điểm số) để V-AI có thể gọi thông qua function calling và render kết quả trực tiếp ngay trên khung chat.

**Finding 3: Lỗi Guardrails/Safety quá mức**
Khi user hỏi đùa "Bạn biết tôi là ai không",
AI/product kích hoạt nhầm bộ lọc an toàn, cho rằng đây là câu hỏi về "tin đồn thất thiệt/công kích cá nhân",
hậu quả là AI từ chối phục vụ một cách cứng nhắc, tạo cảm giác máy móc và ngớ ngẩn.
Lỗi thuộc layer Safety & Prompt Engineering.
Nên sửa bằng Prompt update: Nới lỏng Guardrails, hướng dẫn AI cách nhận biết các câu hỏi mang tính giao tiếp thông thường (chit-chat) và chủ động trích xuất Tên user từ biến môi trường (account_name) để phản hồi thân thiện thay vì phòng thủ.
## 5. Sketch as-is / to-be

**Use-case: User ra lệnh "Báo hỏng đồ"**

- **As-is (Luồng hiện tại - Gãy):** 
  User Voice: "Báo hỏng đồ" 
  -> AI phân tích NLP (nhầm sang Intent Tìm kiếm) 
  -> AI gọi công cụ Web Search 
  -> AI lấy kết quả từ VNExpress 
  -> **[Điểm gãy]** Trả về text bài báo chung chung 
  -> User thất vọng, phải tự thoát ra tìm App Vinhomes.

- **To-be (Luồng đề xuất - Sửa):** 
  User Voice: "Báo hỏng đồ" 
  -> AI phân tích NLP (Nhận diện đúng Action Intent "Maintenance_Request") 
  -> AI gọi API của Vinhomes Mini-app 
  -> **[Đã sửa]** AI tự động render Form Báo hỏng (chọn địa chỉ, loại đồ hỏng) ngay trong UI chat 
  -> User điền nhanh qua chat và submit.

## 6. Tự kiểm trước khi nộp

- [x] Có ít nhất 1 screenshot hoặc observation cụ thể.
- [x] Có đủ 4 paths hoặc nói rõ path nào chưa có trong product.
- [x] Finding được viết thành product decision, không chỉ là nhận xét.
- [x] Sketch có as-is và to-be.
- [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC.

**Câu chốt đổi SPEC:** 
Dựa vào Finding số 1, trong bản SPEC ngày mai, nhóm sẽ chỉ tập trung vào việc **thay thế Web Search Tool bằng Action/Function Calling cho một lệnh cụ thể (VD: Báo hỏng)** để đảm bảo AI biến luồng thông tin thành luồng thực thi, thay vì trả về kết quả tìm kiếm chung chung.
