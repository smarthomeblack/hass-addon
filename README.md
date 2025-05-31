# Hướng Dẫn Thêm Kho Add-on cho Home Assistant

Kho add-on này chứa các tiện ích mở rộng (add-ons) được phát triển bởi **smarthomeblack** để sử dụng trên Home Assistant. Dưới đây là hướng dẫn từng bước để thêm kho repository vào Home Assistant của bạn.

## Bước 1: Mở Home Assistant
- Đăng nhập vào giao diện Home Assistant trên trình duyệt (ví dụ: `http://home-assistant.local:8123` hoặc địa chỉ IP của thiết bị chạy Home Assistant).

## Bước 2: Truy cập phần Add-on Store
- Nhấp vào **Settings** (Cài đặt) ở góc dưới bên trái.
- Chọn **Add-ons** > **Add-on Store**.

## Bước 3: Thêm Kho Repository
- Trong giao diện Add-on Store, nhấp vào biểu tượng **ba dấu chấm** (⋮) ở góc trên bên phải.
- Chọn **Add Repository** (Thêm Kho).
- Dán đường dẫn sau vào ô nhập liệu:
https://github.com/smarthomeblack/hass-addon

- Nhấp **Add** để xác nhận.

## Bước 4: Cài đặt Add-on
- Sau khi thêm kho thành công, bạn sẽ thấy các add-on từ kho `smarthomeblack` xuất hiện trong danh sách.
- Nhấp vào add-on bạn muốn cài đặt, sau đó nhấp **Install** (Cài đặt).
- Sau khi cài đặt, nhấp **Start** (Bắt đầu) để kích hoạt add-on.

## Danh sách Add-on Hiện Có
Dưới đây là danh sách các add-on hiện có trong kho `smarthomeblack/hass-addon`:
- **NPC Miền Bắc**: Add-on hỗ trợ tích hợp và quản lý dữ liệu từ NPC (Tổng Công ty Điện lực Miền Bắc) trên Home Assistant, giúp theo dõi và quản lý thông tin điện năng.

## Lưu ý
- Đảm bảo Home Assistant của bạn đã bật tính năng Add-on (thường có sẵn trên bản cài đặt Home Assistant Supervised hoặc Home Assistant OS).
- Nếu gặp lỗi, kiểm tra kết nối mạng hoặc cập nhật Home Assistant lên phiên bản mới nhất.
- Để biết thêm chi tiết về từng add-on, hãy xem mô tả trong trang cài đặt của add-on.

## Hỗ trợ
Nếu bạn cần trợ giúp, hãy mở issue trên GitHub tại:  
[https://github.com/smarthomeblack/hass-addon/issues](https://github.com/smarthomeblack/hass-addon/issues)

Cảm ơn bạn đã sử dụng kho add-on của chúng tôi!
