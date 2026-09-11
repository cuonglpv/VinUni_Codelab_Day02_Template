# 01 — Problem Scan & Quick Cards (Cá nhân)

**Học viên:** Nguyễn Vũ Huy — **MSSV:** 2A202602662 — **Branch:** `2A202602662_NguyenVuHuy`
**Vai trò:** AI Product Engineer @ Vin Smart Future

> Lưu ý: Các con số thời gian/chi phí trong file này là **ước tính giả định** để phục vụ scoping, chưa được xác thực bằng dữ liệu vận hành thật của Vingroup.

---

# 🔍 Phase 1 — SCAN: Danh sách bài toán (4 Lenses)

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Vinhomes** | Lặp lại | Ban Quản Lý (BQL) tòa nhà đọc thủ công ~150–300 phản ánh/ngày trên app Vinhomes Resident (mất nước, hỏng thang máy, ồn, xe lạ đỗ sai…), rồi **gõ tay** phân loại + chuyển ticket cho đúng tổ (Kỹ thuật / An ninh / Vệ sinh / Kế toán). |
| 2 | **VinFast** | AI có thể tốt hơn | Tổng đài CSKH nhận mô tả lỗi xe bằng tiếng Việt đời thường ("đi qua gờ kêu cụp cụp bánh trước") và phải đoán mã lỗi sơ bộ để đặt lịch xưởng → nhiều lịch đặt sai chuyên môn kỹ thuật viên. |
| 3 | **Xanh SM** | Pain từ người khác | Tài xế phàn nàn app gợi ý điểm đón sai (ngõ cụt, đường một chiều); điều phối viên phải đọc chat tài xế + GPS để sửa thủ công từng cuốc. |
| 4 | **Vinmec** | Tốn thời gian | Bác sĩ mất 20–30 phút/bệnh nhân để viết tóm tắt xuất viện từ bệnh án điện tử, xét nghiệm và ghi chú; đây là phần việc bị than phiền nhiều nhất cuối ca. |
| 5 | **Vinpearl** | Pain từ người khác | Quản lý khách sạn phải quét review trên Booking/Agoda/Google Maps mỗi sáng để lọc phàn nàn khẩn cấp ("phòng bẩn", "mất đồ") → phản hồi chậm 24–48h, mất điểm rating. |
| 6 | **VinFast** | Lặp lại | Kế toán đối chiếu hàng nghìn dòng hóa đơn sạc từ trụ sạc đối tác với log hệ thống mỗi tuần; lệch số phải tra tay từng dòng. |

---

# 🃏 Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

Chọn top 3: **#1 (Vinhomes — phân loại phản ánh cư dân)**, **#2 (VinFast — chẩn đoán lỗi từ mô tả)**, **#5 (Vinpearl — lọc review khẩn cấp)**.

## Card #1 — Vinhomes: Phân loại & điều hướng phản ánh cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): BQL tòa nhà phân loại & chuyển thủ công   │
│ hàng trăm phản ánh/ngày từ app Vinhomes Resident, gây chậm  │
│ phản hồi và chuyển nhầm bộ phận.                            │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên trực BQL (CSKH tòa nhà);     │
│ cư dân chờ phản hồi; tổ kỹ thuật nhận nhầm ticket.          │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Cư dân gửi phản ánh (text + ảnh) trên app              │
│   ──> 2. Nhân viên BQL đọc, hiểu nội dung                   │
│   ──> 3. Gõ tay: chọn loại sự cố + mức ưu tiên + tổ xử lý   │
│   ──> 4. Soạn tin phản hồi ban đầu cho cư dân               │
│   ──> 5. Tổ xử lý nhận ticket, phản hồi lại nếu sai tổ       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3–4 (⏱ ~6 phút/lượt)  │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3 (đề xuất       │
│ category/priority/tổ) + Bước 4 (draft phản hồi)             │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   - Thời gian xử lý 1 phản ánh: 6 phút ──> dưới 1.5 phút    │
│   - Tỉ lệ chuyển đúng tổ ngay lần đầu: ~80% ──> ≥ 95%       │
│   - Phản ánh khẩn (cháy/ngập/thang máy kẹt) được gắn cờ     │
│     trong < 60 giây: 100%                                   │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

