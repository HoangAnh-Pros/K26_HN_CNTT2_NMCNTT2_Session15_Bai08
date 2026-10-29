# Phần 1: Phân tích lỗ hổng

1. Dòng log nguồn gốc rò rỉ: Dòng 1 (08:15 T2 - file campuspay_beta_users.xlsx).
- Tổ hợp lỗi: Cấp quyền "Editor" kết hợp với phạm vi "Anyone with the link".
- Cơ chế rò rỉ: Bất kỳ ai trên Internet có đường dẫn đều có toàn quyền chỉnh sửa, sao chép, tải xuống và chia sẻ tiếp file chứa thông tin nhạy cảm của sinh viên ra ngoài công cộng.

2. Ba giả thuyết "Email người lạ" truy cập campuspay_api_keys.txt:
- Giả thuyết 1: Trưởng nhóm hoặc thành viên được cấp quyền đã vô tình chuyển tiếp nội dung file hoặc gửi nhầm đường dẫn trực tiếp qua kênh không bảo mật.
- Giả thuyết 2: File ban đầu bị cấu hình nhầm quyền công khai (Anyone with the link) trong khoảng thời gian ngắn trước khi được chỉnh sửa lại thành Restricted.
- Giả thuyết 3: Tài khoản email được cấp quyền hợp lệ (Email B) bị lộ thông tin đăng nhập, tạo cửa hậu cho người lạ truy cập.

# Phần 2: Sửa lỗi & Nghiệm thu

3. Bảng cấu hình quyền chia sẻ chuẩn:

| Tên file | Quyền đúng | Phạm vi đúng | Giải thích ngắn gọn |
| :--- | :--- | :--- | :--- |
| campuspay_beta_users.xlsx | Viewer | Restricted | Chỉ cho phép xem dữ liệu test, giới hạn đúng email nội bộ nhóm. |
| campuspay_api_keys.txt | Viewer | Restricted | Bảo vệ thông tin khóa API cốt lõi, chỉ cấp quyền xem cho người thực sự cần. |
| slide_pitch_v8.pptx | Commenter | Anyone with the link | File thuyết trình cần nhận góp ý từ cộng đồng/giảng viên mà không sợ bị sửa đổi tài liệu gốc. |

4. Xử lý sau sự cố:
- Tính năng vô hiệu hóa link cũ nhanh nhất: Đổi liên kết chia sẻ mới hoặc xóa quyền chia sẻ hiện tại (Remove access).
- Thời điểm dùng 'Set Expiration Date': Nên dùng khi chia sẻ tài liệu cho bên thứ ba, thực tập sinh hoặc đối tác trong một khoảng thời gian dự án ngắn hạn để hệ thống tự động thu hồi quyền.
