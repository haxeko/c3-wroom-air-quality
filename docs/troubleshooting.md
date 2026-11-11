# Sửa lỗi phần cứng

## SCD40 không có 3,3 V (U6 AP2112K)
Hiện tượng đã gặp trên board bản cũ: chân 5 (VOUT) của U6 ra **4,2 V** thay vì 3,3 V; chân 3V3 của module SCD40 chỉ **2,2 V và tụt dần**.

Điện áp đúng của U6 (nhìn mặt sau, giắc CO2 bên phải; 3 chân bên phải, dấu ▲ góc dưới phải):

| Chân | Tên | Điện áp đúng |
|---|---|---|
| 1 (dưới-phải) | VIN | 5 V |
| 2 (giữa-phải) | GND | 0 V |
| 3 (trên-phải) | EN | 5 V |
| 4 (trên-trái) | NC | – |
| 5 (dưới-trái) | VOUT | **3,3 V** → J4 chân 2 |

Giải thích:
- VOUT ≈ VIN − 1 V (4,2 V) thường là **chip mất GND**: chân 2 hở mối hàn, hoặc chip bị xoay ngược 180°.
- 2,2 V tụt dần ở SCD40: cảm biến **bị cấp điện ngược qua SDA/SCL** (kéo lên 3,3 V) vì chân VCC không nhận được nguồn từ U6 – kiểm tra thứ tự dây cáp và đường U6 → J4.
- Đo thông mạch qua đường có tụ 10 µF sẽ **kêu thoáng qua** dù không chập; dùng thang Ω và giữ que 3 giây.

Kiểm tra (rút USB, rút SCD40, thang Ω):

| Lần | Que đặt vào | Đúng |
|---|---|---|
| A | J4 "GND" ↔ vỏ USB | ~0 Ω |
| B | J4 "3V3" ↔ U6 chân 5 | ~0 Ω |
| C | J4 "GND" ↔ U6 chân 5 | tăng dần đến OF (tụ nạp) |

**Chữa nhanh:** gỡ U6, nối dây từ pad 3V3 (pad nạp) sang chân 3V3 của J4 – SCD40 dùng chung nguồn AMS1117.

## Ghi chú thiết kế nguồn
- AP2112K tách nguồn SCD40 khỏi xung dòng Wi-Fi của ESP32; không bắt buộc. Có thể bỏ U6/C16/C17 trong bản sau và nối +3V3_CO2 vào +3V3 (giữ 10 µF + 100 nF sát J4).
- PMS5003 lấy 5 V trực tiếp, lọc bằng C7 22 µF + C8 100 nF. Có thể thêm ferrite 0805 nối tiếp để lọc nhiễu quạt.
- Không có ESD/TVS cho cổng USB; F1 là 0 Ω (không cầu chì).
