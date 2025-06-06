# 🔌 EVN VN

Công cụ EVN NPC,SPC,HN,CPC lấy dữ liệu điện tiêu thụ & tiền điện, và gửi qua MQTT về Home Assistant.

# Addon Home Assistant Xem Hướng Dẫn Ở Tab Tài Liệu

# EVNVN Docker Container

EVNVN là một container cho phép bạn lấy thông tin tiêu thụ điện từ tài khoản EVN Theo Khu Vực, hỗ trợ tích hợp với MQTT để sử dụng trong các hệ thống nhà thông minh như Home Assistant.

## 🧰 Tính năng

- Lấy dữ liệu điện tiêu thụ theo ngày, tháng, năm
- Hiển thị tiền điện tương ứng
- Hỗ trợ nhiều tài khoản EVN
- Tích hợp MQTT để dễ dàng tích hợp vào Home Assistant
- Hỗ trợ AI (Gemini) bypass capcha

---

## 🚀 Cài đặt

### Yêu cầu

- Docker đã được cài đặt trên hệ thống
- Máy có kết nối mạng và thời gian hệ thống chính xác (Timezone: Asia/Ho_Chi_Minh)
- Có tài khoản trên website EVN Khu vực của bạn

### Cấu hình `docker-compose.yml`

Tạo file `docker-compose.yml` như sau:

```yaml
services:
  evnvn:
    image: ghcr.io/smarthomeblack/evnvn-amd64:latest
    container_name: evnvn
    restart: unless-stopped
    network_mode: host
    environment:
      - TZ=Asia/Ho_Chi_Minh
    volumes:
      - /DATA/AppData/evnvn_docker:/config/evnvn
      - /DATA/AppData/evnvn_docker/options.json:/data/options.json
```

> 📁 Đảm bảo bạn đã tạo sẵn thư mục `/DATA/AppData/evnvn_docker` và file `options.json` bên trong đó.hoặc sử dụng thư mục tùy ý của bạn

---

## ⚙️ Cấu hình `options.json`

Tạo file `options.json` tại đường dẫn đã chỉ định với nội dung như sau:

```json
{
  "accounts_json": "[{\"userevn\": \"tài_khoản_1\", \"passevn\": \"mật_khẩu_1\", \"ngaydauky\": \"1\"}, {\"userevn\": \"tài_khoản_2\", \"passevn\": \"mật_khẩu_2\", \"ngaydauky\": \"15\"}]",
  "mqtt_server": "192.168.1.16",
  "mqtt_port": 1883,
  "mqtt_username": "tài khoản mqtt",
  "mqtt_password": "mật khẩu mqtt",
  "mqtt_topic_prefix": "homeassistant",
  "gemini_api_key": "api_key_gemini",
  "gemini_model": "gemini-2.0-flash",
  "ngaydauky": "1"
}
```

### 🔍 Giải thích các trường

- `accounts_json`: Danh sách các tài khoản EVN cần theo dõi.
- `mqtt_server`, `mqtt_port`, `mqtt_username`, `mqtt_password`: Thông tin kết nối MQTT
- `gemini_api_key`, `gemini_model`: Dùng để bypass capcha(Chỉ dùng cho NPC và SPC, Các khu vực khác điền bừa cũng được)
- `ngaydauky`: Mặc định cho kỳ điện nếu không chỉ định riêng từng tài khoản

---

## ▶️ Chạy container

Trong thư mục chứa `docker-compose.yml`, chạy lệnh:

```bash
docker compose up -d
```

---

## 📡 Tích hợp với Home Assistant

Các thông tin sẽ được publish đến MQTT dưới topic:  
```
homeassistant/tên_tài_khoản/...
```

- Vào Hacs Thêm Repo sau: https://github.com/smarthomeblack/npc
- Sau khi thêm thì tìm EVN VN
- Khởi động lại Home Assistant, Vào Thiết Bị --> Thêm Thiết bị --> Nhập Tên Đăng Nhập EVN để thêm các Sensor(CPC Miền trung đăng nhập bằng sdt thì khúc này nhập mã khách hàng)
- Hoặc tải thủ công custom_components/npc về rồi copy vào Home Assistant
---

## 🛠️ Ghi chú

- Đảm bảo thông tin đăng nhập EVN là chính xác.
- Mỗi tài khoản EVN nên có `ngaydauky` chính xác (thường là `1` hoặc `15`).
- Hệ thống sẽ tự động cập nhật dữ liệu theo chu kỳ 2 tiếng mỗi lần.

---

## 🖼️ Demo

<img title="NPC Cảm Biến Cơ Bản" src="https://raw.githubusercontent.com/smarthomeblack/hass-addon/refs/heads/main/evnvn/evn1.png" width="500px"></img>
<img title="NPC Cảm Biến Cơ Bản" src="https://raw.githubusercontent.com/smarthomeblack/hass-addon/refs/heads/main/evnvn/evn2.png" width="500px"></img>

---

## 📞 Hỗ trợ

Nếu bạn có câu hỏi hoặc muốn cải tiến, hãy mở [Issue](https://github.com/smarthomeblack/hass-addon/evnvn/issues) hoặc gửi PR.

---

## 🧾 License

MIT License

