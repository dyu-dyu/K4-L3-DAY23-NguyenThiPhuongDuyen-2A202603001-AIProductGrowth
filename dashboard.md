<style>
@media print {
  @page { size: A4 landscape; margin: 5mm; }
  body { font-size: 7pt; line-height: 1.02; }
  h1 { font-size: 13pt; margin: 0 0 2px; }
  h3 { font-size: 8.5pt; margin: 3px 0 1px; }
  p { margin: 1px 0; }
  table { font-size: 6.2pt; line-height: 1; margin: 1px 0; }
  th, td { padding: 1px 2px; }
  ol { font-size: 6.6pt; margin: 1px 0 1px 14px; padding: 0; }
  li { margin: 0; }
}
</style>

# OPERATING DASHBOARD — AI IT Helpdesk Automation

**Loại mô hình:** B2B · **Kênh:** PLG cho SMB; paid pilot chuẩn hóa, không Sales-Led bespoke · **Cập nhật:** 09/10/2026 · **Nguyễn Thị Phương Duyên — MSSV: 2A202603001**  
**Chốt loại:** Doanh nghiệp trả tiền từ ngân sách IT operations; nhân viên và đội IT của chính doanh nghiệp sử dụng bot Microsoft Teams; không có partner đưa sản phẩm tới khách hàng bên ngoài.  
**NORTH STAR:** Median TTFV của 3 khách/pilot gần nhất — **hiện tại: chưa đo** — **mục tiêu: <30 ngày**.

### Đèn báo sớm — Leading

| Đèn | Hiện tại | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---:|---|---|---|
| Median TTFV | Chưa đo 🔧 | <30 ngày / 30–60 / >60 | [TB], baseline 08/12/2026 | Usage depth → NRR |
| Deal chết ở security/procurement | Chưa đo 🔧 | <10% / 10–20% / >20% | [TB], baseline 31/12/2026 | POC→paid → CAC payback |

### Đèn vận hành — Operating

| Đèn | Hiện tại | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---:|---|---|---|
| POC→paid | Chưa đo ❌ | ≥50% / 35–<50% / <35% | [BM] [ICONIQ 2026](https://www.iconiq.com/growth/reports/state-of-go-to-market-2026), 09/10/2026 | CAC payback |
| Usage depth/tài khoản | Chưa đo 🔧 | ≥60% / 30–<60% / <30% | [TB], baseline 08/12/2026 | NRR |
| Chi phí AI/doanh thu outcome | 3,31% mô phỏng | ≤3,31% / >3,31–18,20% / >18,20% | [MH] Cost model | Gross Margin |

### Đèn kết quả — Lagging

| Đèn | Hiện tại | 🟢 / 🟡 / 🔴 | Nguồn | Báo trước cho |
|---|---:|---|---|---|
| NRR | Chưa đo ❌ | ≥110% / 100–<110% / <100% | [BM] [Benchmarkit 2026](https://www.benchmarkit.ai/2026-saas-ai-native-metrics), 09/10/2026 | LTV · ARR |
| Gross Margin | 74,89% mô phỏng | ≥60% / 50–<60% / <50% | [MH] Cost/Job | Runway · hòa vốn |
| CAC payback | 213,66 tháng mô phỏng 🔴 | ≤12 / >12–24 / >24 tháng | [BM] [Bessemer](https://www.bvp.com/atlas/scaling-to-100-million) + [MH], 09/10/2026 | Runway · vốn lưu động |

### 5 luật quyết định — ⏹ là luật dừng

1. ⏹ **NẾU** median TTFV >60 ngày **TRÊN** 3 pilot gần nhất **VÀ** cả 3 đã go-live **THÌ** dừng nhận pilot rộng; Product/GTM cắt pilot mới trong sprint kế tiếp xuống một use case, một phòng ban, một outcome **KHÔNG THÌ** không tuyển sales hoặc thêm integration để che TTFV.
2. ⏹ **NẾU** deal chết ở security/procurement >20% **TRONG** một quý **VÀ** có ≥5 deal đã đóng **THÌ** dừng POC sales-assisted/demo tùy biến 2 tuần và hoàn thành Evidence Pack **KHÔNG THÌ** không giảm giá hoặc hứa ngoại lệ bảo mật.
3. **NẾU** POC→paid <35% **TRÊN** 3 POC gần nhất **VÀ** mỗi POC có buyer, baseline, success metric **THÌ** khóa POC mới 5 ngày; Product/GTM phân loại lý do thua và siết POC brief **KHÔNG THÌ** không kéo dài miễn phí hoặc giảm giá.
4. **NẾU** chi phí AI/doanh thu outcome >18,20% **TRONG** 2 tuần **VÀ** mỗi tuần ≥200 ticket attempt **THÌ** áp cost cap theo tài khoản trong sprint kế tiếp; Backend/AI thực hiện model routing và KB cache **KHÔNG THÌ** không tăng giá đại trà hoặc bỏ chi phí ticket thất bại khỏi phép tính.
5. ⏹ **NẾU** CAC payback PLG >24 tháng **TRONG** 2 cohort **VÀ** mỗi cohort ≥3 khách trả tiền **THÌ** dừng acquisition trả phí/tuyển AE 30 ngày và chuẩn hóa paid pilot **KHÔNG THÌ** không tăng ngân sách acquisition hoặc mở Sales-Led bespoke để mua logo.

### Cổng gác 90 ngày

| Ngày | Metric duy nhất | Ngưỡng qua cổng | Bằng chứng vật lý | Nếu trượt |
|---|---|---|---|---|
| **30 · 08/11/2026** | Evidence Pack completion | **3/3 tài sản đạt v1** | Thư mục có `eval-results.md`, `risk-checklist.md`, `pilot-report.md`, mỗi file có owner, mẫu số và ngày | **FIX một lần:** thu hẹp eval về một use case và hoàn tất tài sản thiếu trong 30 ngày; trượt lại → PIVOT value metric |
| **60 · 08/12/2026** | Median TTFV | **<30 ngày trên ≥2 pilot go-live** | CRM export có `pilot_start_at`; ticket log có ID, `first_verified_resolution_at` và xác nhận của user/IT | **FIX một lần:** cắt pilot xuống một use case, một phòng ban; trượt lại → **PIVOT** sang onboarding PLG chuẩn hóa, không FIX lần hai |
| **90 · 07/01/2027** | POC→paid | **≥35% trên đủ 3 POC hoàn tất (tức ≥2/3)** | CRM export danh sách POC kết thúc + hợp đồng trả tiền ký trong ≤30 ngày | **PIVOT:** dừng POC bespoke và chuyển sang onboarding PLG có paid pilot chuẩn hóa, giới hạn phạm vi |

**KILL CRITERIA:** Đến **07/01/2027**, KILL hướng AI IT Helpdesk cho SMB nếu sau một lần FIX thu hẹp phạm vi vẫn có **<3 pilot go-live đạt first value trong ≤60 ngày**.

**CHƯA ĐO ĐƯỢC:** Chưa có số thật cho TTFV, security loss, POC→paid, usage depth, NRR, GM và CAC payback. Cần CRM chuẩn hóa; timestamp pilot/first value; event Teams/ticket; log token, HITL, hóa đơn và chi phí GTM. Có baseline TTFV/usage ngày **08/12/2026**, security ngày **31/12/2026**, POC→paid/GM/CAC ngày **07/01/2027**, NRR cohort đầu ngày **31/03/2027**. Các số 3,31%, 74,89% và 213,66 tháng hiện chỉ là mô phỏng.
