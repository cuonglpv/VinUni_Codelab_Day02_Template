# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| **1** | **Xanh SM**               | Repetitive + Stakeholder Pain | **Phân loại nguyên nhân chuyến hủy / không hoàn thành** từ dữ liệu chuyến, ghi chú tài xế, chat/call để biết chính xác vì sao chuyến thất bại. |
| **2** | **Vinhomes**              | Repetitive + Time-consuming   | **Tự động phân loại và chuyển ticket cư dân**: điện, nước, thang máy, vệ sinh, an ninh, phí dịch vụ… → đúng bộ phận xử lý.                     |
| **3** | **VinFast**               | Repetitive + Time-consuming   | **Triage lỗi bảo hành/sửa chữa**: đọc mô tả lỗi + error code + lịch sử xe → phân nhóm lỗi và gợi ý hướng kiểm tra ban đầu.                     |
| **4** | **Vinpearl / VinWonders** | Repetitive + AI-upgrade       | **Tự động xử lý câu hỏi khách hàng** về vé, phòng, voucher, giờ hoạt động, đổi lịch, tiện ích… thay cho CSKH trả lời từng câu giống nhau.      |
| **5** | **Vinhomes**              | Repetitive + Stakeholder Pain | **Phát hiện bất thường điện/nước**: hệ thống tự phát hiện tòa nhà/khu vực tiêu thụ bất thường để đội vận hành kiểm tra trước khi có khiếu nại. |



