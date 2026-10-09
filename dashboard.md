# OPERATING DASHBOARD — ÔnNhớ AI

Dương Thị Hồng Viên · 2A202602385 · B2C · 09/10/2026

**Dữ liệu hiện tại: chưa đo.** Ngưỡng [MH] từ mô hình minh họa; số hiện tại N/A.

**North Star:** L1, mức rơi D30→D60; mục tiêu ≤2 điểm %. Cá nhân tự trả tiền và tự ôn trên web ÔnNhớ AI, không có trung gian.

## Leading — báo sớm

| Đèn | Hiện | Xanh / Vàng / Đỏ | Nguồn và lý do | Báo trước |
|---|---|---|---|---|
| L1 Mức rơi retention D30→D60 | N/A | ≤2 điểm % / >2 đến 5 điểm % / >5 điểm % | [MH] 200 user: chấp nhận mất tối đa 10 người sau D30; mục tiêu chỉ mất 4. | GM các tháng tiếp theo |
| L2 Activation 24 giờ | N/A | ≥60% / 40% đến <60% / <40% | [MH] 100 user/tuần; hỗ trợ được 40 người chưa activation, tối đa 60 khi dành thêm buổi hỗ trợ. | Trial→paid |
| L3 p95 AI cost / ARPU | N/A | ≤40% / >40% đến 50% / >50% | [MH] GM mỗi user tối thiểu 40%, chi phí khác 10%: AI tối đa 50%; mục tiêu GM 50% cho nhóm nặng cho trần 40%. | GM |

## Operating — vận hành

| Đèn | Hiện | Xanh / Vàng / Đỏ | Nguồn và lý do | Báo trước |
|---|---|---|---|---|
| O1 Trial→paid | N/A | ≥6% / 5% đến <6% / <5% | [MH] Chi phí thu hút + phục vụ trial 6.000đ; lãi gộp tháng đầu/paid 120.000đ: cần 5%, mục tiêu 6% có dư 20%. | CAC payback, GM |
| O2 Free AI cost / tổng COGS | N/A | ≤20% / >20% đến 25% / >25% | [MH] 100 paid: doanh thu 20 triệu, COGS paid 6 triệu; GM 60% cho phép free 2 triệu: 2/(6+2)=25%. | GM |
| O3 Refund rate | N/A | ≤2% / >2% đến 5% / >5% | [MH] Với giá bằng nhau, ngân sách hoàn tiền mục tiêu 400.000đ/20 triệu =2%; giới hạn rủi ro 1 triệu/20 triệu =5%; giả định thận trọng mỗi refund mất cả giá gói. | GM, tiền thu ròng |

## Lagging — kết quả

| Đèn | Hiện | Xanh / Vàng / Đỏ | Nguồn và lý do | Báo trước |
|---|---|---|---|---|
| G1 Gross margin | N/A | ≥60% / 50% đến <60% / <50% | [MH] Mục tiêu giữ ≥12 triệu trên doanh thu thuần 20 triệu; mức sàn giữ 10 triệu để bù một phần chi phí cố định. | Kết quả; đối chiếu L3/O2 |

## 5 luật (⏹ = dừng; Viên thực hiện ngay khi đủ điều kiện)

1. ⏹ NẾU L1 >5 điểm % TRÊN 2 cohort liên tiếp đã đủ D60 VÀ mỗi cohort ≥200 user THÌ dừng ads 21 ngày, sửa phiên ôn đầu và nhắc ôn; KHÔNG THÌ không tăng ads để bù người rời.

2. NẾU L3 >50% TRONG 30 ngày VÀ có ≥100 user trả phí THÌ áp quota 250 phiên/tháng, chuyển lượt vượt quota sang gói credit trong 7 ngày; KHÔNG THÌ không tăng giá mọi user. Kiểm tra thêm nhóm top 5% để không bỏ sót đuôi sau p95.

3. NẾU O1 <5% TRÊN 3 cohort trial đã chín VÀ mỗi cohort ≥100 user THÌ thử paywall sau phiên ôn thành công trong 14 ngày; KHÔNG THÌ không giảm giá gói.

4. ⏹ NẾU O2 >25% TRONG 2 tháng liên tiếp VÀ mỗi tháng ≥100 paid THÌ dừng cấp quota free mới, giảm free xuống 3 phiên/tuần trong 7 ngày; KHÔNG THÌ không mở thêm free để lấy lượt đăng ký.

5. NẾU L2 <40% TRONG 2 tuần liên tiếp VÀ mỗi tuần ≥100 user mới THÌ rút onboarding còn chọn chủ đề → ôn 5 câu, thử với 10 người trong 7 ngày; KHÔNG THÌ không thêm tính năng để che lỗi onboarding.

## Cổng 90 ngày

| Ngày | Metric | Qua cổng | Bằng chứng | Trượt |
|---|---|---|---|---|
| 30 · 08/11/2026 | Số user có bản ghi activation 24h đầy đủ (cả đạt và chưa đạt) | ≥200 | activation_baseline.csv + event_dictionary.md | FIX tracking 30 ngày nếu lỗi log; PIVOT kênh tuyển nếu không tuyển đủ |
| 60 · 08/12/2026 | L1 của cohort ngày khởi động, ≥200 user đủ D60 | ≤5 điểm % | cohort_retention.csv: user ẩn danh, R30, R60, mẫu số cố định | FIX phiên ôn 30 ngày nếu rõ lỗi; PIVOT nếu nhu cầu sai; KILL nếu đã FIX vẫn >5 |
| 90 · 07/01/2027 | O1 trên ≥100 trial cùng phiên bản đã đủ 14 ngày | ≥5% | trial_paid.csv + payment_reconciliation.csv | FIX paywall 30 ngày nếu chưa sửa; PIVOT nếu sai người trả; KILL nếu đã FIX vẫn <5% |

GO khi đạt ngưỡng và đủ mẫu → sang chặng sau; FIX 30 ngày, sửa đúng một việc nếu biết lỗi và chưa FIX; PIVOT khi giả định gốc sai; KILL khi đã FIX một lần mà vẫn không đạt (không FIX lần hai); thiếu mẫu ghi N/A, dừng tăng chi tiền và PIVOT kênh tuyển, không kết luận retention/conversion.

**KILL CRITERIA:** Đến 07/01/2027, nếu O1 vẫn <5% trên ≥100 trial cùng phiên bản đủ14 ngày sau đúng một lần FIX paywall thì em dừng hẳn thử nghiệm thuê bao ÔnNhớ AI và ngừng chi tiền thu hút người dùng cho hướng này.

**CHƯA ĐO ĐƯỢC:** Cả 7 đèn chưa đo (🔧/❌ Trạm 1): L2 cần signup/completed/viewed, dự kiến 23/10/2026; O1 cần trial/billing đủ14 ngày, 08/11/2026; L3 cần AI ledger paid đủ30 ngày, O3 cần refund đủ30 ngày, 08/11/2026; O2/G1 cần sổ COGS free/paid và doanh thu thuần 2 kỳ, 08/12/2026; L1 cần cohort ≥200 đủD60, 08/12/2026. Tất cả là lịch dự kiến nếu đủ mẫu; chưa có log thật. M12 chưa chọn vào dashboard, sớm nhất09/10/2027.
