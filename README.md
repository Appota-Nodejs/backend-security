![Basic Web Security](./img/markus-spiske-4T5MTKMrjZg-unsplash.jpg)

# **Basic Web Security - SQLi & XSS**

SQL Injection & XSS - Hai trong số những lổ hổng bảo mật phổ biến nhất.

## **1. [SQL Injection](./SQL%20Injection/1.%20SQLi%20Overview.md)**

## 2. XSS

### **Tổng quan**

XSS (là viết tắt của cụm từ Cross-Site Scripting) hiểu đơn giản là một hình thức tấn công bằng mã độc phổ biến, trong đó, hacker sẽ lợi dụng các lỗ hổng để chèn các mã script vào, sau đó gửi cho người dùng (hoặc người dùng vô tình truy cập vào trang bị nhiễm mã độc). Qua đó đánh cắp thông tin Cookie của người dùng và dùng nó để đăng nhập các tài khoản trên website đã bị nhiễm mã độc.

Hiện tại có 3 loại XSS chính là: Stored XSS, Reflected XSS, DOM-based XSS

### **2.1. Stored XSS** - ([link](/backend-security/XSS/2.1-storedXSS.md))

### **2.2. Reflected XSS** - ([link](/backend-security/XSS/2.2-reflectedXSS.md))

### **2.3. DOM Based XSS** ([link](/backend-security/XSS/2.3-domBasedXSS.md))

### **2.4. Cách phòng tránh**

Có 3 phương pháp thường dùng để fix lỗi này:

**1. Encoding**
<br>
Sử dụng hàm encoding có sẵn trong ngôn ngữ/framework để chuyển các kí tự `<>` thành `&lt;` `%gt;`

**2. Validation/Sanitize**
<br>
Một cách chống XSS khác là validation: loại bỏ hoàn toàn các kí tự khả nghi trong input của
người dùng, hoặc thông báo lỗi nếu trong input có các kí tự này.
<br>
Ngoài ra, nếu muốn cho phép người dùng nhập vào HTML, hãy sử dụng các thư viện sanitize.
Các thư viện này sẽ lọc các thẻ HTML, CSS, JS nguy hiểm để chống XSS. Người dùng vẫn có thể
sử dụng các thẻ `<p>`, `<span>`, `<ul>` để trình bày văn bản.

- **Validation (xác nhận)**: Đây là những kiểm tra được chạy để đảm bảo dữ liệu bạn có là phù hợp. Chẳng hạn, email là email, date là date và number(hoặc được chuyển đổi) một là integer(số nguyên).

- **Sanitization / Escaping**: Đây là các filter (bộ lọc) được áp dụng cho dữ liệu để làm cho dữ liệu 'an toàn' trong tình huống cụ thể. Chẳng hạn, để hiển thị code HTML trong textarea, cần phải thay thế tất cả các thẻ HTML bằng các thực thể tương đương với chúng

**3. CSP (Content Security Policy)**
<br>
Hiện tại, ta có thể dùng chuẩn CSP để chống XSS. Với CSP, trình duyệt chỉ chạy JavaScript từ
những domain được chỉ định.

<br>

`CSP là một lớp bảo mật được thêm vào mục đích để phát hiện và ngăn chặn một số loại tấn công thường gặp, bao gồm cả cuộc tấn công XSS (Cross Site Scripting) và tấn công data injection.`

<br>

Giả sử như `a.com` sử dụng CSP, chỉ chạy Javascript có nguồn gốc là `a.com`. Nếu để mã độc là `b.com` không nằm trong whitelist nên đoạn mã javascript ko được thực thi.

```html
<div>
    <p>
        <script src="/b.com/madoc.js"></script>
    </p>
</div>
```

Để sử dụng CSP, server chỉ cần thêm header Content-Security-Policy vào mỗi response. Nội
dung header chứa những domain mà ta tin tưởng.

```js
Content-Security-Policy: script-src 'self' https://apis.google.com
```