## Card #2 — VinFast: Chẩn đoán lỗi xe sơ bộ từ mô tả tiếng Việt

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Tổng đài CSKH VinFast phải "dịch" mô tả   │
│ lỗi đời thường của khách thành nhóm lỗi kỹ thuật để đặt     │
│ lịch xưởng đúng chuyên môn.                                 │
│ Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác                   │
│                                                             │
│ Ai đang đau (Actor)? Tổng đài viên (không có nền kỹ thuật); │
│ kỹ thuật viên xưởng nhận lịch sai nhóm; khách phải quay lại.│
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách gọi/chat mô tả triệu chứng                       │
│   ──> 2. Tổng đài viên hỏi thêm theo checklist giấy         │
│   ──> 3. Tự đoán nhóm lỗi (gầm/điện/pin/phần mềm)           │
│   ──> 4. Đặt lịch xưởng + ghi chú tự do cho kỹ thuật viên   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ ~8 phút/cuộc,    │
│ ước tính ~25% đặt sai nhóm lỗi)                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3: gợi ý câu   │
│ hỏi làm rõ + đề xuất nhóm lỗi & mức khẩn (draft)            │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   - Tỉ lệ đặt đúng nhóm lỗi ngay lần đầu: 75% ──> ≥ 90%     │
│   - Thời gian cuộc gọi: 12 phút ──> dưới 7 phút             │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

## Card #3 — Vinpearl: Lọc review khẩn cấp đa nền tảng

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Quản lý khách sạn Vinpearl phải đọc tay   │
│ review từ 3–4 nền tảng mỗi sáng để tìm phàn nàn khẩn cấp,   │
│ dẫn tới phản hồi chậm và tụt rating.                        │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [x] Khác: Vinpearl         │
│                                                             │
│ Ai đang đau (Actor)? Front Office Manager; khách hàng chờ   │
│ phản hồi; đội Housekeeping bị phát hiện lỗi muộn.           │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Mở lần lượt Booking / Agoda / Google Maps              │
│   ──> 2. Đọc từng review mới (30–80 review/ngày/cơ sở)      │
│   ──> 3. Đánh dấu review "cần xử lý gấp" vào Excel          │
│   ──> 4. Soạn phản hồi công khai + giao việc nội bộ         │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3 (⏱ ~45 phút/ngày, │
│ dễ bỏ sót review tiếng nước ngoài)                          │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3: phân loại   │
│ mức khẩn + tóm tắt; Bước 4: draft phản hồi                  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   - Thời gian từ khi review đăng → được gắn cờ: 24h ──> <1h │
│   - Recall phàn nàn khẩn cấp ≥ 95% (không bỏ sót)           │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

# 🗳️ Đề xuất cho nhóm: chọn **Card #1 — Vinhomes**

**Lý do chọn #1:**
- Khối lượng lặp lại lớn nhất (hàng trăm lượt/ngày/khu đô thị), dữ liệu đã có sẵn dưới dạng text trong app → dễ lấy log để đánh giá.
- Rủi ro khi AI sai **thấp và kiểm soát được**: AI chỉ *đề xuất* phân loại và *draft* phản hồi, nhân viên BQL vẫn bấm xác nhận (HITL). Sai thì chuyển lại tổ, không gây hậu quả an toàn.
- Có thể đo baseline ngay bằng log ticket hiện tại (thời gian xử lý, tỉ lệ chuyển nhầm).

**Lý do chưa chọn #2 (VinFast):** liên quan an toàn xe; cần bộ nhãn mã lỗi chuẩn từ kỹ thuật, chưa có → **NOT YET**.
**Lý do chưa chọn #3 (Vinpearl):** giá trị tốt nhưng phần lớn bước 2–3 có thể giải quyết trước bằng rule/keyword + sentiment API sẵn có; chưa cần LLM ngay.
