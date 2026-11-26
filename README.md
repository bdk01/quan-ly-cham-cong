# Ứng dụng Web Quản lý Chấm công & Tính lương

## 1. Cách chạy trực tiếp trên máy
1. Giải nén file `web_cham_cong_tinh_luong.zip`.
2. Mở file `index.html` (hoặc `cham_cong_tinh_luong.html`) bằng trình duyệt bất kỳ (Chrome, Edge, Safari, Firefox).

## 2. Cách xuất bản lấy link online miễn phí
- **Netlify Drop:** Truy cập https://app.netlify.com/drop và kéo thả thư mục đã giải nén (hoặc file `.zip`) vào trang để nhận link HTTPS ngay lập tức.
- **GitHub Pages / Vercel:** Đẩy thư mục chứa `index.html` lên repository và bật Pages/Deploy.

## 3. Tính năng chính
- Đồng hồ thời gian thực (`dd/mm/yyyy` & `hh:mm:ss`).
- 3 chế độ khung giờ: Ca cố định 1 (`20:00 - 01:00`), Ca cố định 2 (`19:00 - 01:00`), và Khung giờ tự chọn (`hh:mm`).
- Đơn giá mặc định `40.000 VNĐ/h` (có thể tùy chỉnh).
- Lịch tháng tương tác có dấu tick xanh (`✓`) trên các ngày đã làm việc.
- Bảng kê chi tiết có bộ lọc theo tháng và hàng `TOTAL THÁNG` tự động cộng dồn.
- Lưu trữ tự động trên trình duyệt, xuất Excel (CSV), sao lưu/khôi phục JSON và đồng bộ trực tuyến qua Google Drive.

## 4. Đồng bộ Google Drive trên laptop và điện thoại

1. Deploy thư mục chứa `index.html`. Với GitHub Pages, vào **Settings → Pages** và chọn nhánh chứa file, thư mục **/ (root)**.
2. Trong [Google Cloud Console](https://console.cloud.google.com/apis/library/drive.googleapis.com), tạo project và bật **Google Drive API**.
3. Trong **Google Auth Platform**, cấu hình **Branding** và **Audience**. Với Gmail cá nhân, chọn **External**. Nếu ứng dụng ở chế độ **Testing**, thêm Gmail của bạn vào **Test users**. Trong **Data Access**, thêm scope `https://www.googleapis.com/auth/drive.appdata`.
4. Trong **Clients**, tạo OAuth Client ID loại **Web application**. Thêm origin của web vào **Authorized JavaScript origins**. Ví dụ, với `https://ten-github.github.io/cham-cong/`, nhập `https://ten-github.github.io`. Giữ Client Secret và access token ngoài repo.
5. Client ID của bản GitHub Pages đã được đặt trong hằng `DRIVE_CLIENT_ID` trong hai file HTML. Trên web, bấm **Kết nối Google Drive**, chọn tài khoản Google và cấp quyền. Khi đã kết nối, nút đổi thành **Đăng xuất Google Drive**. Đăng xuất kết thúc phiên Drive của tab và giữ dữ liệu cục bộ.
6. Nếu Drive chưa có bản chấm công và máy có dữ liệu, web sẽ hỏi có muốn lưu bản đầu tiên lên Drive. Dùng cùng tài khoản Google trên các thiết bị còn lại để tải bản đó. Với dữ liệu từ bản HTML cũ hoặc một file JSON tải xuống từ Drive, dùng **Nhập JSON** trên thiết bị chứa bản chính trước khi lưu lên Drive.

Web tự lưu khi thêm, sửa hoặc xóa ca và phiên Google còn hiệu lực. Nếu vừa kết nối trên trình duyệt trống với tài khoản Drive chưa có dữ liệu, ca đầu tiên tự tạo file trên Drive. Mỗi tài khoản Google có dữ liệu riêng. Khi quay lại tab hoặc có mạng trở lại, web kiểm tra bản mới. Bạn có thể lấy dữ liệu ngay bằng **Refresh dữ liệu**. Tải lại trang trong cùng tab sẽ tiếp tục phiên Google nếu phiên còn hạn. Khi phiên hết hạn hoặc mở tab mới chưa có phiên, bấm **Kết nối Google Drive**.

Nếu cả bản trên máy và Drive đã thay đổi, web báo xung đột. Xuất JSON của bản trên máy trước khi tải bản Drive. Sau đó có thể nhập gộp để lấy lại các ca mới hoặc sửa lại các ca chồng nhau. Khi dùng nhiều máy, đợi báo đã lưu lên Drive rồi mới chuyển máy, vì kiểm tra phiên bản trước khi ghi vẫn có thể gặp hai lần ghi đồng thời.
