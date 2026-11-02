# Cổng Nền tảng số pháp luật Việt Nam – Bản thiết kế demo

> **Đây là bản thiết kế demo, không phải cổng chính thức của Bộ Tư pháp.** Số liệu, tên người và hồ sơ trên giao diện đều là dữ liệu minh họa.

**Xem giao diện:** https://linhmy2001.github.io/cong-ntspl-demo/

---

## 1. Bối cảnh

Nền tảng số pháp luật Việt Nam gồm nhiều phần mềm nghiệp vụ chạy riêng lẻ. Mỗi phần mềm có màn hình, tài khoản và danh sách công việc riêng. Cán bộ phải mở từng phần mềm mới biết mình đang có việc gì và số liệu từng mảng ra sao.

Đơn vị CNTT muốn có một **cổng truy cập tập trung**: người dùng đăng nhập một lần, thấy ngay số liệu chính của mọi nghiệp vụ trên một màn hình, rồi đi thẳng vào hồ sơ cần xử lý.

Bản demo này là thiết kế sơ bộ để các bên góp ý trước khi chốt yêu cầu.

## 2. Mục tiêu

| Mục tiêu | Cách giao diện đáp ứng |
|---|---|
| Truy cập tập trung | Một cổng chung, đăng nhập một lần (SSO) vào các phần mềm |
| Theo dõi nhanh | Mỗi nghiệp vụ có một thẻ số liệu, xem được ngay trên trang chủ |
| Đi thẳng vào việc | Bấm số liệu thì ra danh sách chi tiết. Bấm một hồ sơ thì mở đúng hồ sơ đó trên phần mềm gốc |
| Cá nhân hóa | Thứ tự thẻ và nhãn "Của tôi" thay đổi theo vai trò người dùng |

## 3. Các phần mềm được tích hợp

| # | Phần mềm | Nghiệp vụ chính |
|---|---|---|
| 1 | Phần mềm quản lý chương trình xây dựng VBQPPL | Chương trình lập pháp, các bước xây dựng văn bản từ soạn thảo đến ban hành |
| 2 | Phần mềm hỗ trợ dự thảo VBQPPL | Soạn thảo trực tuyến, góp ý, tiếp thu, giải trình |
| 3 | Cơ sở dữ liệu quốc gia về pháp luật | Khai thác, biên tập văn bản, văn bản hợp nhất, pháp điển |
| 4 | Phần mềm hỗ trợ theo dõi thi hành VBQPPL | Kế hoạch triển khai thi hành, vướng mắc, phản ánh, kiến nghị |
| 5 | Phần mềm hỗ trợ kiểm tra, rà soát VBQPPL | Kiểm tra, rà soát, hệ thống hóa văn bản |

Cổng được xây dựng trên Hệ thống quản trị nền tảng số pháp luật Việt Nam. Hệ thống này quản lý người dùng, đồng bộ tài khoản sang các phần mềm và xác thực đăng nhập.

## 4. Cấu trúc giao diện: 2 lớp

```
┌──────────────────────────────────────────────────────────────┐
│ BANNER: Logo · NỀN TẢNG SỐ PHÁP LUẬT VIỆT NAM · Tài khoản SSO │
│ Ô tìm kiếm chung trên tất cả phần mềm                         │
├───────────────┬──────────────────────────────────────────────┤
│ Phần mềm      │ LỚP 1 – TỔNG QUAN                             │
│ nghiệp vụ     │  • Biểu đồ tổng hợp                           │
│ (5 lối vào)   │  • Số liệu theo nghiệp vụ (6 thẻ)             │
│               │  • Tiến trình xây dựng VBQPPL (7 bước)        │
│ Tra cứu       │  • Tiện ích Không gian làm việc số            │
│ CSDLQG        │                                               │
│               │        │ bấm vào một con số                   │
│               │        ▼                                      │
│               │ LỚP 2 – DANH SÁCH CHI TIẾT                    │
│               │  • Tab trạng thái · bộ lọc · bảng hồ sơ        │
│               │  • "Xử lý ↗" mở đúng hồ sơ trên phần mềm gốc   │
└───────────────┴──────────────────────────────────────────────┘
```

### Lớp 1 – Tổng quan

**a) Biểu đồ tổng hợp**

| Biểu đồ | Dạng | Ý nghĩa |
|---|---|---|
| Văn bản QPPL cập nhật vào CSDLQG theo tháng | Đường | Biến động số văn bản mới trong 12 tháng gần nhất |
| Dự thảo VBQPPL theo trạng thái | Vành khuyên | Tỷ lệ dự thảo Đang soạn thảo / Đã hoàn thành / Đã ban hành |

**b) Số liệu theo nghiệp vụ**

| Thẻ | Các chỉ số |
|---|---|
| Chương trình xây dựng VBQPPL | Nhiệm vụ trong Chương trình lập pháp năm · VB quy định chi tiết cần ban hành · VB quy định chi tiết nợ ban hành · VB quy định chi tiết đã ban hành |
| Hỗ trợ dự thảo VBQPPL | Đang soạn thảo · Đã hoàn thành · Đã ban hành · Góp ý chờ tiếp thu, giải trình |
| Kiểm tra VBQPPL | Chờ kiểm tra · Đang kiểm tra · Đã kiểm tra · Trái pháp luật – có kết luận |
| Rà soát, hệ thống hóa VBQPPL | Cần rà soát · Đã rà soát · Cần sửa đổi, bổ sung, thay thế, bãi bỏ · Hết hiệu lực, tạm ngưng đã công bố |
| Theo dõi thi hành VBQPPL | Kế hoạch triển khai thi hành · Đề nghị hướng dẫn, vướng mắc chờ xử lý · Phản ánh, kiến nghị · Kết luận kiểm tra thi hành |
| CSDL quốc gia về pháp luật | Văn bản QPPL trong CSDL · Văn bản hợp nhất · VB chuyển đến chờ tiếp nhận · Đề mục pháp điển đang thực hiện |

