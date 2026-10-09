# Worksheet — AI IT Helpdesk Automation

Họ tên: Nguyễn Thị Phương Duyên · MSSV: 2A202603001 · Ngày làm: 09/10/2026

## Trạm 1 — Loại mô hình

### Ba câu hỏi phân loại theo thực tế hiện tại

1. **Ai trả tiền?** Doanh nghiệp có bộ phận IT nội bộ trả tiền từ ngân sách phần mềm/IT operations. IT Manager hoặc Head of IT đề xuất; CIO, COO, CFO hoặc giám đốc có thẩm quyền phê duyệt.
2. **Ai dùng sản phẩm?** Nhân viên của chính doanh nghiệp mua sử dụng bot để yêu cầu hỗ trợ IT; đội IT nội bộ quản trị Knowledge Base, nhận ticket và xử lý các trường hợp được chuyển tiếp.
3. **Có bên trung gian và có chạm end-user không?** Không có partner trung gian phân phối sản phẩm tới khách hàng của họ. Sản phẩm phục vụ người dùng nội bộ của doanh nghiệp mua và chạm họ trực tiếp qua bot hỗ trợ IT trong Microsoft Teams, cùng log hội thoại/ticket trong phạm vi tenant được doanh nghiệp cấp quyền.

**Câu chốt loại:** Chúng tôi là **B2B** vì doanh nghiệp có bộ phận IT nội bộ trả tiền từ ngân sách IT operations, nhân viên và đội IT của chính doanh nghiệp đó trực tiếp sử dụng sản phẩm qua bot Microsoft Teams, và không có partner trung gian đưa sản phẩm tới khách hàng của họ.

### Bảng đèn B2B (§3.2)

Quy ước: ✅ đo được hôm nay (ghi số nằm ở đâu) · 🔧 đo được trong 2 tuần (ghi rõ cần bổ sung log, event tracking hoặc dữ liệu gì) · ❌ chưa đo được và hiện chưa biết cách tạo ra một số hợp lệ (ghi trung thực điều kiện còn thiếu, không dùng số mô phỏng thay thế).

