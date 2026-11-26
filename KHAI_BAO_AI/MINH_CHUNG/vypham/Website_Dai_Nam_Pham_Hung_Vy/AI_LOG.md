# AI_LOG - Rà soát toàn bộ mã nguồn

Ngày kiểm tra: 23/11/2026

Phạm vi kiểm tra:
- `index.html`
- `style.css`
- `README.md`
- `CHANGELOD.md`

Tình trạng: Đã rà soát xong. Chưa sửa mã nguồn.

## Tổng quan

- Tổng số lỗi/điểm vi phạm đã phát hiện: 10
- Mức nghiêm trọng Cao: 3
- Mức nghiêm trọng Trung bình: 5
- Mức nghiêm trọng Thấp: 2

## Lỗi nghiêm trọng

### [Cao] FORM-001 - Form liên hệ không gửi được dữ liệu
- Tệp: `index.html`
- Vị trí: thẻ `<form>` trong phần Liên hệ.
- Mô tả: Form không có `action`, không có `method` và nút sử dụng `type="button"` thay vì `submit`.
- Hậu quả: Người dùng nhập thông tin nhưng không có dữ liệu được gửi đi; nút không thực hiện tác vụ nào.
- Khuyến nghị: Thêm xử lý gửi form bằng JavaScript hoặc cấu hình backend, đổi nút thành `type="submit"` và xử lý sự kiện submit. Nếu giữ trang tĩnh, thêm liên kết email/tel hoặc dịch vụ form hợp lệ.

### [Cao] FORM-002 - Thiếu thuộc tính dữ liệu và validation bắt buộc
- Tệp: `index.html`
- Vị trí: các thẻ `<input>` và `<textarea>`.
- Mô tả: Các trường không có thuộc tính `name`, `required`, hoặc quy tắc `pattern/minlength`; không khai báo trạng thái hợp lệ của dữ liệu.
- Hậu quả: Không thể đọc hoặc gửi dữ liệu bởi backend; trình duyệt không kiểm tra bắt buộc nhập và định dạng email/điện thoại.
- Khuyến nghị: Thêm `name`, `required`, `autocomplete`, `type="email"`, và quy tắc hợp lệ phù hợp cho từng trường.

### [Cao] DOC-001 - Tài liệu README chứa tên và cấu trúc thư mục sai
- Tệp: `README.md`
- Vị trí: mục 4, mục cấu trúc thư mục.
- Mô tả:
  - README ghi tên thư mục dự án là `BAI TAP LON THIET KE WEBSITE/`, trong khi thư mục thực tế có tên `bai tap lon thiet ke ưebsite`.
  - README ghi file `CHANGELOG.md`, nhưng tên file hiện tại là `CHANGELOD.md`.
- Hậu quả: Người đọc có thể không tìm thấy nhật ký thay đổi hoặc làm theo sai cấu trúc thư mục.
- Khuyến nghị: Đồng nhất tên thư mục và tên file thực tế; nên đổi `CHANGELOD.md` thành `CHANGELOG.md` nếu đây là lỗi chính tả.

## Lỗi trung bình

### [Trung bình] A11Y-001 - Các ô nhập liệu thiếu nhãn truy cập
- Tệp: `index.html`
- Vị trí: form liên hệ.
- Mô tả: Các trường chỉ dùng `placeholder`; không có thẻ `<label>` hoặc thuộc tính `aria-label/aria-labelledby`.
- Hậu quả: Placeholder có thể biến mất khi nhập, gây khó hiểu cho người dùng; hỗ trợ công nghệ trợ năng không chắc nhận diện đúng mục đích của từng trường.
- Khuyến nghị: Thêm `<label>` liên kết bằng `for/id` cho từng trường, đồng thời có thể giữ placeholder làm gợi ý bổ sung.