Số màu đỏ là số cần chú ý, ví dụ văn bản nợ ban hành, vướng mắc chờ xử lý, văn bản trái pháp luật.

**c) Tiến trình xây dựng VBQPPL:** số nhiệm vụ ở từng bước: Soạn thảo → Lấy ý kiến, tham vấn → Thẩm định → Trình Chính phủ → Thẩm tra → Thông qua → Ban hành.

**d) Tiện ích Không gian làm việc số** *(đề xuất bổ sung, chưa có trong yêu cầu gốc)*: văn bản điện tử, lịch công tác, họp trực tuyến, hộp thư công vụ, ký số, trợ lý pháp luật, tài liệu của tôi, hỗ trợ.

### Lớp 2 – Danh sách chi tiết

- Mở ra khi bấm vào bất kỳ con số nào ở Lớp 1.
- Có tab để chuyển giữa các trạng thái trong cùng nghiệp vụ.
- Bảng gồm các cột: số/ký hiệu, tên văn bản, cơ quan, cấp, ngày, trạng thái, hạn xử lý.
- Nút **"Xử lý ↗"** mở đúng hồ sơ trên phần mềm nghiệp vụ qua SSO, không phải đăng nhập lại.

## 5. Căn cứ nghiệp vụ

Các chỉ số được đối chiếu với **Phụ lục 1 – Danh sách yêu cầu của người sử dụng** (tài liệu thiết kế cơ sở Nền tảng số PLVN, phiên bản 1.1). Một số căn cứ chính:

| Nội dung trên giao diện | Căn cứ trong Phụ lục 1 |
|---|---|
| Trạng thái dự thảo: Đang soạn thảo / Đã hoàn thành / Đã ban hành | PM Hỗ trợ dự thảo – YC19 (cập nhật trạng thái soạn thảo) |
| Các bước xây dựng VBQPPL | PM Quản lý chương trình – mục VII.8 đến VII.14 |
| Đã kiểm tra, trái pháp luật | PM Kiểm tra, rà soát – thống kê YC87, YC88 |
| Đã rà soát | PM Kiểm tra, rà soát – thống kê YC90 |
| Vướng mắc chờ xử lý / đã xử lý | PM Theo dõi thi hành – YC70 |
| Biểu đồ biến động văn bản | CSDLQG – YC46, YC50 |
| Cơ quan, cá nhân làm công tác pháp chế; người sử dụng | Hệ thống quản trị – dashboard YC94, YC95, YC96 |
| Đăng nhập một lần | Hệ thống quản trị – YC1; API xác thực YC46, YC47 |

## 6. Ràng buộc và vấn đề cần chốt

**Ràng buộc đã biết:**
- CSDLQG và Pháp điển **không áp dụng KPI**, nên không có cảnh báo quá hạn cho hai mảng này.
- Pháp điển **chưa có phạm vi chia sẻ API**. Số liệu pháp điển hiện chỉ để minh họa và cần xác nhận lại.
- Phần mềm Hỗ trợ dự thảo **không có API chia sẻ riêng**. Trạng thái được đồng bộ qua phần mềm Quản lý chương trình.

**Câu hỏi cần các bên trả lời:**
1. Phụ lục 1 **không có khái niệm hạn xử lý hay quá hạn**. Có giữ cột "Hạn xử lý" ở Lớp 2 không? Nếu giữ, hạn được tính từ đâu?
2. Các giá trị trạng thái của Kiểm tra (chờ / đang / đã kiểm tra) và Rà soát (chưa / đã rà soát) chưa được liệt kê trong Phụ lục 1. Đơn vị phát triển phần mềm cần xác nhận.
3. Trạng thái ý kiến góp ý trên dự thảo không thống nhất giữa YC124 (Mới / Đã xem / Đã phản hồi) và YC127 (Đang xem xét / Đã xử lý / Từ chối). Cần chọn một bộ.
4. Mỗi phần mềm có cung cấp được **mẫu đường dẫn mở thẳng một hồ sơ** cho nút "Xử lý ↗" không?
5. Các tiện ích Không gian làm việc số có nằm trong phạm vi dự án không?

## 7. Về bản demo này

| Mục | Mô tả |
|---|---|
| Trạng thái | Thiết kế sơ bộ, dùng để lấy góp ý |
| Dữ liệu | Toàn bộ là số liệu minh họa, chưa kết nối phần mềm thật |
| Vai trò mặc định | Cán bộ pháp chế |
| Thiết bị | Thiết kế cho màn hình máy tính (khung 1440px) |
| Công nghệ | Một file HTML duy nhất (`index.html`), không cần máy chủ riêng |

---

*Bản demo do nhóm phân tích nghiệp vụ FIS chuẩn bị để phục vụ trao đổi với Bộ Tư pháp.*
