# ⏱️ CronJob_Python - Tự Động Hóa Gọi URL & Webhook Bằng Python

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-3776AB?logo=python&logoColor=white" alt="Python 3.8+" />
  <img src="https://img.shields.io/badge/Thư_viện-requests-blue" alt="Requests" />
  <img src="https://img.shields.io/badge/Nền_tảng-Windows_|_Linux_|_macOS-brightgreen" alt="Platform" />
  <img src="https://img.shields.io/badge/Giấy_phép-MIT-yellow.svg" alt="License: MIT" />
</p>

<p align="center">
  <b>Công cụ tự động gửi request HTTP GET định kỳ đến danh sách URL phục vụ keep-alive, ping uptime, kích hoạt cron webhooks cho các dịch vụ web máy chủ miễn phí (Render, Heroku, Supabase, Vercel...).</b>
</p>

---

## 📖 Giới Thiệu (Overview)

**CronJob_Python** là một script tự động hóa siêu nhỏ gọn, dễ dùng, được viết bằng Python. Chương trình đọc danh sách các đường dẫn (URLs) từ file `cron.txt`, tuần tự gửi các truy vấn HTTP GET qua thư viện `requests`, và hiển thị chi tiết nội dung phản hồi (`Response`) của từng phiên chạy.

### Ứng dụng thực tế:
- 🟢 **Keep-alive / Chống ngủ đông**: Giữ cho các ứng dụng web deploy trên các nền tảng miễn phí (như Render, Koyeb, Glitch, Heroku...) luôn ở trạng thái thức (active) 24/7.
- 🔄 **Webhook & Task Triggers**: Tự động kích hoạt các endpoint chạy tác vụ định kỳ của hệ thống quản trị, crawler dữ liệu, gửi email hoặc sao lưu database.
- 📡 **Uptime Monitor cơ bản**: Theo dõi trạng thái hoạt động của các server, API endpoint.

---

## ✨ Tính Năng Nổi Bật (Key Features)

- 📋 **Quản lý danh sách URL linh hoạt**: Quản lý toàn bộ endpoint cần gọi trong file văn bản `cron.txt` đơn giản, không cần sửa mã nguồn khi thêm/bớt URL.
- 🖥️ **Ghi nhật ký trực quan (Real-time Logging)**: In ra màn hình số thứ tự phiên (`Phiên`), URL mục tiêu và dữ liệu phản hồi (`Response: ...`) trực tiếp.
- ⏱️ **Tùy biến chu kỳ lặp**: Dễ dàng chỉnh thời gian trễ giữa các vòng lặp qua biến `limit` (mặc định 5 giây).
- 🚀 **Nhẹ & Tiêu hao ít tài nguyên**: Hoạt động mượt mà ngay cả trên các gói VPS cấu hình thấp nhất (1 vCPU, 512MB RAM).

---

## 🚀 Hướng Dẫn Cài Đặt & Sử Dụng (Getting Started)

