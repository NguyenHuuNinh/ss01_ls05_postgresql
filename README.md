ĐỀ BÀI
Ứng dụng Quản lý Tài chính Cá nhân (Smart Finance Tracker)


[Bài tập] Ứng dụng Quản lý Tài chính Cá nhân (Smart Finance Tracker)
1. Bối cảnh dự án (Business Context)
Hãy tưởng tượng bạn đang xây dựng phần mềm backend cho một ứng dụng giống như Money Lover hay Spendee.

Người dùng hiện đại thường gặp vấn đề "chưa hết tháng đã hết tiền" vì họ có quá nhiều nguồn tiền (Tiền mặt, Thẻ tín dụng, Momo, Techcombank...) và vô số khoản chi lặt vặt không nhớ nổi. Họ cần một ứng dụng để:

Ghi chép nhanh các khoản Thu / Chi hàng ngày.
Biết chính xác tiền đang nằm ở Ví nào.
Đặt ra Ngân sách (Budget) (VD: Chỉ được tiêu 3 triệu tiền ăn uống trong tháng này).
Theo dõi Mục tiêu tiết kiệm (Goal) (VD: Mua Macbook mới).
2. Mục tiêu bài học
Làm chủ kỹ năng thiết kế mô hình ERD có yếu tố thời gian (Time-series data như các giao dịch hàng ngày).
Vận dụng linh hoạt Khóa chính (PK) để xử lý các mối quan hệ phức tạp (1-N, N-N).
Có tư duy mở rộng hệ thống (Scalability) để phục vụ cho các bài toán Phân tích dữ liệu (Data Analytics)
3. Phân tích Yêu cầu Dữ liệu (Database Schema Requirements)
Hệ thống cần quản lý 4 nhóm thông tin chính. Sinh viên hãy đọc kỹ các nghiệp vụ dưới đây để xác định các cột (thuộc tính) cho từng bảng:

A. Quản lý Người dùng & Ví tiền (Bảng users và wallets)
Người dùng (users): Lưu trữ thông tin cá nhân. Cần các trường:
user_id (PK)
họ tên
email
created_at (ngày tạo tài khoản để sau này thống kê thâm niên)
Ví tiền (wallets): Một người dùng có thể có nhiều ví (1 User → N Wallets). Cần các trường: 
wallet_id (PK)
tên ví (Tiền mặt, Thẻ tín dụng, Momo...)
số dư ban đầu
loại tiền tệ (VND, USD)
B. Quản lý Danh mục (Bảng categories) Để vẽ được biểu đồ hình tròn (Pie chart), mọi giao dịch phải được gắn vào một danh mục.
Cần các trường: 
category_id (PK)
tên danh mục (Ăn uống, Lương, Mua sắm...)
Bài toán tư duy: Danh mục này là do hệ thống tạo ra dùng chung cho tất cả mọi người, hay mỗi User được quyền tự tạo danh mục riêng của mình? 
C. Quản lý Giao dịch - Trái tim hệ thống (Bảng transactions) Bảng này sẽ phình to rất nhanh, ghi lại từng biến động số dư.
Cần các trường: 
transaction_id (PK)
ngày giao dịch
số tiền
loại (THU/CHI)
đoạn text mô tả.
Các mối quan hệ bắt buộc:
Giao dịch này của ai? (User)
Trừ tiền từ ví nào? (Wallet)
Thuộc danh mục nào? (Category)
Mở rộng (Tùy chọn): Bảng recurring_transactions dùng để cấu hình các khoản thu/chi tự động lặp lại hàng tháng (Ví dụ: Tiền thuê nhà, Tiền lương).
D. Quản lý Ngân sách & Mục tiêu (Bảng budgets và goals)
Ngân sách (budgets): Giới hạn số tiền tối đa được tiêu cho một danh mục trong một tháng cụ thể. Cần các trường: 
budget_id (PK)
tháng
năm
số tiền giới hạn
Các mối quan hệ bắt buộc:
Ngân sách này của ai? (User)
Ngân sách thuộc về danh mục nào? (Category)
Mục tiêu (goals): Lập kế hoạch tiết kiệm. Cần các trường: 
goal_id (PK)
tên mục tiêu (Mua xe, Du lịch...)
số tiền cần đạt
và ngày đến hạn (deadline)
Các quan quan hệ bắt buộc:
Mục tiêu của ai? (User)
4. Nhiệm vụ của Sinh viên
Thiết kế Sơ đồ ERD Hoàn chỉnh
Từ các mô tả trên, bạn hãy sử dụng các công cụ vẽ (draw.io, dbdiagram.io, MySQL Workbench...) để thiết kế ERD.

Xác định đầy đủ Thực thể, Thuộc tính, PK
Vẽ rõ các đường nối thể hiện quan hệ (1-N, N-N)
