# Worksheet — ÔnNhớ AI

Dương Thị Hồng Viên · 2A202602385 · 09/10/2026

## Chuẩn bị — Số liệu đầu vào

Các số là giả định riêng cho bài thực hành, chưa phải số đã đo.

| Đầu vào của mô hình giả định | Giá trị | Căn cứ |
|---|---|---|
| ARPU | 200.000đ/paid/tháng | Giá gói giả định; không tính free |
| Gross margin mục tiêu | 60% | 20 triệu doanh thu −8 triệu COGS |
| CAC dự kiến | 100.000đ/paid | 6.000đ/trial ÷6% conversion |
| CAC payback mục tiêu | ≤1 tháng | Mục tiêu thu hồi chi phí thu hút trong tháng đầu |
| CAC payback dự kiến | 0,833 tháng | 100.000 ÷(200.000 ×60%) |
| Runway kịch bản không có doanh thu | 6 tháng | 180 triệu tiền mặt ÷30 triệu burn/tháng |
| Value Metric | Thuê bao/tháng, quota250 phiên | Credit riêng cho lượt vượt quota |
| Cost/Job | 400đ/phiên ôn5 câu | Chi phí AI giả định, gồm retry; hạ tầng/hỗ trợ tính riêng |

## Trạm 1 — Chốt loại

**Câu chốt loại:** ÔnNhớ AI là B2C vì cá nhân tự trả phí và trực tiếp ôn tập, em chạm người dùng qua web ÔnNhớ AI và log tài khoản ẩn danh, không có doanh nghiệp hay đối tác trung gian trong mô hình này.

- Ai trả tiền? Cá nhân mua gói ôn tập.
- Ai dùng? Chính người mua.
- Có trung gian và chạm end-user không? Không có trung gian; tiếp xúc trực tiếp qua web.

Em chọn sản phẩm ÔnNhớ AI và số liệu giả định để thực hành Day 23. Day 24–25 là nội dung trong lộ trình chưa được học; các đầu vào dưới đây được đặt ngay trong bài này, chưa phải số thực đo.

- Sản phẩm: ÔnNhớ AI, tạo phiên ôn 5 câu kèm giải thích từ ghi chú; cá nhân tự mua và dùng trên web → B2C.
- Value metric: thuê bao 200.000đ/tháng, quota dự kiến 250 phiên; credit riêng cho phần vượt. Free ban đầu 5 phiên/tuần.
- Cost/Job giả định: 400đ/phiên gồm cả retry trung bình; nhóm paid thông thường 100 phiên/tháng → AI 40.000đ; chi phí phục vụ khác 20.000đ/paid/tháng.
- Kịch bản 100 paid: doanh thu thuần 20 triệu, paid COGS 6 triệu, ngân sách free 2 triệu → tổng COGS 8 triệu, GM 60%. Quy mô và giá trị này chưa đo.
- Chi phí mỗi trial (marketing + free trong trial) 6.000đ; không cộng lại khoản này vào CAC một lần nữa. Chi phí R&D/nhân sự cố định 30 triệu/tháng; tiền mặt 180 triệu → runway kịch bản không thu tiền 6 tháng, không phải runway đã kiểm toán.
- CAC kỳ vọng ở conversion 6% = 6.000/0,06 =100.000đ; payback theo GM bình quân 60% =100.000/120.000=0,833 tháng. Mục tiêu ≤1 tháng. Không ước tính LTV khi chưa có lịch sử retention.
- Tất cả ngưỡng dùng [MH] từ giả định, không dùng [BM], không có baseline [TB] thực đo. Màu hiện tại luôn N/A, không gán xanh cho số chưa có.

| Đèn trong bảng B2C | Trạng thái | Vị trí / cần gì |
|---|---|---|
| Retention curve | 🔧 | tracking thiết kế được trong 2 tuần, D60 phải chờ đủ tuổi cohort |
| Activation | 🔧 | event hoàn thành và xem giải thích; baseline sau 2 tuần |
| p95 cost / ARPU | 🔧 | usage ledger theo user; cần cửa sổ 30 ngày |
| Trial→paid | 🔧 | trial và billing; chờ đủ 14 ngày |
| Retention M12 | ❌ | biết cách đo nhưng chưa có cohort 12 tháng; 09/10/2027 mới có |
| Free / COGS | 🔧 | usage free/paid và sổ chi phí tháng |
| Refund | 🔧 | payment/refund; chờ cửa sổ30 ngày |
| LTV/CAC · payback · GM | 🔧 | chỉ mô hình tính được; GM/payback đối chiếu chi phí; LTV chưa kết luận |

