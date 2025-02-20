# 🚀 Fix Lỗi 401 Khi Gửi Request API Trong WPF MVVM

## 🔍 Vấn Đề Gặp Phải
Khi sử dụng WPF theo mô hình **MVVM** để gửi request API chứa **username** và **password** dạng **JSON**, backend Spring Boot báo lỗi **401 Unauthorized** mặc dù dữ liệu đã được kiểm tra là đúng.

Sau khi debug kỹ càng và so sánh với dữ liệu test trên **Postman**, phát hiện vấn đề nằm ở cách gửi **username** và **password** từ WPF.

---

## 🔎 So Sánh Dữ Liệu

### ✅ Dữ Liệu Test trên Postman (Gửi thành công)
```json
{
    "username": "admin",
    "password": "123456"
}
```

### ❌ Dữ Liệu Gửi Từ WPF (Bị lỗi 401)
```json
{
    "Username": "admin",
    "Password": "123456"
}
```

💡 **Vấn đề:**
- Trong dữ liệu gửi từ WPF, **các key `Username` và `Password` đều viết hoa chữ cái đầu**, trong khi API chỉ chấp nhận **username** và **password** toàn bộ viết thường.

---

## 🎯 Giải Pháp

### 🔧 Cách Fix
**Cần đảm bảo dữ liệu JSON gửi đi có đúng định dạng key theo yêu cầu API.**

📌 **Cách thực hiện:**
 **Sử dụng Annotation `[JsonProperty]` (nếu dùng Newtonsoft.Json)**
   ```csharp
   public class LoginRequest
   {
       [JsonProperty("username")]
       public string Username { get; set; }
       
       [JsonProperty("password")]
       public string Password { get; set; }
   }
   ```

2. **Kiểm tra API để xác định key JSON đúng chuẩn trước khi gửi request.**

---

## 🛠 Kết Quả Sau Khi Fix
Sau khi chỉnh sửa dữ liệu JSON theo đúng yêu cầu của API:
- ✅ Request từ WPF đã gửi đúng JSON format.
- ✅ API xử lý thành công, không còn lỗi 401.
- ✅ Đăng nhập hoàn tất!

🚀 **Lưu ý:** Luôn kiểm tra kỹ JSON request trước khi gửi, tránh lỗi do **viết hoa/viết thường không đúng format**!

---

🔥 **Hy vọng bài viết giúp bạn fix lỗi nhanh chóng!**

