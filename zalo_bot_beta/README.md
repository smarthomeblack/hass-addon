## ❓ Nhóm Support:
- Zalo: https://zalo.me/g/alvkgn274
- Telegram: https://t.me/smarthomeblack

---

# 🤖 ZALO BOT

ZALO BOT gửi và nhận tin nhắn, thông báo trên Home Assistant.

# Addon Home Assistant Xem Hướng Dẫn Ở Tab Tài Liệu

# ZALO BOT Docker Container

ZALO BOT là một container cho phép bạn gửi và nhận tin nhắn, thông báo trên Home Assistant về Zalo.

## 🧰 Tính năng

- Webbook cho phép nhận tin nhắn để kích hoạt tự động hóa.
- Gửi thông báo tin nhắn Zalo tới tài khoản cá nhân hoặc nhóm.
- Hỗ trợ nhiều tài khoản Zalo.

---

## 🚀 Cài đặt

### Yêu cầu

- Docker đã được cài đặt trên hệ thống
- Máy có kết nối mạng và thời gian hệ thống chính xác (Timezone: Asia/Ho_Chi_Minh)
- Có tài khoản Zalo

### Cấu hình `docker-compose.yml`

Tạo file `docker-compose.yml` như sau:

```yaml
services:
  evnvn:
    image: ghcr.io/smarthomeblack/zalobot-amd64:latest
    container_name: zalo
    restart: unless-stopped
    network_mode: host
    environment:
      - TZ=Asia/Ho_Chi_Minh
    volumes:
      - /DATA/AppData/Hass/config/zalo_bot:/app/data
      - /DATA/AppData/Hass/config/www/zalo_bot:/config/www/zalo_bot
```

> 📁 Đảm bảo thư mục `/DATA/AppData/Hass/config/` là thư mục config của Home Assistant.


---

## ▶️ Chạy container

Trong thư mục chứa `docker-compose.yml`, chạy lệnh:

```bash
docker compose up -d
```

---

## 📡 Cấu hình tài khoản Zalo

- Sau khi đã chạy container zalo bot thành công thì vào địa chỉ http://ip:3000 (thay ip thành ip host của bạn)
- Đăng nhập quản trị bằng tài khoản mặc định admin/admin
- Sau đó chọn Đăng nhập Zalo --> Tạo mã QR --> Dùng điện thoại quét mã để đăng nhập

---

## 📡 Cài Bộ tích hợp ZALO BOT

Xem chi tiết hướng dẫn cài ở đây: https://github.com/smarthomeblack/zalo_bot

---

## 📞 Hỗ trợ

Nếu bạn có câu hỏi hoặc muốn cải tiến, hãy mở [Issue](https://github.com/smarthomeblack/hass-addon/zalo_bot/issues) hoặc gửi PR.

---

## 🧾 License

MIT License

## Cảm ơn
- Cảm ơn tới nhóm ChickenAI đã tạo ra 1 thư viện miễn phí
- Khảm khảo: https://github.com/ChickenAI/multizlogin