| Đèn | ✅ / 🔧 / ❌ | Số nằm ở đâu / cần gì để đo |
|---|---|---|
| Time-to-first-value (TTFV) | 🔧 | Chưa có số thật. Trong pilot cần chốt “first value” là ticket hợp lệ đầu tiên được AI xử lý thành công và được xác nhận; ghi `contract/pilot_start_at` và `first_verified_resolution_at` trong log ticket để tính số ngày. Không dùng mốc “đã cài xong”. |
| Pipeline coverage | 🔧 | Chưa có CRM/pipeline được xác minh. Tạo danh sách cơ hội với giá trị dự kiến, stage đủ điều kiện và target doanh thu quý; tính tổng giá trị cơ hội đủ điều kiện ÷ target doanh thu quý. Không tính phỏng vấn hoặc lead chưa qualified. |
| % deal chết ở security/procurement | 🔧 | Thêm trường `closed_lost_reason` trong CRM, tách riêng security, data/privacy và procurement. Cần log mọi deal đóng hoặc mất; số ban đầu có thể lấy sau khi bắt đầu tiếp cận IT Manager, nhưng chưa đủ mẫu để làm baseline. |
| POC → paid | ❌ | Hiện chưa có POC hoàn tất hay hợp đồng trả tiền và chưa biết cách tạo một tỷ lệ hợp lệ khi mẫu số vẫn bằng 0; không dùng demo, phỏng vấn hoặc mục tiêu pilot làm dữ liệu thay thế. Điều kiện tối thiểu để thiết kế cách đo về sau là có mã POC, ngày bắt đầu/kết thúc và hợp đồng trả tiền liên kết với từng POC. |
| Sales cycle (tuần) | ❌ | Hiện chưa có deal đóng và chưa biết cách tạo số chu kỳ bán hợp lệ khi chưa có quan sát từ qualified opportunity đến hợp đồng ký; không lấy ngày phỏng vấn đầu tiên hoặc số mô phỏng thay thế. Điều kiện tối thiểu để thiết kế cách đo về sau là CRM có timestamp qualified và ngày ký cho từng deal. |
| Usage depth trong tài khoản | 🔧 | Gắn event cho bot Microsoft Teams và ticket API: user/workflow đủ điều kiện, hoạt động hằng tuần, ticket AI xử lý và ticket escalated. Cần thống nhất mẫu số là seat hoặc workflow đã mua; không tính tài khoản test và thao tác nội bộ của đội triển khai. |
| Chi phí triển khai ÷ ACV | 🔧 | Model Day22 có Cost/Job mô phỏng nhưng chưa có chi phí triển khai thật. Cần timesheet theo khách, đơn giá giờ công, chi phí connector/hạ tầng và ACV đã ký; tính `(giờ triển khai × đơn giá + chi phí tích hợp riêng) ÷ ACV`. Không gộp chi phí phát triển sản phẩm dùng chung. |
| Tập trung doanh thu | ❌ | Hiện chưa có khách trả tiền và chưa biết cách tạo tỷ lệ hợp lệ khi tổng doanh thu thực nhận bằng 0; không dùng pipeline hoặc giá trị hợp đồng chưa ghi nhận thay thế. Điều kiện tối thiểu để thiết kế cách đo về sau là hóa đơn/kế toán tách doanh thu thuần theo từng khách trong cùng kỳ. |
| Net Revenue Retention (NRR) | ❌ | Hiện chưa có cohort khách đầu kỳ hay một chu kỳ gia hạn và chưa biết cách tạo NRR hợp lệ khi doanh thu đầu kỳ bằng 0; không tính khách mới hoặc số mô phỏng. Điều kiện tối thiểu để thiết kế cách đo về sau là billing theo khách qua ít nhất một chu kỳ, có expansion, contraction và churn. |
| Gross Margin | 🔧 | Day22 đang có GM **74,89% mô phỏng**, không phải số vận hành. Cần log chi phí LLM/retrieval/storage theo ticket, chi phí hỗ trợ trực tiếp và doanh thu thuần thực nhận; tính `(doanh thu − COGS trực tiếp) ÷ doanh thu`. Không đánh dấu ✅ cho đến khi có dữ liệu pilot hoặc hóa đơn thật. |
| CAC payback | ❌ | Day22 chỉ có CAC và ARPU giả định/mô phỏng; chưa có khách trả tiền nên chưa biết cách tạo payback thực tế hợp lệ mà không thay dữ liệu thật bằng giả định. Điều kiện tối thiểu để thiết kế cách đo về sau là chi phí sales/marketing phân bổ cho khách mới và gross profit thực tế theo tháng của cùng cohort. |

### Khoảng trống dữ liệu cần mang sang dashboard

- Chưa có pilot đã hoàn tất, khách trả tiền hoặc dữ liệu gia hạn; vì vậy POC→paid, sales cycle, revenue concentration, NRR và CAC payback chưa thể có số thật.
- Chưa có định nghĩa sự kiện “first value” và chưa có event tracking cho Microsoft Teams/ticket API.
- Chưa có CRM với stage, giá trị cơ hội và lý do closed-lost chuẩn hóa.
- Chưa có timesheet triển khai theo khách hoặc cost log AI theo ticket.
- Các số Cost/Job, containment, ARPU, CAC và GM trong bài Day22 hiện là giả định/mô phỏng; không được trình bày như dữ liệu đã đo.

**Nguồn đối chiếu:** `NguyenThiPhuongDuyen_Day22_onepager.docx` và `NguyenThiPhuongDuyen_Day22_model.xlsx` trong thư mục Day22; one-pager ghi rõ các số cần pilot/eval để xác minh.

## Trạm 2 — Thẻ đèn

**North Star:** **Median Time-to-first-value (TTFV) của 3 khách/pilot gần nhất** — hiện tại **chưa đo được vì chưa có pilot đủ điều kiện** — mục tiêu **<30 ngày** từ lúc pilot bắt đầu đến ticket thật đầu tiên được AI giải quyết và người dùng/IT xác nhận.

**Kênh GTM dùng trong dashboard:** **PLG cho SMB**; POC/paid pilot là bước xác minh có hỗ trợ và được chuẩn hóa, không phải motion Sales-Led bespoke. CAC Sales-Led trong model chỉ là đối chứng để loại bỏ một kênh không khả thi.