### [Trung bình] A11Y-002 - Thiếu liên kết bỏ qua phần điều hướng
- Tệp: `index.html`
- Vị trí: mở đầu `<body>`, trước `<header>`.
- Mô tả: Không có liên kết “Skip to content” để bàn phím bỏ qua menu và đi thẳng đến nội dung chính.
- Hậu quả: Người dùng chỉ dùng bàn phím hoặc công nghệ trợ năng phải duyệt nhiều phần điều hướng lặp lại.
- Khuyến nghị: Thêm liên kết skip có thể focus, trỏ tới `<main id="main-content">`.

### [Trung bình] A11Y-003 - Trạng thái focus liên kết/chức năng chưa rõ
- Tệp: `style.css`
- Vị trí: quy tắc `a`, `nav a`, `.button`, `.major-card a`, `footer a`, `form button`.
- Mô tả: Chỉ khai báo `:hover`; chưa có quy tắc `:focus-visible` thống nhất cho các liên kết và nút.
- Hậu quả: Người dùng bàn phím khó nhận biết phần tử đang được focus.
- Khuyến nghị: Thêm `:focus-visible` với outline/box-shadow rõ ràng, không phụ thuộc vào màu nền.

### [Trung bình] HTML-001 - Không có cảnh báo/action hiển thị sau khi gửi form
- Tệp: `index.html`
- Vị trí: nút `Gửi thông tin`.
- Mô tả: Nút là `type="button"` không có listener hoặc thông báo phản hồi, nên không có UX sau khi thao tác.
- Hậu quả: Người dùng không biết liệu thông tin đã được gửi hay chưa.
- Khuyến nghị: Thêm trạng thái loading/thành công/thất bại hoặc chuyển sang cơ chế liên hệ thật.

### [Trung bình] UX-001 - Banner dính sang điện thoại ở một số kích thước tablet
- Tệp: `style.css`
- Vị trí: media query `@media (max-width: 900px)`.
- Mô tả: `banner` vẫn dùng hai cột đến `600px`; ở chiều rộng tablet hẹp, nội dung và khung hình có thể bị ép chật.
- Hậu quả: Văn bản/banner hình ảnh có thể tràn, xuống dòng nhiều hoặc mất cân đối.
- Khuyến nghị: Kiểm tra thực tế ở khoảng 601–900px; chuyển banner sang một cột sớm hơn nếu layout bị chật.

## Lỗi thấp

### [Thấp] A11Y-004 - Biểu tượng emoji có thể được đọc như ký tự
- Tệp: `index.html`
- Vị trí: icon ngành học `💻`, `📊`, `🌍` và các biểu tượng địa chỉ liên hệ.
- Mô tả: Emoji mang tính trang trí nhưng không có `aria-hidden="true"`; screen reader có thể đọc tên emoji.
- Hậu quả: Bị đọc thừa thông tin không cần thiết.
- Khuyến nghị: Thêm `aria-hidden="true"` cho icon trang trí hoặc thay bằng SVG/icon font có nhãn rõ ràng.

### [Thấp] SEO-001 - Thiếu mô tả trang và dữ liệu Open Graph
- Tệp: `index.html`
- Vị trí: phần `<head>`.
- Mô tả: Chỉ có `<title>` và charset/viewport; thiếu `<meta name="description">` và thẻ Open Graph cơ bản.
- Hậu quả: Mô tả khi chia sẻ hoặc xuất hiện trên công cụ tìm kiếm có thể kém rõ ràng.
- Khuyến nghị: Thêm `description`, `canonical` và các thẻ Open Graph như `og:title`, `og:description`, `og:image`.

## Danh sách kiểm tra đã xác nhận hoạt động

- Tất cả đường neo trong menu trỏ tới ID hiện có trong trang.
- Các nguồn ảnh được tham chiếu tồn tại trong thư mục dự án:
  - `Logo-DH-Dai-Nam-.webp`
  - `anh chinh.jpg`
  - `anh2.webp`
  - `anh3.jpg`
  - `anh4.jpg`
  - `anh5.jpg`
- Thẻ `<meta name="viewport">` đã được khai báo.
- Liên kết website bên ngoài có `target="_blank"` và `rel="noopener noreferrer"`.
- CSS có bố cục cho tablet và điện thoại.