### 1. Yêu Cầu Môi Trường (Prerequisites)
- [Python 3.8+](https://www.python.org/downloads/) đã được cài đặt trên máy.
- Đảm bảo đã tích chọn **"Add Python to PATH"** khi cài đặt trên Windows.

---

### 2. Tải Về & Cài Đặt (Installation)

1. **Clone repository:**
   ```bash
   git clone https://github.com/kingbone2006/CronJob_Python.git
   cd CronJob_Python
   ```

2. **Cài đặt thư viện phụ thuộc (`requests`):**
   ```bash
   pip install requests
   ```

---

### 3. Cấu Hình Danh Sách URL (`cron.txt`)

Mở file `cron.txt` và nhập các đường link URL bạn muốn hệ thống tự động gọi định kỳ (mỗi link trên **một dòng riêng biệt**):

```text
https://my-app.onrender.com/api/ping
https://example.com/cron-task
https://api.mysite.vn/health
```

> [!TIP]
> Đảm bảo mỗi đường dẫn đều có đầy đủ giao thức `http://` hoặc `https://`. Tránh để các dòng trống ở cuối file.

---

### 4. Khởi Chạy (Run)

Khởi chạy script bằng lệnh:

```bash
python 1.py
```

Khi chạy thành công, kết quả sẽ hiển thị liên tục theo từng phiên:

```text
Phiên: 1
+ URL: https://my-app.onrender.com/api/ping
+ Response: {"status":"ok","timestamp":1726589000}
-------------------------------------
Phiên: 2
+ URL: https://example.com/cron-task
+ Response: Success
-------------------------------------
```

Để dừng tiến trình, nhấn tổ hợp phím `Ctrl + C` trong terminal.

---

## ⚙️ Tùy Chỉnh Mã Nguồn (Configuration)

Mở file `1.py` để tùy chỉnh các thông số hoạt động:

```python
limit = 5  # Số giây nghỉ giữa các chu kỳ lặp (ví dụ: 60 = lặp lại sau mỗi 1 phút)
loop = True # Đặt False nếu chỉ muốn chạy đúng 1 lượt rồi thoát
```

---

## 🔄 Hướng Dẫn Chạy Nền 24/7 (Running 24/7 in Background)

### Trên Linux / VPS:

1. **Dùng lệnh `nohup` (Không tắt khi ngắt SSH):**
   ```bash
   nohup python3 1.py > cron.log 2>&1 &
   ```
   *Kiểm tra tiến trình đang chạy:*
   ```bash
   ps aux | grep 1.py
   ```

2. **Dùng công cụ `PM2` (Khuyên dùng - Tự khởi động lại khi lỗi hoặc reboot server):**
   ```bash
   npm install -g pm2
   pm2 start 1.py --name "cronjob" --interpreter python3
   pm2 save
   pm2 startup
   ```

3. **Dùng công cụ `screen`:**
   ```bash
   screen -S cronjob
   python3 1.py
   # Nhấn Ctrl + A rồi ấn phím D để thoát ra ngoài mà chương trình vẫn chạy
   ```

---

### Trên Windows:

Để chạy ẩn hoàn toàn dưới nền không hiện cửa sổ đen CMD, tạo một file `run_silent.vbs` cùng thư mục với nội dung sau:

```vbs
Set WshShell = CreateObject("WScript.Shell")
WshShell.Run "python 1.py", 0, False
```
*Nhấp đúp chuột vào file `.vbs` để chạy ngầm.*

---

## 📁 Cấu Trúc Thư Mục (Project Structure)

```text
CronJob_Python/
├── 1.py          # Script thực thi chính (gửi requests & lặp chu kỳ)
├── cron.txt      # Danh sách URLs mục tiêu cần gọi
├── README.md     # Tài liệu hướng dẫn sử dụng
├── LICENSE       # Giấy phép mã nguồn mở MIT
└── .gitignore    # Loại trừ các file rác / pycache
```

---

## 🛠️ Xử Lý Sự Cố Thường Gặp (Troubleshooting)

| Vấn đề | Nguyên nhân | Cách khắc phục |
| :--- | :--- | :--- |
| `ModuleNotFoundError: No module named 'requests'` | Chưa cài đặt thư viện `requests` | Chạy lệnh `pip install requests` |
| `MissingSchema: Invalid URL '': No scheme supplied` | Có dòng trắng/trống trong `cron.txt` | Xóa các dòng trống ở cuối file `cron.txt` |
| `ConnectionError` / `Timeout` | URL mục tiêu bị sập hoặc sai tên miền | Kiểm tra lại kết nối mạng và tính khả dụng của URL trên trình duyệt |

---

## 📜 Giấy Phép (License)

Dự án được phát hành dưới giấy phép mã nguồn mở [MIT License](LICENSE). Mọi người đều có quyền tự do sử dụng, chỉnh sửa và phân phối lại.

---

<p align="center">
  Tạo bởi <a href="https://github.com/kingbone2006">kingbone2006</a>
</p>
