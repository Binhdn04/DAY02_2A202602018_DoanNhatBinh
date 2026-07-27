# 01 — Individual Problem Scan

## Scan rộng

Mình scan 7 problems.

| # | Lăng kính | Problem quan sát được | Ai chịu ảnh hưởng? | Dấu hiệu thật |
|---|---|---|---|---|
| 1 | Tốn thời gian | HR phải đọc nhiều CV để lọc ra ứng viên tiềm năng | HR | 100–200 CV/vị trí |
| 2 | Lặp lại | Trả lời ticket hỗ trợ có nội dung giống nhau | Customer Support | 2-5 phút/ticket, 60% ticket lặp lại |
| 3 | AI có thể tốt hơn | Tìm thông tin trong tài liệu nội bộ từ nhiều nguồn: Confluence, Notion | Team member | 10-15 phút/lần tìm |
| 4 | Pain từ người khác | Người học hỏi lặp đi lặp lại một vấn đề | Mentor, trợ giảng | 5-10 phút/lần trả lời |
| 5 | Lặp lại | Giáo viên chấm các câu hỏi tự luận ngắn có đáp án gần giống nhau | Giáo viên | 1-3 phút/bài |
| 6 | Tốn thời gian | Kế toán đối chiếu hóa đơn với sao kê ngân hàng | Kế toán | 10-15 phút/lần |
| 7 | AI có thể tốt hơn | Marketing phải tổng hợp phản hồi của khách hàng | Marketing | 2-3 phút/bình luận |

## Top 3

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 | Sàng lọc CV ứng viên | Workflow rõ từng bước, ảnh hưởng trực tiếp đến chất lượng tuyển dụng, tốn nhiều thời gian | Đo "chất lượng shortlist" thế nào; CV chứa dữ liệu cá nhân nên cần cẩn trọng privacy |
| 2 | Trả lời ticket hỗ trợ lặp lại | Impact tăng theo số lượng ticket lớn | Ranh giới ticket nào AI được tự trả lời, ticket nào cần người xử lý |
| 3 | Tìm tài liệu nội bộ (Confluence/Notion) | Nhiều người đau, lặp lại thường xuyên, impact rộng cho cả team | Data access qua nhiều nguồn khác nhau phức tạp, scope có thể quá lớn cho MVP |

## Problem Card #1 — Sàng lọc CV ứng viên

**Problem 1 câu:**
Với mỗi vị trí tuyển dụng, HR phải đọc thủ công 100–200 CV để lọc ra ứng viên tiềm năng, trong đó bước đọc kỹ để đánh giá kinh nghiệm/kỹ năng tốn nhiều thời gian nhất và dễ khiến HR quá tải khi tuyển nhiều vị trí song song.

**Actor:**
HR/Recruiter chịu trách nhiệm sàng lọc CV cho một vị trí tuyển dụng và gửi shortlist cho hiring manager.

**Thời điểm / bối cảnh:**
Giai đoạn nhận CV sau khi đăng tuyển (thường 1–2 tuần đầu), khi số lượng CV đổ về nhiều nhất và cần chốt shortlist trước khi hiring manager yêu cầu update.

**Current workflow:**

```text
1. Tải và tập hợp CV từ email / job board / ATS
2. Đọc lướt để loại CV không đạt tiêu chí cơ bản (bằng cấp, năm kinh nghiệm, ngành)
3. Đọc kỹ CV còn lại để đánh giá kỹ năng, kinh nghiệm thực tế
4. Đối chiếu với JD, ghi chú điểm mạnh/yếu từng ứng viên
5. Xếp hạng và chọn ra shortlist
6. Tổng hợp shortlist + nhận xét gửi cho hiring manager
7. Lên lịch phone screen cho ứng viên được chọn
```

**Bottleneck:**
Bước 3 — đọc kỹ CV còn lại để đánh giá kỹ năng/kinh nghiệm mất khoảng 3–5 phút/CV, và số CV này thường vẫn chiếm 30–50% tổng số CV ban đầu sau khi đã lọc thô.

**Impact:**
Với 100–200 CV/vị trí, tổng thời gian sàng lọc có thể lên đến 5–8 giờ/vị trí. HR thường xử lý nhiều vị trí song song nên dễ quá tải, dẫn đến đọc lướt/rush vào cuối và có thể bỏ sót ứng viên tốt.

**Success metric:**
Giảm tổng thời gian sàng lọc từ ~5–8 giờ xuống dưới 2 giờ/vị trí, không giảm tỷ lệ ứng viên trong shortlist pass phone screen so với trước khi dùng AI.

**Non-AI alternative:**
Bộ lọc từ khóa trong ATS kết hợp checklist tiêu chí cứng (bằng cấp, năm kinh nghiệm, kỹ năng bắt buộc) có thể loại bớt CV không đạt ngay từ đầu, nhưng không đánh giá được ngữ cảnh (ví dụ: kinh nghiệm liên quan dù chức danh khác), nên vẫn cần người đọc kỹ phần còn lại.

**AI hypothesis:**
AI đọc CV, trích xuất thông tin chính (kinh nghiệm, kỹ năng, học vấn), so khớp với JD và xếp hạng kèm giải thích ngắn (why fit / why not fit). HR vẫn review kết quả xếp hạng và quyết định shortlist cuối cùng, AI không tự động loại ứng viên.

**Quick gut:**
Workflow.

### Draft current workflow

