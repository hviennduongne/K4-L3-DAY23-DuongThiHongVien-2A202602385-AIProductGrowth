# AI Log & Reflection — Day 23

**Họ tên:** Dương Thị Hồng Viên  
**MSSV:** 2A202602385  
**Ngày làm:** 09/10/2026

## 1. Cách em tiếp cận bài

Sau khi đọc lý thuyết, em hiểu bài này cần chọn những chỉ số giúp phát hiện vấn đề sớm và viết sẵn cách xử lý. Nếu chỉ nhìn doanh thu thì có thể đến lúc doanh thu giảm mới biết người dùng đã bỏ sản phẩm từ trước.

Em dùng tình huống ÔnNhớ AI, một sản phẩm tạo câu hỏi ôn tập từ ghi chú. Em chọn B2C vì người học tự trả tiền và trực tiếp sử dụng. Sản phẩm và số liệu trong bài là giả định để thực hành. Các nội dung tài chính và Cost/Job được nhắc trong lộ trình Day 24–25 chưa được học, nên ở bài này em ghi rõ đầu vào giả định và trình bày phép tính để giải thích ngưỡng.

## 2. Quá trình làm bài

Em chia bài theo 5 trạm trong hướng dẫn. Đầu tiên là chốt mô hình B2C, sau đó chọn 7 chỉ số gồm 3 chỉ số báo sớm, 3 chỉ số vận hành và 1 chỉ số kết quả. Em chọn mức giảm retention từ D30 đến D60 làm chỉ số chính, vì cần biết người dùng có tiếp tục ôn tập hay không.

Ở phần định nghĩa, em ghi rõ người dùng hoạt động phải hoàn thành ít nhất một phiên ôn 5 câu. Chỉ mở ứng dụng thì chưa tính. Với activation, người dùng còn phải xem phần giải thích trong 24 giờ đầu. Cách ghi này giúp tránh trường hợp mỗi lần đo lại hiểu “hoạt động” theo một kiểu khác nhau.

Phần đặt ngưỡng khó hơn phần chọn chỉ số. Em dùng kịch bản 100 người trả phí, giá 200.000đ/tháng, tạo ra 20 triệu đồng doanh thu. Chi phí phục vụ nhóm trả phí là 6 triệu đồng. Nếu muốn biên lãi gộp 60% thì tổng chi phí phục vụ chỉ được đến 8 triệu đồng. Như vậy phần miễn phí còn ngân sách 2 triệu đồng, bằng 25% tổng chi phí. Em dùng phép tính này để đặt ngưỡng đỏ cho chi phí free, thay vì chọn một tỷ lệ chỉ vì thấy có trong slide.

Tiếp theo, em viết 5 luật theo mẫu NẾU – TRONG/TRÊN – THÌ – KHÔNG THÌ. Em đặt thêm điều kiện số lượng người dùng để tránh phản ứng quá mạnh với mẫu nhỏ. Hai luật dừng là dừng quảng cáo khi retention xấu và dừng cấp thêm quota miễn phí khi chi phí free vượt trần.

Cuối cùng, em đặt các mốc ngày 30, 60 và 90. Ngày 30 tập trung vào việc có dữ liệu activation; ngày 60 kiểm tra retention; ngày 90 kiểm tra tỷ lệ dùng thử chuyển sang trả phí. Mỗi mốc chỉ có một chỉ số quyết định để dễ kiểm tra đạt hay chưa đạt.

## 3. Chỗ vướng và cách sửa

Một chỗ phải sửa là cửa sổ đo retention. Bản đầu dùng D57–63, nhưng đến ngày 60 thì chưa thể có dữ liệu của ngày 63. Sau khi rà lại, em đổi thành D54–60 và dùng nhóm đăng ký đúng ngày bắt đầu cho cổng ngày 60.

Em cũng cần phân biệt chi phí AI trung bình với chi phí của nhóm dùng nhiều. Nếu chỉ nhìn trung bình, một số người dùng quá nhiều có thể làm mất lãi mà bảng vẫn trông ổn. Vì vậy em giữ chỉ số p95 và thêm việc kiểm tra nhóm top 5% khi chi phí vượt ngưỡng.

Phần chi phí dùng thử và chi phí miễn phí dễ bị cộng hai lần. Trong bài, em ghi chú cần phân bổ từ cùng một sổ chi phí. Các phép tính hiện dùng số giả định; khi có dữ liệu thực tế thì phải đối chiếu lại phần này.

## 4. Em sử dụng AI như thế nào

Em dùng AI hỗ trợ giải thích ba tầng chỉ số, gợi ý cách trình bày thẻ đèn và soạn bản nháp các luật. AI cũng hỗ trợ rà phép tính, điều kiện mẫu và những hành động không nên làm khi chỉ số xấu.

Phần xuất PDF và script kiểm tra có AI hỗ trợ viết. Nhờ đó, bài có thể kiểm tra lại số trang, thông tin học viên và các phép tính. Nội dung AI Log cũng được hỗ trợ diễn đạt từ quá trình làm bài. Những số về người dùng và doanh thu trong bài vẫn là giả định, không phải dữ liệu AI tìm được hay kết quả khảo sát.

## 5. Kết quả kiểm tra

Script `scripts/build_lab.py` đã chạy thành công. Sau khi rà checklist Trạm 5, bộ kiểm tra được bổ sung để kiểm tra ba bảng đèn, ba cổng có ngưỡng số, ngày 30 là cổng học, quy định FIX một lần và mục chưa đo đủ 7 đèn. Kết quả của lần chạy cuối được lưu trong `evidence/validation.json`.

PDF có đúng 2 trang: trang đầu là dashboard, trang sau là giả định và phép tính. Sau khi xuất PDF, cả hai trang đã được chuyển thành ảnh để kiểm tra bố cục; không thấy bảng chồng lên nhau hoặc nội dung bị cắt. Bản cuối đã được dựng lại sau khi sửa cửa sổ retention.

Khi rà lại Trạm 5, em tách bảng đèn thành ba tầng và sửa quyết định ở cổng ngày 60 cho rõ: biết lỗi thì FIX, sai giả định thì PIVOT, đã FIX mà vẫn không đạt thì KILL. Em cũng thêm mẫu tối thiểu vào cổng ngày 90 và rút kill criteria thành một câu có số và ngày.

Kết quả kiểm tra trên là kiểm tra tài liệu và phép tính. Các chỉ số hiện tại vẫn để N/A vì bài chưa có dữ liệu người dùng thực tế. Các luật xử lý và cổng 90 ngày là kế hoạch vận hành cho tình huống này.

## 6. Điều em rút ra

Qua bài này, em hiểu hơn vì sao cần ghi cả định nghĩa và hành động cho từng chỉ số. Trước đó em nghĩ dashboard chủ yếu là một bảng để xem số. Khi làm phần luật, em thấy bảng chỉ có ích nếu nhìn vào đó biết bước tiếp theo cần làm gì.

Phần em cần luyện thêm là đặt ngưỡng. Một con số có vẻ hợp lý chưa chắc phù hợp với chi phí của sản phẩm. Sau khi học thêm phần tài chính và Cost/Job, em sẽ quay lại kiểm tra các giả định trong bài, nhất là giá gói, chi phí mỗi phiên ôn và ngân sách cho người dùng miễn phí.
