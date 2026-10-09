# Kiểm tra bài Day 23

Học viên: Dương Thị Hồng Viên · MSSV: 2A202602385.

- [x] Repo cá nhân tên `K4-L3-DAY23-DuongThiHongVien-2A202602385-AIProductGrowth` đã push lên tài khoản hviennduongne; kiểm tra API GitHub không đăng nhập xác nhận public. Origin là repo cá nhân, upstream là repo đề bài; chưa kiểm tra bằng cửa sổ ẩn danh của trình duyệt.
- [x] Có README.md, worksheet.md, dashboard.md, dashboard.pdf. PDF trang 1 chứa toàn bộ dashboard, trang 2 chứa phụ lục [MH].
- [x] Ba bảng Leading/Operating/Lagging; 7 đèn, ≥2 Leading, 1 đèn chi phí AI, chỉ 1 Lagging.
- [x] Từng ngưỡng có [MH] và lý do; 7 phép tính trong worksheet và phụ lục PDF. Đầu vào giả định được ghi rõ.
- [x] Không sử dụng [BM]; mục ngày kiểm tra benchmark không áp dụng.
- [x] 5 luật có NẾU, TRONG/TRÊN, THÌ, KHÔNG THÌ; 2 luật dừng đánh dấu ⏹ trong Markdown và [DỪNG] trong PDF.
- [x] 3 cổng có một metric quyết định, ngưỡng số, bằng chứng cần thu thập và lựa chọn nếu trượt; ngày 30 là cổng học. Điều kiện mẫu là điều kiện đủ tin cậy, không phải metric thứ hai.
- [x] FIX tối đa một lần/vấn đề; thiếu mẫu không được kết luận conversion/retention. Kill criteria có ngưỡng 5%, mẫu ≥100 và ngày 07/01/2027.
- [x] CHƯA ĐO ĐƯỢC nêu đủ 7 đèn, dữ liệu cần có và ngày dự kiến. File log người dùng ở các cổng là bằng chứng tương lai, chưa tồn tại.
- [x] Nội dung bài dùng số giả định, không đưa API key, token hay dữ liệu khách hàng vào các file nộp.
- [ ] Dán link repo lên LMS. Repo: https://github.com/hviennduongne/K4-L3-DAY23-DuongThiHongVien-2A202602385-AIProductGrowth ; chưa nộp LMS.

## Cách xuất bản in

`dashboard.md` là bản nguồn nội dung. `python scripts/build_lab.py` xuất cùng nội dung thành trang 1 của dashboard.pdf và thêm phụ lục ở trang 2, theo khổ A4. Bố cục của Markdown Preview/GitHub phụ thuộc trình xem và cài đặt in; dùng PDF đã kiểm tra để giữ bản một trang thống nhất.

Kết quả kiểm tra tự động nằm trong validation.json. Kiểm tra bố cục thực hiện bằng cách render và xem ảnh cả hai trang PDF.