| # | Tầng (L/O/G) | Đèn | Định nghĩa (đếm gì · **không** đếm gì) | Công thức | Nhịp · ai lấy số | Báo trước cho |
|---|---|---|---|---|---|---|
| 1 | L | **Median Time-to-first-value (TTFV)** | Trung vị số ngày của tối đa 3 khách/pilot gần nhất, tính từ lúc pilot chính thức bắt đầu đến ticket production đầu tiên được AI giải quyết, có ticket ID và được nhân viên hoặc IT xác nhận. **Không** tính ngày cài đặt xong, demo, ticket test, câu trả lời chưa được xác nhận hoặc ticket đã chuyển cho IT xử lý. | Với từng tài khoản: `first_verified_resolution_at − pilot_start_at`; đèn tuần = median TTFV của tối đa 3 tài khoản đủ điều kiện gần nhất. | Cập nhật khi phát sinh first value, xem hằng tuần · Product/GTM + Backend/AI | **Usage depth** → **NRR**; khách thấy giá trị sớm có khả năng đưa bot vào luồng hỗ trợ thật và tiếp tục sử dụng cao hơn. |
| 2 | L | **% deal chết ở security/procurement** | Tỷ lệ cơ hội đã đóng trong kỳ có lý do chính là security, privacy/data hoặc procurement. **Không** tính deal còn mở, lead chưa qualified, deal trùng, deal thua vì không có nhu cầu hoặc vì giá. | `Số opportunity closed-lost do security/procurement ÷ (tổng opportunity closed-won + closed-lost trong kỳ) × 100%`. | Hằng tháng · Product/GTM | **POC→paid** → **CAC payback**; vướng duyệt làm ít POC chuyển thành hợp đồng và kéo dài chi phí bán hàng. |
| 3 | O | **POC → paid** | Tỷ lệ POC đã kết thúc trong kỳ dẫn tới hợp đồng trả tiền được ký trong vòng 30 ngày sau khi POC kết thúc. **Không** tính demo, phỏng vấn, POC đang chạy, gia hạn thử miễn phí hoặc thư bày tỏ quan tâm chưa ký. | `Số POC hoàn tất có hợp đồng trả tiền trong ≤30 ngày ÷ tổng POC hoàn tất trong kỳ × 100%`. | Cập nhật sau mỗi POC, tổng hợp hằng tháng/quý · Product/GTM | **CAC payback**; conversion thấp làm chi phí của các POC thất bại dồn lên mỗi khách có được. |
| 4 | O | **Usage depth trong tài khoản** | Tỷ lệ ticket hỗ trợ IT production thuộc phạm vi pilot/hợp đồng được nhân viên gửi qua bot Microsoft Teams trong tuần. Ticket đã dùng bot vẫn được tính nếu sau đó escalated. **Không** tính ticket test, ticket trùng, ticket ngoài phạm vi và thao tác của đội triển khai. | `Số ticket production in-scope khởi tạo qua bot ÷ tổng ticket production in-scope trên mọi kênh trong tài khoản × 100%`; báo cáo từng tài khoản, không lấy trung bình che khuất tài khoản yếu. | Hằng tuần · Product + Backend/AI | **NRR**; tài khoản đưa bot vào tỷ trọng workflow thật cao có khả năng gia hạn hoặc mở rộng cao hơn. |
| 5 | O | **Tỷ lệ chi phí AI trên doanh thu outcome** | Toàn bộ chi phí biến đổi LLM, embedding/reranking, vector retrieval và hạ tầng phát sinh từ các lần thử xử lý ticket, quy về mỗi ticket được xác nhận giải quyết thành công, rồi so với giá outcome. **Không** bỏ chi phí của lần thử thất bại/escalated; không tính R&D, sales hoặc chi phí triển khai một lần. | `[(Tổng chi phí AI biến đổi của mọi ticket attempt) ÷ số ticket verified resolved] ÷ doanh thu outcome trên mỗi verified resolution × 100%`. | Hằng tuần theo từng tài khoản · Backend/AI + Product/GTM | **Gross Margin**; chi phí token/retrieval tăng xuất hiện ở đây trước khi làm biên gộp tháng giảm. |
| 6 | G | **Net Revenue Retention (NRR)** | Doanh thu định kỳ cuối kỳ từ đúng nhóm khách đã tồn tại đầu kỳ, sau expansion, contraction và churn. **Không** tính doanh thu từ khách mới, phí triển khai một lần hoặc POC miễn phí. | `(Recurring revenue đầu kỳ + expansion − contraction − churn) ÷ recurring revenue đầu kỳ × 100%`. | Hằng quý · Product/GTM + người phụ trách tài chính | **LTV và độ ổn định ARR**; NRR dưới 100% làm doanh thu cohort co lại dù vẫn ký thêm khách. |
| 7 | G | **Gross Margin thực tế** | Tỷ lệ doanh thu thuần còn lại sau toàn bộ COGS trực tiếp: AI inference/retrieval, hosting, hỗ trợ vận hành và nhân công trực tiếp phục vụ khách. **Không** tính R&D sản phẩm dùng chung, sales/marketing hoặc G&A; không dùng GM mô phỏng thay cho số vận hành. | `(Doanh thu thuần − COGS trực tiếp) ÷ doanh thu thuần × 100%`. | Hằng tháng, chốt hằng quý · Product/GTM + người phụ trách tài chính | **Runway và khả năng hòa vốn**; biên thấp làm mỗi đồng doanh thu đóng góp ít tiền hơn cho chi phí cố định. |
| 8 | G | **CAC payback** | Số tháng gross profit cần để thu hồi CAC đầy đủ của một cohort khách mới. CAC gồm sales/marketing, thời gian demo/POC và chi phí acquisition phân bổ. **Không** tính chi phí R&D, không dùng giá trị pipeline chưa ký và không dùng ARPU/GM giả định như số thật. | `CAC đầy đủ bình quân mỗi khách mới ÷ gross profit bình quân mỗi khách mỗi tháng`. | Hằng quý theo cohort · Product/GTM + người phụ trách tài chính | **Runway và nhu cầu vốn lưu động**; payback dài khóa tiền mặt trước khi cohort hoàn vốn. |

