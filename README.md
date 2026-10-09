# Day 23 — ÔnNhớ AI
Học viên: **Dương Thị Hồng Viên** · MSSV: **2A202602385** · Ngày làm: 09/10/2026.
Mô hình B2C: cá nhân tự trả tiền và tự dùng web ôn tập; chưa có khách hoặc dữ liệu vận hành thật.
Bài làm: [worksheet](worksheet.md), [dashboard](dashboard.md), [PDF](dashboard.pdf), [AI Log](AI_LOG.md), [kết quả kiểm tra](evidence/validation.json).
Tên repo khi nộp: `K4-L3-DAY23-DuongThiHongVien-2A202602385-AIProductGrowth`. Repo cá nhân: https://github.com/hviennduongne/K4-L3-DAY23-DuongThiHongVien-2A202602385-AIProductGrowth · Chưa nộp LMS.

## Phạm vi và tài liệu
Tôi giữ tài liệu gốc trong folder. Slide `D:/AIthucchien/track1/day7.pdf` ghi Day 26, nhưng README/HANDBOOK xác nhận bài trong repo là Day 23 theo cách đánh số của lớp. Tôi dùng yêu cầu repo để chốt đầu ra.
Em chọn sản phẩm ÔnNhớ AI và số liệu giả định để thực hành Day 23. Day 24–25 là nội dung trong lộ trình chưa được học; các đầu vào dưới đây được đặt ngay trong bài này, chưa phải số thực đo.

- Sản phẩm: ÔnNhớ AI, tạo phiên ôn 5 câu kèm giải thích từ ghi chú; cá nhân tự mua và dùng trên web → B2C.
- Value metric: thuê bao 200.000đ/tháng, quota dự kiến 250 phiên; credit riêng cho phần vượt. Free ban đầu 5 phiên/tuần.
- Cost/Job giả định: 400đ/phiên gồm cả retry trung bình; nhóm paid thông thường 100 phiên/tháng → AI 40.000đ; chi phí phục vụ khác 20.000đ/paid/tháng.
- Kịch bản 100 paid: doanh thu thuần 20 triệu, paid COGS 6 triệu, ngân sách free 2 triệu → tổng COGS 8 triệu, GM 60%. Quy mô và giá trị này chưa đo.
- Chi phí mỗi trial (marketing + free trong trial) 6.000đ; không cộng lại khoản này vào CAC một lần nữa. Chi phí R&D/nhân sự cố định 30 triệu/tháng; tiền mặt 180 triệu → runway kịch bản không thu tiền 6 tháng, không phải runway đã kiểm toán.
- CAC kỳ vọng ở conversion 6% = 6.000/0,06 =100.000đ; payback theo GM bình quân 60% =100.000/120.000=0,833 tháng. Mục tiêu ≤1 tháng. Không ước tính LTV khi chưa có lịch sử retention.
- Tất cả ngưỡng dùng [MH] từ giả định, không dùng [BM], không có baseline [TB] thực đo. Màu hiện tại luôn N/A, không gán xanh cho số chưa có.

## Tái tạo và kiểm tra
Chạy `python scripts/build_lab.py` với Python có reportlab và pypdf. Script dựng các tài liệu, kiểm tra phép tính/boundary và ghi kết quả vào evidence/validation.json. Đây là kiểm tra bài làm trên số giả định, không phải chạy thử app hay đo user thật. PDF trang 1 là dashboard; trang 2 là phép tính.
