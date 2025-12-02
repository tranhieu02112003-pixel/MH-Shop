# Shop Mini (MQTT) — Gói hoàn chỉnh

Mình đã tạo cho bạn một project **Shop Mini** sử dụng **MQTT** để gửi thông báo đơn hàng realtime, không cần server.

## Nội dung gói
- `index.html` — danh mục sản phẩm
- `product.html` — trang chi tiết sản phẩm
- `order.html` — form đặt hàng (publish lên MQTT topic)
- `product-data.js` — dữ liệu sản phẩm (cập nhật tùy ý)
- `styles.css` — giao diện
- `mqtt-subscriber.html` — trang để mở trên máy tính (subscribe topic và nhận thông báo)
- `README.md` — hướng dẫn nhanh

## Hướng dẫn triển khai nhanh (A → Z)

### 1) Tạo broker MQTT (gợi ý)
- EMQX public broker (dùng demo): `wss://broker.emqx.io:8084/mqtt` (không cần user/pass) — thử nhanh được.
- Hoặc đăng ký EMQX Cloud / CloudMQTT để có broker riêng (miễn phí tier).

### 2) Cấu hình `order.html`
- Mở `order.html` trong editor.
- Tìm khối `MQTT_CONFIG` (gần đầu script) và sửa:
  - `brokerUrl` → ví dụ: `wss://broker.emqx.io:8084/mqtt` hoặc broker của bạn (websocket URL)
  - `options.username` / `options.password` → nếu broker yêu cầu

> Nếu bạn dùng `wss://broker.emqx.io:8084/mqtt`, bạn có thể để cấu hình mặc định (sẵn trong `mqtt-subscriber.html`).

### 3) Nhận thông báo trên điện thoại
- Tải app MQTT (Android / iOS):
  - MQTTX Mobile, MQTT Dash, MyMQTT, IoT MQTT Panel...
- Thêm broker (host, port, user, pass)
- Subscribe topic: `shop/orders`
- Bây giờ mở `order.html`, gửi 1 đơn — bạn sẽ nhận message trên điện thoại.

### 4) Nhận thông báo trên máy tính
- Mở `mqtt-subscriber.html` trên trình duyệt (File → Open) hoặc host trên server.
- Điền Broker URL → Connect → nhận message realtime. Trình duyệt sẽ cố gắng yêu cầu quyền hiển thị Notification.

## Gợi ý nâng cấp
- Thêm xác thực CAPTCHA để tránh spam.
- Lưu lịch sử đơn lên server hoặc Google Sheets khi cần.
- Kết nối MQTT broker với một service nhỏ (IFTTT/webhook) để tự động gửi Zalo/Telegram/email khi có đơn.
- Tạo dashboard quản lý đơn (web) bằng cách subscribe cùng topic và lưu các message vào localStorage hoặc DB.

---

Nếu bạn muốn, mình sẽ:
- Thay sản phẩm thành dữ liệu của bạn (gửi ảnh + tên + giá).
- Tùy chỉnh giao diện (màu, logo).
- Tạo 1 file ZIP để bạn tải (mình đã tạo sẵn).
