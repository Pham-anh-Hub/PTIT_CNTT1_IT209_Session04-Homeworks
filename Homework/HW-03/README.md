# Bài tập 3: Cấu hình xác thực SSH và Đẩy dự án lên GitHub

### 1. Kiểm tra kết nối tới gitHub
```bash
ssh -T git@github.com
```


## Quy trình tạo SSH Key, liên kết remote repository
(Do đã sử dụng github và cấu hình sẵn --> nên toàn bộ quy trình là được tổng hợp lại)

### 1. Kiểm tra và tạo mới cặp khóa SSH (SSH Keypair)
- Kiểm tra xem máy tính cá nhân đã có sẵn khóa SSH chưa, nếu chưa tiến hành sinh khóa mới.
```bash
ls -la ~/.ssh
```
- Kết quả có thể sẽ thấy các tệp tin như id_ed25519 và id_ed25519.pub, có nghĩa là bạn đã có khóa SSH
  - Nếu đã có -- bỏ qua bước tạo mới 
  - Nếu chưa có, Nếu chưa có khóa, tiến hành tạo mới bằng thuật toán bảo mật Ed25519
  ```bash 
  ssh-keygen -t ed25519 -C "email@example.com
  ```
### 2.  Sao chép Public Key và cấu hình lên GitHub:
(Đưa khóa công khai lên tài khoản GitHub để máy chủ nhận diện máy local của bạn)
- Hiển thị nội dung của khóa công khai:
```bash
cat ~/.ssh/id_ed25519.pub
```
- Bôi đen và sao chép toàn bộ nội dung hiển thị
- Đăng nhập vào GitHub, truy cập vào Settings (ở góc phải trên cùng) -> SSH and GPG keys -> chọn New SSH Key.
- Nhập tiêu đề tùy chọn (ví dụ: My Laptop) và dán toàn bộ nội dung khóa công khai đã copy vào ô Key, sau đó nhấn Add SSH Key.

### 3. Kiểm tra kết nối SSH tới GitHub
```bash
ssh -T git@github.com
```
- Terminal sẽ hỏi bạn có muốn tin tưởng máy chủ GitHub hay không, gõ "yes" và nhấn "Enter"
- Terminal hiển thị thông điệp chào mừng: ```Hi username! You've successfully authenticated, but GitHub does not provide shell access```. Có nghĩa là đã cấu hình SSH thành công!

### 4. Tạo Repository trống trên GitHub
```angular2html
Tạo nơi chứa dự án trên đám mây để chuẩn bị liên kết.

1. Truy cập trang chủ GitHub, nhấn nút New (hoặc nút Create repository).
2. Đặt tên kho chứa (ví dụ: git-practice-remote).
3. Chọn chế độ hiển thị là Public hoặc Private.
4. Lưu ý quan trọng: Không tích chọn bất kỳ mục nào như Add a README file, Add .gitignore hay Choose a license để tránh tạo ra commit ban đầu gây lệch nhánh.
5. Nhấn Create repository.
6. Tại giao diện hiển thị, chọn tab SSH (không chọn HTTPS) và sao chép đường dẫn repository có dạng: git@github.com:username/git-practice-remote.git.
```
### 5. Liên kết Local Repository với GitHub
- Khai báo đường dẫn remote cho dự án local đã làm việc ở bài trước.
- Mở thư mục dự án git-practice ở local trên Terminal và chạy lệnh:
```bash
git remote add origin git@github.com:username/git-practice-remote.git
```
- Kiểm tra remote liên kết thiết lập chính xác chưa
```bash
git remote -v
```

### 6. Đẩy mã nguồn lên GitHub (Git Push)
- Chạy lệnh đẩy nhánh main lên remote:
```bash 
git push -u origin main
```