Không có đèn ✅ thực đo. 🔧 nghĩa là có thể xây khả năng thu thập trong 2 tuần, không phải đã có giá trị. Retention M12 chưa thể đo trong thời gian lab. Tôi chọn B2C theo tình huống, không khẳng định đây là sản phẩm thực tế của tôi.

## Trạm 2 — Thẻ đèn

North Star: L1, mức rơi retention D30→D60; hiện tại N/A, mục tiêu ≤2 điểm %. Đây là đại diện độ phẳng ngắn hạn, chưa chứng minh retention dài hạn.
| ID | Tầng | Đèn | Định nghĩa và công thức | Nhịp / người đo | Báo trước cho | Luật |
|---|---|---|---|---|---|---|
| L1 | L | Mức rơi retention D30→D60 | max(0, R30−R60), điểm %; cohort đăng ký theo tuần, hoạt động = hoàn thành ≥1 phiên ôn 5 câu trong cửa sổ D24–30 / D54–60; loại test, bot, trùng ID; mẫu số cố định là user đăng ký ban đầu. | Tuần; Viên | GM các tháng tiếp theo | 1 |
| L2 | L | Activation 24 giờ | User mới hoàn thành và xem giải thích phiên ôn 5 câu trong 24h / user mới hợp lệ; loại test, bot; không đếm mở app hoặc tạo bài chưa xong. | Ngày; Viên | Trial→paid | 5 |
| L3 | L | p95 AI cost / ARPU | p95 nearest-rank của tổng chi phí AI mỗi user trả phí trong 30 ngày / 200.000đ; gồm lượt lỗi và retry có tính tiền, loại test; free đo riêng. | Tuần, cửa sổ 30 ngày; Viên | GM | 2 |
| O1 | O | Trial→paid | User hết trial 7 ngày và có thanh toán thành công trong 7 ngày tiếp / user hết trial có cửa sổ đủ 14 ngày; loại test; trả phí tính một lần/user. | Tuần theo cohort đã chín; Viên | CAC payback, GM | 3 |
| O2 | O | Free AI cost / tổng COGS | Tổng chi phí AI free / (AI paid + AI free + hạ tầng và hỗ trợ trực tiếp); cùng tháng, gồm retry, không gồm marketing hoặc R&D. | Tháng; Viên | GM | 4 |
| O3 | O | Refund rate | Giao dịch thanh toán hoàn tiền toàn phần hoặc một phần trong 30 ngày / giao dịch thành công đã đủ cửa sổ 30 ngày; một giao dịch đếm một lần; loại test và thanh toán thất bại. | Tháng; Viên | GM, tiền thu ròng | 3 |
| G1 | G | Gross margin | (Doanh thu thuần sau refund − toàn bộ COGS kể cả free) / doanh thu thuần; cùng kỳ, loại thuế thu hộ; không dùng doanh thu trước refund. | Tháng; Viên | Kết quả; đối chiếu L3/O2 | 2,4 |

Cây tín hiệu: L2 → O1 → G1; L1 → G1 các tháng tiếp theo; L3 → G1; O2/O3 → G1. Có 3 Leading, 3 Operating, 1 Lagging; L3 là đèn AI. G1 là kết quả đối chiếu, không gán cho nó khả năng dự báo.

## Trạm 3 — Ngưỡng

| ID | Xanh | Vàng | Đỏ | Nguồn | Lý do |
|---|---|---|---|---|---|
| L1 | ≤2 điểm % | >2 đến 5 điểm % | >5 điểm % | [MH] | 200 user: chấp nhận mất tối đa 10 người sau D30; mục tiêu chỉ mất 4. |
| L2 | ≥60% | 40% đến <60% | <40% | [MH] | 100 user/tuần; hỗ trợ được 40 người chưa activation, tối đa 60 khi dành thêm buổi hỗ trợ. |
| L3 | ≤40% | >40% đến 50% | >50% | [MH] | GM mỗi user tối thiểu 40%, chi phí khác 10%: AI tối đa 50%; mục tiêu GM 50% cho nhóm nặng cho trần 40%. |
| O1 | ≥6% | 5% đến <6% | <5% | [MH] | Chi phí thu hút + phục vụ trial 6.000đ; lãi gộp tháng đầu/paid 120.000đ: cần 5%, mục tiêu 6% có dư 20%. |
| O2 | ≤20% | >20% đến 25% | >25% | [MH] | 100 paid: doanh thu 20 triệu, COGS paid 6 triệu; GM 60% cho phép free 2 triệu: 2/(6+2)=25%. |
| O3 | ≤2% | >2% đến 5% | >5% | [MH] | Với giá bằng nhau, ngân sách hoàn tiền mục tiêu 400.000đ/20 triệu =2%; giới hạn rủi ro 1 triệu/20 triệu =5%; giả định thận trọng mỗi refund mất cả giá gói. |
| G1 | ≥60% | 50% đến <60% | <50% | [MH] | Mục tiêu giữ ≥12 triệu trên doanh thu thuần 20 triệu; mức sàn giữ 10 triệu để bù một phần chi phí cố định. |