**Đèn chi phí AI là đèn số 5 — Tỷ lệ chi phí AI trên doanh thu outcome.** Đèn này tính cả chi phí của các lần AI thử nhưng không tạo ra outcome được thu tiền, nên không để tỷ lệ containment thấp làm Cost/Job trông đẹp giả tạo.

### Cây quan hệ ba tầng

```text
TTFV ───────────────→ Usage depth ───────────────→ NRR ─────────→ LTV / ARR

Deal chết ở security
/ procurement ──────→ POC → paid ───────────────→ CAC payback ─→ Runway

Chi phí AI / doanh thu outcome ──────────────────→ Gross Margin → Runway
```

## Trạm 3 — Ngưỡng

| # | Đèn | 🟢 | 🟡 | 🔴 | Nguồn [BM]/[MH]/[TB] | Lý do (1 câu) · ngày kiểm tra nếu [BM] |
|---|---|---|---|---|---|---|
| 1 | Median TTFV | <30 ngày | 30–60 ngày | >60 ngày | [TB] | Chưa có chuẩn riêng của sản phẩm; dùng guardrail B2B ban đầu, đo 2 chu kỳ pilot rồi chốt baseline vào **08/12/2026**; trên 60 ngày nghĩa là khách chưa thấy giá trị trong phần lớn một quý. |
| 2 | % deal chết ở security/procurement | <10% | 10–20% | >20% | [TB] | Chưa có lịch sử closed-lost; dùng dải khởi đầu của bảng B2B, chỉ kích hoạt sau ≥5 opportunity đã đóng và chốt baseline sau 2 chu kỳ tháng vào **31/12/2026**. |
| 3 | POC → paid | ≥50% | ≥35% và <50% | <35% | [BM] | [ICONIQ State of GTM 2026](https://www.iconiq.com/growth/reports/state-of-go-to-market-2026) ghi POC/free-trial→paid khoảng 50% năm 2026 và khoảng 36% năm 2025, nên 50% là mức xanh còn dưới 35% là tụt dưới mặt bằng cũ; nguồn truy cập **09/10/2026**. |
| 4 | Usage depth trong tài khoản | ≥60% | ≥30% và <60% | <30% | [TB] | Chưa có baseline production; dùng guardrail B2B ban đầu và đo riêng từng tài khoản qua 2 chu kỳ pilot 4 tuần, dự kiến có baseline **08/12/2026**. |
| 5 | Tỷ lệ chi phí AI trên doanh thu outcome | ≤3,31% | >3,31% và ≤18,20% | >18,20% | [MH] | 3,31% là tỷ lệ chi phí AI biến đổi đang mô phỏng; 18,20% là ngân sách AI tối đa còn lại để giữ GM 60% sau HITL, tính tại Phụ lục [MH] 1. |
| 6 | NRR | ≥110% | ≥100% và <110% | <100% | [BM] | [Benchmarkit 2026 SaaS & AI-Native Metrics](https://www.benchmarkit.ai/2026-saas-ai-native-metrics) ghi NRR 108% cho usage pricing và 98% cho seat pricing; sản phẩm Hybrid đặt xanh ≥110% để vượt mốc usage, còn dưới 100% là cohort co lại; nguồn truy cập **09/10/2026**. |
| 7 | Gross Margin thực tế | ≥60% | ≥50% và <60% | <50% | [MH] | Model chọn GM mục tiêu 60%, tương ứng Cost/Job tối đa $0,396; dưới 50% vượt Cost/Job $0,495 và vi phạm điều kiện sống còn đã ghi trong one-pager, xem Phụ lục [MH] 2. |
| 8 | CAC payback | ≤12 tháng | >12 và ≤24 tháng | >24 tháng | [BM] + [MH] | [Bessemer — Scaling to $100 Million](https://www.bvp.com/atlas/scaling-to-100-million) dùng mốc SMB/Mid/Enterprise lần lượt 12/18/24 tháng; sản phẩm đang chọn SMB nên >12 tháng đã cảnh báo và >24 tháng là vượt cả trần Enterprise; nguồn truy cập **09/10/2026**, còn ngân sách CAC của model được tính tại Phụ lục [MH] 3. |

### Phụ lục [MH] — phép tính (≥2)

> Tất cả đầu vào dưới đây là **giả định/mô phỏng trong model Day22**, chưa phải kết quả pilot. Chúng được dùng để xác định ranh giới sống còn và phải được thay bằng số thật khi có Pilot Report.

**[MH] 1 — Tỷ lệ chi phí AI trên doanh thu outcome**

```
Đầu vào:
- Giá outcome P = $0,99/job                         (2_Pricing!B19)
- Job hoàn thành = 820/tháng                       (1_Cost_Job!B11)
- Chi phí AI biến đổi = $26,87/tháng               (1_Cost_Job!B62: API + infra + retry)
- HITL = $177/tháng                                (1_Cost_Job!B63)
- GM mục tiêu = 60%                                (2_Pricing!B32)
- Giá Claude Haiku 4.5 = $1 input / $5 output mỗi 1M token
  (Anthropic, truy cập 09/10/2026: https://www.anthropic.com/claude/haiku)

Chi phí AI biến đổi/job = 26,87 ÷ 820 = $0,032768
Tỷ lệ AI/doanh thu outcome hiện mô phỏng = 0,032768 ÷ 0,99 = 3,3099%

HITL/job = 177 ÷ 820 = $0,215854
Tổng COGS/job tối đa để giữ GM 60% = 0,99 × (1 − 60%) = $0,396
Ngân sách AI/job tối đa còn lại = 0,396 − 0,215854 = $0,180146
Tỷ lệ AI tối đa = 0,180146 ÷ 0,99 = 18,1966%

Kết quả → 🟢 ≤3,31% · 🟡 >3,31% đến ≤18,20% · 🔴 >18,20%
```

**[MH] 2 — Gross Margin thực tế**

```
Đầu vào:
- Giá outcome = $0,99/job                          (2_Pricing!B19)
- Cost/Job mô phỏng = $0,248621951/job             (1_Cost_Job!B66)
- GM mục tiêu của model = 60%                      (2_Pricing!B32)
- Mức mô hình gãy đã chọn trong one-pager = GM <50%

GM mô phỏng = (0,99 − 0,248621951) ÷ 0,99 = 74,8867%
Cost/Job tối đa tại GM 60% = 0,99 × (1 − 60%) = $0,396
Cost/Job tại GM 50% = 0,99 × (1 − 50%) = $0,495

Kết quả → 🟢 GM ≥60% (Cost/Job ≤$0,396)
          🟡 GM ≥50% và <60% (Cost/Job >$0,396 đến ≤$0,495)
          🔴 GM <50% (Cost/Job >$0,495)
```

**[MH] 3 — CAC tối đa và CAC payback**

```
Đầu vào:
- ARPU = $200/khách/tháng                          (4_Channel_Fit!B5)
- GM mô phỏng = 74,8867%                          (4_Channel_Fit!B6)
- Payback tối đa cho SMB = 12 tháng               (4_Channel_Fit!B8; benchmark Bessemer)
- CAC Sales-Led ước tính = $32.000/khách           (4_Channel_Fit!B22; đối chứng kênh, không phải CAC của PLG đã chọn)

Gross profit/khách/tháng = 200 × 74,8867% = $149,7733
CAC tối đa để payback trong 12 tháng = 149,7733 × 12 = $1.797,28
Payback của CAC ước tính = 32.000 ÷ 149,7733 = 213,66 tháng
Độ lệch CAC = 32.000 ÷ 1.797,28 = 17,80 lần ngân sách cho phép

Kết quả → 🟢 ≤12 tháng · 🟡 >12 đến ≤24 tháng · 🔴 >24 tháng
Kết luận đối chứng: 🔴 213,66 tháng; Sales-Led không khả thi với ARPU và CAC này,
vì vậy dashboard giữ PLG làm kênh chính và sẽ thay số đối chứng bằng CAC PLG thực tế khi có cohort trả tiền.
```

## Trạm 4 — 5 luật quyết định

Đánh dấu ⏹ cho luật dừng (cần ≥2).

1. ⏹ **NẾU** median TTFV **>60 ngày** **TRÊN** 3 khách/pilot gần nhất **VÀ** cả 3 đã go-live với ít nhất một ticket production hợp lệ **THÌ** **dừng nhận pilot phạm vi rộng ngay lập tức**; Product/GTM cắt mọi pilot mới trong sprint kế tiếp xuống đúng một use case, một phòng ban và một outcome được xác nhận **KHÔNG THÌ** không được tuyển thêm sales, thêm integration hoặc nhồi thêm tính năng để che việc khách chưa thấy giá trị.

2. ⏹ **NẾU** tỷ lệ deal chết ở security/procurement **>20%** **TRONG** một quý **VÀ** có ít nhất 5 opportunity đã closed-won hoặc closed-lost **THÌ** **dừng mở POC sales-assisted và demo tùy biến trong 2 tuần**; Product/GTM cùng Product + Tech hoàn thành Evidence Pack gồm data-flow, ma trận quyền truy cập, chính sách lưu/xóa dữ liệu, Eval Results và Risk Checklist trước khi mở lại luồng chuyển đổi từ PLG sang paid pilot **KHÔNG THÌ** không được giảm giá hoặc hứa ngoại lệ bảo mật riêng để cố cứu deal.

3. **NẾU** POC→paid **<35%** **TRÊN** 3 POC đã kết thúc gần nhất **VÀ** mỗi POC đều có buyer, baseline và success metric được ký trước khi chạy **THÌ** **khóa lịch mở POC kế tiếp trong 5 ngày làm việc**; Product/GTM phân loại lý do thua của cả 3 POC và sửa POC brief để chỉ nhận khách có dữ liệu sẵn, người duyệt ngân sách và tiêu chí chuyển sang trả tiền **KHÔNG THÌ** không được kéo dài POC miễn phí hoặc giảm giá để biến một POC không đạt thành hợp đồng.

4. **NẾU** tỷ lệ chi phí AI trên doanh thu outcome **>18,20%** **TRONG** 2 tuần liên tiếp **VÀ** mỗi tuần có ít nhất 200 ticket attempt hợp lệ **THÌ** **áp trần chi phí theo tài khoản trong sprint kế tiếp**; Backend/AI chuyển intent rủi ro thấp sang model rẻ hơn và cache phần Knowledge Base ổn định cho đến khi tỷ lệ trở lại ≤18,20% **KHÔNG THÌ** không được tăng giá đại trà hoặc loại chi phí của ticket thất bại/escalated khỏi phép tính để làm đèn xanh giả.

5. ⏹ **NẾU** CAC payback của kênh PLG **>24 tháng** **TRONG** 2 cohort acquisition liên tiếp **VÀ** mỗi cohort có ít nhất 3 khách trả tiền với CAC và gross profit đã đối soát **THÌ** **dừng chi tiêu acquisition trả phí và kế hoạch tuyển AE trong 30 ngày**; Product/GTM cùng tài chính giữ onboarding PLG tự phục vụ, chuẩn hóa paid pilot với trần giờ hỗ trợ và đo lại CAC theo cohort **KHÔNG THÌ** không được tăng ngân sách acquisition hoặc mở lại Sales-Led bespoke để mua thêm logo khi mỗi khách mới chưa hoàn vốn.

**Số luật dừng:** 3/5 — luật 1, 2 và 5.