```text
CURRENT STATE — 300 phút (cho ~100 CV/vị trí)

[1 Tải & tập hợp CV: 15']
→ [2 Đọc lướt loại CV không đạt tiêu chí cơ bản: 60']
→ [3 Đọc kỹ CV còn lại (~40 CV) để đánh giá kỹ năng/kinh nghiệm: 140']  <-- bottleneck
→ [4 Đối chiếu với JD, ghi chú đánh giá: 40']
→ [5 Xếp hạng, chọn shortlist: 25']
→ [6 Tổng hợp gửi hiring manager: 20']
```

### Draft future workflow

```text
FUTURE STATE — 70 phút

[1 Auto-thu thập CV vào hệ thống: 5']
→ [2 AI trích xuất thông tin + so khớp JD + xếp hạng kèm giải thích: 3']
→ [3 HR review CV top-ranked: 40']  <-- human boundary
→ [4 HR spot-check một phần CV bị AI loại để tránh bỏ sót: 15']
→ [5 Chọn shortlist & gửi hiring manager: 7']

Fallback: Spot-check phát hiện AI loại sai nhiều → HR tăng số lượng review thủ công.
```

### Câu hỏi phản biện

- AI có thể vô tình loại nhầm ứng viên tốt do bias trong cách viết CV (ví dụ ứng viên background không truyền thống, đổi ngành, gap năm)? Đo bias này bằng cách nào trước khi tin tưởng xếp hạng?
- Nếu HR chỉ review CV top-ranked và spot-check một phần CV bị loại, ai chịu trách nhiệm khi bỏ sót ứng viên tốt bị AI xếp hạng thấp?
- CV chứa thông tin nhạy cảm (tuổi, ảnh, giới tính, tôn giáo...). Làm sao đảm bảo AI không dùng các yếu tố này để đánh giá, dù không được yêu cầu?
- Metric "giảm xuống dưới 2 giờ/vị trí" có tính luôn thời gian spot-check CV bị loại không? Nếu spot-check phải làm kỹ (để an toàn) thì saving thực tế còn đúng không?
- JD khác nhau giữa các vị trí — AI xếp hạng có generalize tốt giữa nhiều loại JD, hay cần điều chỉnh/prompt riêng cho từng vị trí?
- Nếu ứng viên biết CV được AI lọc, có rủi ro họ "đánh lừa" AI bằng keyword thay vì thể hiện năng lực thật không?
- Ai chịu trách nhiệm pháp lý/đạo đức nếu quy trình có yếu tố phân biệt đối xử trong tuyển dụng?

## Problem Cards #2 và #3 — tóm tắt

| Card | Actor | Bottleneck | Metric | Quick gut | Vì sao chưa chọn làm #1 |
|---|---|---|---|---|---|
| Trả lời ticket hỗ trợ lặp lại | Customer Support agent | Soạn lại câu trả lời cho vấn đề đã gặp nhiều lần | 2-5 phút/ticket → dưới 1 phút/ticket | Agent / Workflow | Impact/ticket nhỏ hơn CV; cần xác định rõ ranh giới ticket nào AI được tự trả lời |
| Tìm tài liệu nội bộ (Confluence/Notion) | Team member | Tìm kiếm qua nhiều nguồn khác nhau, không có index chung | 10-15 phút → dưới 3 phút/lần tìm | Agent (RAG-search) | Data access qua nhiều hệ thống phức tạp hơn; scope rộng khó giới hạn cho MVP |

### Draft workflow — Problem #2: Trả lời ticket hỗ trợ lặp lại

```text
CURRENT STATE — 4 phút/ticket

[1 Đọc ticket: 0.5']
→ [2 Xác định loại vấn đề: 0.5']
→ [3 Tìm câu trả lời tương tự đã dùng trước: 1.5']  <-- bottleneck
→ [4 Soạn lại & tùy biến câu trả lời: 1']
→ [5 Gửi phản hồi & đóng ticket: 0.5']
```

```text
FUTURE STATE — 1.5 phút/ticket

[1 AI phân loại ticket + match câu trả lời mẫu có sẵn: 0.2']
→ [2 AI draft câu trả lời tùy biến theo ticket: 0.3']
→ [3 Agent review & chỉnh sửa nếu cần: 0.8']  <-- human boundary
→ [4 Gửi phản hồi & đóng ticket: 0.2']

Fallback: Ticket phức tạp/nhạy cảm (khiếu nại, hoàn tiền...) → agent tự soạn từ đầu, không dùng draft AI.
```

### Draft workflow — Problem #3: Tìm tài liệu nội bộ (Confluence/Notion)

```text
CURRENT STATE — 12 phút/lần tìm

[1 Xác định từ khóa cần tìm: 1']
→ [2 Search trên Confluence: 3']
→ [3 Search trên Notion (nếu Confluence không có): 3']
→ [4 Đọc qua nhiều trang để lọc đúng thông tin: 4']  <-- bottleneck
→ [5 Hỏi đồng nghiệp trên Slack nếu vẫn chưa rõ: 1']
```

```text
FUTURE STATE — 3 phút/lần tìm

[1 Đặt câu hỏi cho AI search (đã index cả Confluence + Notion): 0.5']
→ [2 AI trả lời trực tiếp kèm trích dẫn nguồn: 0.5']
→ [3 Team member kiểm tra nguồn trích dẫn để xác nhận: 1.5']  <-- human boundary
→ [4 Áp dụng thông tin: 0.5']

Fallback: AI không tìm thấy / trích dẫn không rõ → quay lại search thủ công hoặc hỏi đồng nghiệp.
```

---