### Phụ lục [MH]

1. L1: 10/200 ×100 =5 điểm % tối đa; 4/200 ×100 =2 điểm % mục tiêu. Đây là ngân sách mất user giả định, không phải chứng minh đường cong sẽ phẳng. Kiểm tra R30/R60 trên cùng cohort; loại dữ liệu chưa đủ tuổi.
2. L2: (100−40)/100=60% mục tiêu; (100−60)/100=40% tối thiểu. Năng lực hỗ trợ là giả định, cần đo giờ công để hiệu chỉnh.
3. L3: AI tối đa/user =200.000×(1−0,40)−20.000=100.000đ →50% ARPU. Mục tiêu: 200.000×(1−0,50)−20.000=80.000đ →40%. Quota 250×400=100.000đ. Nếu Cost/Job tăng, tính lại quota; p95 không bảo đảm toàn bộ top 5% có lãi.
4. O1: lãi gộp/paid/tháng =200.000×60%=120.000đ; conversion hòa vốn tháng đầu =6.000/120.000=5%; mục tiêu 5%×1,2=6%. Phân bổ free theo kịch bản GM; đối chiếu sổ chi phí để không tính hai lần.
5. O2: trần COGS =20 triệu×(1−60%)=8 triệu; free tối đa=8−6=2 triệu; tỷ trọng free=2/8=25%. Mục tiêu20%: F/(6+F)=0,2 →F=1,5 triệu, GM=62,5%.
6. O3: ngân sách mục tiêu400.000/20 triệu=2%; trần1 triệu/20 triệu=5%. Giả định đồng giá và refund toàn phần cho dự phòng, không phải benchmark ngành.
7. G1: (20−8)/20=60%; giữ tối thiểu10/20=50%. Đây là biên phục vụ, chưa trừ30 triệu chi phí cố định, nên GM xanh không đồng nghĩa công ty có lãi.

Ngưỡng [MH] tính từ đầu vào giả định của bài này. Dự báo 6% chưa phải conversion đã quan sát. Không dùng [BM] nên không có benchmark cần ngày kiểm tra.

## Trạm 4 — Luật

1. ⏹ NẾU L1 >5 điểm % TRÊN 2 cohort liên tiếp đã đủ D60 VÀ mỗi cohort ≥200 user THÌ dừng ads 21 ngày, sửa phiên ôn đầu và nhắc ôn; KHÔNG THÌ không tăng ads để bù người rời.

2. NẾU L3 >50% TRONG 30 ngày VÀ có ≥100 user trả phí THÌ áp quota 250 phiên/tháng, chuyển lượt vượt quota sang gói credit trong 7 ngày; KHÔNG THÌ không tăng giá mọi user. Kiểm tra thêm nhóm top 5% để không bỏ sót đuôi sau p95.

3. NẾU O1 <5% TRÊN 3 cohort trial đã chín VÀ mỗi cohort ≥100 user THÌ thử paywall sau phiên ôn thành công trong 14 ngày; KHÔNG THÌ không giảm giá gói.

4. ⏹ NẾU O2 >25% TRONG 2 tháng liên tiếp VÀ mỗi tháng ≥100 paid THÌ dừng cấp quota free mới, giảm free xuống 3 phiên/tuần trong 7 ngày; KHÔNG THÌ không mở thêm free để lấy lượt đăng ký.

5. NẾU L2 <40% TRONG 2 tuần liên tiếp VÀ mỗi tuần ≥100 user mới THÌ rút onboarding còn chọn chủ đề → ôn 5 câu, thử với 10 người trong 7 ngày; KHÔNG THÌ không thêm tính năng để che lỗi onboarding.

**Người thực hiện:** Viên ghi nhận dữ liệu và bắt đầu hành động trong tuần chỉ số đủ điều kiện đỏ; thời hạn hoàn thành ghi ngay trong từng luật. Luật 1 dừng ads ngay khi kích hoạt, dành21 ngày sửa phiên ôn; luật4 dừng quota mới ngay và hoàn tất chỉnh free trong7 ngày.

