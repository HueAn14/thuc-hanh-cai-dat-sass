# [Thực Hành] Hướng dẫn cài đặt SASS bằng npm & SASS CLI

Dự án thực hành cài đặt môi trường, sử dụng **SASS CLI** và **npm** để quản lý và biên dịch các tệp SCSS sang CSS phục vụ phát triển giao diện web chuyên nghiệp.

---

## 1. Thông Tin Môi Trường Thực Tế

- **Hệ điều hành:** Windows
- **Node.js:** `v24.21.0` (Lệnh kiểm tra: `node -v`)
- **npm:** `11.19.0` (Lệnh kiểm tra: `npm.cmd -v`)
- **SASS CLI:** `1.105.1` compiled with dart2js 3.13.5 (Lệnh kiểm tra: `sass --version`)

---

## 2. Các Bước Thực Hành Chi Tiết

### 🔹 Bước 1 & 2: Kiểm tra và Cài đặt Node.js / npm
Mở Terminal / PowerShell và kiểm tra:
```bash
node -v
npm -v
```

### 🔹 Bước 3 & 4: Cài đặt SASS toàn cục qua npm
Thực hiện cài đặt gói SASS:
```bash
npm install -g sass
```
Kiểm tra phiên bản SASS sau khi cài đặt:
```bash
sass --version
# Output: 1.105.1 compiled with dart2js 3.13.5
```

### 🔹 Bước 5: Cài đặt SASS CLI trực tiếp (Không qua npm)
Có thể tải trực tiếp file thực thi nhị phân từ [SASS GitHub Releases](https://github.com/sass/dart-sass/releases), giải nén và đưa vào `PATH` hệ thống (ví dụ `C:\Program Files\SASS\`).

### 🔹 Bước 6: Chuyển đổi tệp SCSS sang CSS bằng SASS CLI (Biên dịch đơn lẻ)
```bash
sass styles.scss styles.css
```
Lệnh trên đọc tệp `styles.scss` và tự động sinh ra tệp `styles.css` cùng tệp ánh xạ nguồn `styles.css.map`.

### 🔹 Bước 7: Kích hoạt chế độ theo dõi (Watch Mode)
```bash
sass styles.scss styles.css --watch
```
Khi sửa đổi tệp SCSS và lưu lại, tệp CSS sẽ được tự động biên dịch lại ngay lập tức.

### 🔹 Bước 8: Biên dịch cấu trúc nhiều tệp SCSS (Modular SASS)
Biên dịch toàn bộ thư mục `scss/` sang thư mục `css/`:
```bash
sass scss/:css/ --watch
```
Cấu trúc module hỗ trợ tách biệt biến (`_variables.scss`), mixin (`_mixins.scss`) và import vào tệp chính (`styles.scss`).

### 🔹 Bước 9: Xử lý lỗi Set-ExecutionPolicy trên Windows
Nếu gặp lỗi `PSSecurityException` khi thực thi script npm trong PowerShell, chạy PowerShell quyền Administrator và thiết lập:
```powershell
Set-ExecutionPolicy Unrestricted
```
Hoặc gọi trực tiếp file thực thi tương ứng: `npm.cmd` và `sass.cmd`.

---

## 3. Cấu Trúc Dự Án

```text
thuc-hanh-cai-dat-sass/
├── index.html            # Trang demo hiển thị kết quả biên dịch
├── package.json          # Cấu hình scripts npm quản lý biên dịch
├── styles.scss           # Tệp SCSS đơn lẻ thực hành Bước 6 & 7
├── styles.css            # File CSS kết quả biên dịch từ styles.scss
├── styles.css.map        # Sourcemap hỗ trợ debug CSS
├── scss/                 # Thư mục chứa mã nguồn SCSS module (Bước 8)
│   ├── _variables.scss   # Khai báo biến màu sắc, kích thước
│   ├── _mixins.scss      # Khai báo mixin Flexbox, shadow, transition
│   └── styles.scss       # Tệp SCSS chính sử dụng @use
├── css/                  # Thư mục đích nhận kết quả biên dịch
│   ├── styles.css        # File CSS hoàn chỉnh
│   └── styles.css.map    # Sourcemap cho thư mục css
└── README.md             # Hướng dẫn chi tiết
```

---

## 4. Các Lệnh Npm Scripts Tiện Dụng

Trong dự án này, bạn có thể chạy nhanh qua `npm run`:
- **Biên dịch tệp đơn:** `npm run build:single`
- **Theo dõi tệp đơn:** `npm run watch:single`
- **Biên dịch thư mục:** `npm run build:sass`
- **Theo dõi thư mục:** `npm run watch:sass`