---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                          │
│                                                               │
│ Bài toán (1 câu):                                            │
│ Tự động gắn nhãn lý do hủy chuyến từ ghi chú text của        │
│ tài xế/CS sau mỗi cuộc gọi hủy, theo taxonomy cố định.       │
│                                                               │
│ Công ty thành viên: [ ] VinFast  [✓] Xanh SM  [ ] Vinhomes   │
│                      [ ] Vinmec                              │
│                                                               │
│ Ai đang đau (Actor)?                                         │
│ Customer Operations                                          │
│                                                               │
│ Workflow thủ công hiện tại:                                  │
│ 1. Khách/tài xế hủy chuyến, CS ghi chú lý do bằng text       │
│    → 2. Ghi chú lưu vào hệ thống                             │
│    → 3. CS/vận hành đọc và phân loại lý do thủ công          │
│    → 4. Tổng hợp báo cáo pattern hủy chuyến định kỳ          │
│                                                               │
│ Bước nào tốn thời gian/lỗi nhất?                             │
│ Bước 3: đọc và phân loại ghi chú text không cấu trúc         │
│ (⏱ giả định 3–5 phút/case, cần validate bằng log)            │
│                                                               │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                        │
│ Bước 3: gắn 1 nhãn lý do hủy (taxonomy cố định 10–15 nhãn)   │
│ + confidence score cho mỗi ghi chú text đã có sẵn (không     │
│ xử lý audio call trực tiếp). Confidence thấp → route người.  │
│                                                               │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Accuracy theo từng nhãn ≥85% (đo trên tập test gán tay       │
│ ≥200 case); giảm thời gian phân loại/case từ 3–5 phút        │
│ xuống <30 giây (tính từ lúc có ghi chú text).                │
│                                                               │
│ Quick Architecture: [ ] No AI [ ] Rule [✓] LLM [ ] Agent     │
│ (MVP; cân nhắc chuyển sang classifier nhẹ nếu volume đủ lớn) │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu):                                           │
│ Tự động phân loại ticket free-text (hotline/ô mô tả tự do)  │
│ đến đúng đội kỹ thuật phụ trách, loại trừ ticket đã có      │
│ category sẵn hoặc liên quan pháp lý/tài chính.              │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [✓] Vinhomes  │
│                      [ ] Vinmec                              │
│                                                              │
│ Ai đang đau (Actor)?                                         │
│ Customer Service (owner nhãn) — Đội vận hành/kỹ thuật        │
│ (bên nhận kết quả)                                           │
│                                                              │
│ Workflow thủ công hiện tại:                                  │
│ 1. Tiếp nhận ticket free-text từ hotline/app                 │
│    → 2. CS đọc nội dung phản ánh                             │
│    → 3. CS xác định nhóm vấn đề và đội phụ trách             │
│    → 4. Chuyển ticket đến đội kỹ thuật tương ứng             │
│                                                              │
│ Bước nào tốn thời gian/lỗi nhất?                             │
│ Bước 3: đọc và phân loại ticket free-text                    │
│ (⏱ giả định 1–3 phút/ticket, cần validate bằng log)         │
│                                                              │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                        │
│ Bước 3: phân loại ticket vào taxonomy hiện có của BQL +      │
│ đề xuất đội phụ trách + confidence score. Ticket pháp lý/    │
│ tài chính hoặc confidence thấp → route thẳng người.          │
│                                                               │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Accuracy theo từng nhóm ≥90% (đo trên tập test gán tay       │
│ ≥200 ticket); giảm thời gian triage/ticket từ 1–3 phút       │
│ xuống <10 giây.                                              │
│                                                               │
│ Quick Architecture: [ ] No AI [✓] Rule+LLM [ ] Agent         │
│ (rule-based cho nhóm có từ khóa rõ ràng, VD "cháy nổ",       │
│ "mất nước"; LLM cho phần còn lại)                            │
└─────────────────────────────────────────────────────────────┘
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu):                                            │
│ Dựa trên mô tả lỗi tự nhiên của khách hàng + error code      │
│ (nếu có), gợi ý top-3 nhóm lỗi khả dĩ nhất kèm % tin cậy    │
│ cho Service Advisor        │
│                                                               │
│ Công ty thành viên: [✓] VinFast  [ ] Xanh SM  [ ] Vinhomes   │
│                      [ ] Vinmec                              │
│                                                               │
│ Ai đang đau (Actor)?                                         │
│ Service Advisor tại trung tâm dịch vụ                        │
│                                                               │
│ Workflow thủ công hiện tại:                                  │
│ 1. Tiếp nhận mô tả lỗi từ khách hàng                         │
│    → 2. Kiểm tra error code (nếu có)                         │
│    → 3. SA tổng hợp thông tin, xác định nhóm lỗi ban đầu     │
│    → 4. Chuyển kỹ thuật viên kiểm tra theo nhóm lỗi          │
│                                                               │
│ Bước nào tốn thời gian/lỗi nhất?                             │
│ Bước 3: tổng hợp mô tả lỗi + error code để xác định nhóm     │
│ lỗi ban đầu (⏱ cần validate bằng log thực tế)                │
│                                                               │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                        │
│ Bước 3: kết hợp mô tả lỗi (free text) + error code, gợi ý    │
│ top-3 nhóm lỗi khả dĩ nhất kèm % tin cậy. SA xác nhận cuối.  │
│ Lịch sử sửa chữa xe: chưa đưa vào MVP đầu (thêm sau).        │
│                                                               │
│ Đo thành công bằng gì (Metric có số)?                        │
│ Top-3 hit rate ≥85% (đo trên tập test gán tay ≥150 case);   │
│ giảm thời gian triage ban đầu của SA ≥30% (hạ từ ≥50% vì    │
│ đây là công cụ hỗ trợ, không thay bước xác nhận của người). │
│                                                               │
│ Quick Architecture: [ ] No AI [ ] Rule [✓] LLM [ ] Agent     │
│ (dạng suggestion/gợi ý, không tự động hành động)             │
└─────────────────────────────────────────────────────────────┘

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Ai đang thực hiện tác vụ hằng ngày? |
| **2. Current Workflow** | Mô tả tóm tắt quy trình thủ công hiện tại và công cụ sử dụng. |
| **3. Bottleneck** | Bước nào chậm, lỗi, hoặc cần xử lý ngôn ngữ tự động nhiều nhất? |
| **4. Business Impact** | Tổn thất thực tế đo bằng thời gian, chi phí, hoặc SLA của Vingroup. |
| **5. Success Metric** | AI giải quyết được thì đạt ngưỡng số mấy? (Ví dụ: *"85% vé được phân loại dưới 10s"*). |
| **6. Operational Boundary** | AI được phép làm gì, TUYỆT ĐỐI không được làm gì, điểm nào cần duyệt? |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Viết lý giải chi tiết tại đây*

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