Màu đỏ chỉ khởi động luật khi đủ thời gian/mẫu; mẫu thiếu ghi N/A. Không gộp cohort có mức giá hoặc quota khác nhau. O3 đỏ: Viên tổng hợp10 phản hồi hoàn tiền trong7 ngày và sửa lời hứa trên paywall; không bỏ giao dịch refund khỏi số liệu. G1 đỏ: Viên đối soát doanh thu/COGS trong7 ngày, xác định phần AI/free cần cắt theo luật2/4, không tăng ads để bù biên lãi. Đây là cách xử lý bổ sung của thẻ đèn, không thêm luật thứ6.

**Quy ước đo:** các công thức tỷ lệ nhân100 để biểu diễn%; mẫu số0 hoặc cửa sổ chưa đủ thì N/A. p95 nearest-rank là giá trị thứceil(0,95×n) sau khi sắp chi phí tăng dần; chỉ dùng user trả phí có đủ30 ngày. ARPU trong L3 là mức giá giả định200.000đ; nếu giá/doanh thu đổi phải cập nhật mẫu số. L1 ởD60 không thể dự báo conversion đã xảy ra ởD14 của cùng cohort; nó giúp kiểm tra giả định giữ chân cho các cohort tuyển tiếp và GM/gia hạn tương lai.

## Trạm 5 — Cổng gác

| Ngày | Một metric | Ngưỡng | Bằng chứng phải có | Nếu trượt |
|---|---|---|---|---|
| 30 · 08/11/2026 | Số user có bản ghi activation 24h đầy đủ (cả đạt và chưa đạt) | ≥200 | activation_baseline.csv + event_dictionary.md | FIX tracking 30 ngày nếu lỗi log; PIVOT kênh tuyển nếu không tuyển đủ |
| 60 · 08/12/2026 | L1 của cohort ngày khởi động, ≥200 user đủ D60 | ≤5 điểm % | cohort_retention.csv: user ẩn danh, R30, R60, mẫu số cố định | FIX phiên ôn 30 ngày nếu rõ lỗi; PIVOT nếu nhu cầu sai; KILL nếu đã FIX vẫn >5 |
| 90 · 07/01/2027 | O1 trên ≥100 trial cùng phiên bản đã đủ 14 ngày | ≥5% | trial_paid.csv + payment_reconciliation.csv | FIX paywall 30 ngày nếu chưa sửa; PIVOT nếu sai người trả; KILL nếu đã FIX vẫn <5% |

GO khi đạt ngưỡng và đủ mẫu → sang chặng sau; FIX 30 ngày, sửa đúng một việc nếu biết lỗi và chưa FIX; PIVOT khi giả định gốc sai; KILL khi đã FIX một lần mà vẫn không đạt (không FIX lần hai); thiếu mẫu ghi N/A, dừng tăng chi tiền và PIVOT kênh tuyển, không kết luận retention/conversion. Ghi quyết định và lần FIX trong decision_log.md. Các file bằng chứng là đầu ra tương lai, chưa tồn tại. Mốc tính từ09/10/2026 +30/+60/+90 ngày. Cổng30 lấy200 bản ghi để tính baseline activation (kể cả user chưa activation), không phải200 người activation thành công; cổng60 dùng trần mất10/200=5 điểm %; cổng90 dùng conversion hòa vốn6.000/120.000=5%.

**KILL CRITERIA:** Đến 07/01/2027, nếu O1 vẫn <5% trên ≥100 trial cùng phiên bản đủ14 ngày sau đúng một lần FIX paywall thì em dừng hẳn thử nghiệm thuê bao ÔnNhớ AI và ngừng chi tiền thu hút người dùng cho hướng này.

**CHƯA ĐO ĐƯỢC:** Cả 7 đèn chưa đo (🔧/❌ Trạm 1): L2 cần signup/completed/viewed, dự kiến 23/10/2026; O1 cần trial/billing đủ14 ngày, 08/11/2026; L3 cần AI ledger paid đủ30 ngày, O3 cần refund đủ30 ngày, 08/11/2026; O2/G1 cần sổ COGS free/paid và doanh thu thuần 2 kỳ, 08/12/2026; L1 cần cohort ≥200 đủD60, 08/12/2026. Tất cả là lịch dự kiến nếu đủ mẫu; chưa có log thật. M12 chưa chọn vào dashboard, sớm nhất09/10/2027.
