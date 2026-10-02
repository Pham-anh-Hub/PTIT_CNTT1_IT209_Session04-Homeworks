# Bài tập 4: Quản lý tệp tin bỏ qua và sửa đổi commit

**Bối cảnh:**
```
Vô tình commit nhầm file chứa thông tin bảo mật credentials.txt lên Git.
```

**Yêu cầu:**
```
Cần gỡ bỏ file này khỏi sự theo dõi mà không làm mất file vật lý trên đĩa cứng, 
cấu hình để Git bỏ qua file này trong tương lai, và sửa lại tin nhắn commit gần nhất cho sạch sẽ.
```

### Quy trình:

#### 1. Gỡ bỏ lệnh file khỏi lệnh cache của Git:
```bash
git rm --cached HW-04/credentials.txt
```

#### 2. Cấu hình bỏ qua file trong tương lai
- Thủ công: mở file .gitignore -- Thêm file 'HW-04/credentials.txt'
- Lệnh: 
```bash
echo "credentials.txt" >> .gitignore
```

#### 3. Cập nhật lại .gitignore vào staging
```bash
git add .gitignore
```

#### 4. Sửa lại lịch sử commit gần nhất
```bash
git commit --amend -m "remove file credentials.txt and update gitignore"
```

#### 5. Kiểm tra lại
```bash
git status
```

