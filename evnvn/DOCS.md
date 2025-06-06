# 🔌 EVN VN

Công cụ EVN VN(NPC Miền Bắc, SCP Miền Nam, CPC Miền Trung, EVN Hanoi, E-thanglong lấy dữ liệu điện tiêu thụ & tiền điện, và gửi qua MQTT về Home Assistant.

- ✅ Không cần đăng nhập thủ công
- ✅ Hỗ trợ MQTT Discovery (Home Assistant nhận dạng tự động)

---

## 🚀 Cách sử dụng

### 1. Tạo cấu hình
Chú ý tài khoản cuối cùng luôn không có ký tự , ở cuối
```ini
accounts_json: |
  [
    {"userevn": "xxxxxx", "passevn": "xxxxxx", "ngaydauky": "1"},
    {"userevn": "xxxxxx", "passevn": "xxxxxx", "ngaydauky": "15"}
  ]
mqtt_server: 192.168.1.22
mqtt_port: 1883
mqtt_username: admin
mqtt_password: 11223344
mqtt_topic_prefix: homeassistant
gemini_api_key: Key API
gemini_model: gemini-2.0-flash
ngaydauky: "1"


```
NPC và SPC Cần điền đúng key api gemini để bypass Capcha. Còn lại EVN khác thì điền bừa key api cũng được
Cấu hình Port 1093 để có view đẹp


> Bạn cần có tài khoản [Google Gemini](https://makersuite.google.com/app/apikey) để lấy `gemini_api_key`.

### 2. Chạy Addon
- Sau khi config xong thì chạy addon, sang tab logs xem có lỗi gì không, đợi cho chạy xong lần đầu rồi làm bước tiếp theo
- Vào Hacs Thêm Repo sau: https://github.com/smarthomeblack/npc
- Sau khi thêm thì tìm EVN VN
- Khởi động lại Home Assistant, Vào Thiết Bị --> Thêm Thiết bị --> Nhập Tên Đăng Nhập EVN để thêm các Sensor(CPC Miền trung đăng nhập bằng sdt thì khúc này nhập mã khách hàng)
- Hoặc tải thủ công custom_components/npc về rồi copy vào Home Assistant
## 📡 Kết quả

Sau khi khởi chạy lần đầu sẽ mất chút thời gian để lấy dữ liệu, các cảm biến sẽ xuất hiện trong Home Assistant nhờ MQTT Discovery:

- `Tieu Thu Hom Nay`
- `Tien Dien Thang Truoc`
- `Chi So Cuoi Ky`
- Và nhiều cảm biến khác

---
## View Html

- Tải file [index.html](https://github.com/smarthomeblack/hass-addon/blob/main/evnvn/index.html) cho vào thư mục config/evnvn của hass
- vào Cài đặt -> bảng điều khiển -> thêm bảng điều khiển Trang Web, nhập http://ip hass:1093
## Hiển Thị Cảm Biến Trên Home Assistant

- Chi Tiết Tiêu Thụ Các Ngày Trong Tháng
```yaml
type: markdown
title: Chi Tiết Tiêu Thụ Tháng Này
content: >
  **Trạng thái tháng**: `{{
  states('sensor.chi_tiet_dien_tieu_thu_thang_nay') }}`


  <details>
    <summary><strong>Chi tiết dữ liệu</strong></summary>
    
    Ngày         - Chỉ số (kWh)     - Điện tiêu thụ (kWh)
    -
    {% for d in state_attr('sensor.chi_tiet_dien_tieu_thu_thang_nay', 'data') %}
    {{ d['Ngày'] }} | {{ d['Chỉ số'] }} kWh | {{ d['Điện tiêu thụ (kWh)'] }} kWh
    {% endfor %}

    **Start date**: {{ state_attr('sensor.chi_tiet_dien_tieu_thu_thang_nay','start_date') }}  
    **End date**: {{ state_attr('sensor.chi_tiet_dien_tieu_thu_thang_nay','end_date') }}
  </details>``
```

- Chi Tiết Tiêu Thụ Và Tiền Điện Các Tháng Trong Năm
```yaml
type: markdown
title: Chi Tiết Năm
content: |
  <details>
    <summary><strong>Chi tiết dữ liệu</strong></summary>
    Tháng - Năm  | Tiêu Thụ (KWh) | Tiền Điện (VNĐ)
    {% for d in state_attr('sensor.tien_dien_san_luong_nam_nay', 'TienDien') %}
      {# Tìm entry SanLuong cùng Tháng/Năm #}
      {% set sl = state_attr('sensor.tien_dien_san_luong_nam_nay', 'SanLuong')
         | selectattr('Tháng', 'equalto', d['Tháng'])
         | selectattr('Năm', 'equalto', d['Năm'])
         | first %}
      {{ d['Tháng'] }} - {{ d['Năm'] }}  --> {{ sl['Điện tiêu thụ (KWh)'] }} KWh --> {{ "{:,}".format(d['Tiền Điện'] | int) | replace(',', '.') }} VNĐ
    {% endfor %}

  </details>

```

---

## 🖼️ Demo

<img title="NPC Cảm Biến Cơ Bản" src="https://raw.githubusercontent.com/smarthomeblack/hass-addon/refs/heads/main/evnvn/evn1.png" width="500px"></img>
<img title="NPC Cảm Biến Cơ Bản" src="https://raw.githubusercontent.com/smarthomeblack/hass-addon/refs/heads/main/evnvn/evn2.png" width="500px"></img>

---

## ❓ Câu hỏi thường gặp

#### Q: Dữ liệu có tự động cập nhập không?
> A: Có, dữ liệu sẽ tự động thu thập & gửi dữ liệu mỗi 120 phút.

#### Q: Có logs theo dõi không?
> A: Có. Bạn có thể xem tại tab logs trong addon.

---

## ❤️ Đóng góp

Nếu bạn có câu hỏi hoặc muốn cải tiến, hãy mở [Issue](https://github.com/smarthomeblack/hass-addon/evnvn/issues) hoặc gửi PR.



