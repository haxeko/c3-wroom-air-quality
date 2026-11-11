# Gán chân và giắc cắm

## GPIO ESP32-C3

| GPIO | Chân module | Chức năng | Ghi chú |
|---|---|---|---|
| IO3 | 15 | Dữ liệu LED WS2812 | Qua R7 330 Ω tới LED1 DIN |
| IO4 | 3 | I2C SDA | OLED + SCD40, kéo lên 4,7 kΩ (R8) |
| IO5 | 4 | I2C SCL | OLED + SCD40, kéo lên 4,7 kΩ (R9) |
| IO6 | 5 | UART RX ← PMS5003 TX | 9600 baud |
| IO7 | 6 | UART TX → PMS5003 RX | Chỉ cần khi gửi lệnh cho cảm biến |
| IO9 | 8 | BOOT | Pad nạp số 5; kéo xuống GND khi cấp nguồn để vào chế độ nạp |
| IO10 | 10 | Nút người dùng SW2 | Nút nối xuống GND, dùng kéo lên nội (`INPUT_PULLUP`) |
| IO20 / IO21 | 11 / 12 | UART0 RX / TX | Pad nạp số 4 / 3 |
| IO2, IO8 | 16, 7 | Chân cấu hình khởi động | Đã kéo lên 3,3 V, không dùng |
| EN | 2 | Reset chip | RC tự reset khi cấp nguồn (R3 10 kΩ + C6 1 µF), không có nút |

Chân trống: **IO0, IO1, IO18, IO19**.

## Giắc cắm

### J2B – PMS5003 (JST-PH 2,0 mm, 4 chân)
Nhãn ghi **theo phía cảm biến**, cắm cùng tên vào cùng tên.

| Chân | Nhãn | Nối tới cảm biến |
|---|---|---|
| 1 | GND | GND (chân 2 của PMS5003) |
| 2 | 5V | VCC (chân 1) |
| 3 | TX | TX (chân 5) → ESP32 IO6 |
| 4 | RX | RX (chân 4) ← ESP32 IO7 |

### J4 – SCD40 (JST-PH 2,0 mm, 4 chân, chữ "CO2")
| Chân | Nhãn | Ghi chú |
|---|---|---|
| 1 | GND | |
| 2 | 3V3 | Từ AP2112K (U6), đường +3V3_CO2 riêng |
| 3 | SDA | |
| 4 | SCL | |

### J3 – OLED SH1106 (4 lỗ 2,54 mm)
Thứ tự **đã đảo** so với module OLED thông thường; tính từ pad vuông: **1 SDA, 2 SCL, 3 VCC (3,3 V), 4 GND**. Lắp màn theo hướng lật lại cho khớp nhãn in trên board.

### J5 – Pad nạp (6 pad tròn Ø1,8 mm, bước 2,54 mm, mặt sau)
| Pad | Nhãn | Tín hiệu |
|---|---|---|
| 1 | 3V3 | +3,3 V |
| 2 | GND | GND |
| 3 | TX | IO21 (TXD0) |
| 4 | RX | IO20 (RXD0) |
| 5 | IO9 | BOOT |
| 6 | GND | GND |

Nhãn ghi **theo phía ESP32**: nối **bắt chéo** với mạch nạp USB-UART (RX board → TX mạch nạp, TX board → RX mạch nạp), mức 3,3 V.

**Vào chế độ nạp:** nối tắt pad 5 và 6 (IO9–GND), rút/cắm lại USB, nạp xong bỏ nối tắt.

## LED WS2812
Chuỗi: `IO3 → R7 → LED1 DIN → LED1 DOUT → LED2 → LED3 → (DOUT để trống)`. LED1 là con trên cùng (gần cổng USB), chỉ số 0 trong code. Mỗi LED có tụ 100 nF riêng (C10–C12), nguồn 5 V.

| Chức năng | Bản main (XL-1615) | Bản led2020 (WS2812B-2020) |
|---|---|---|
| DIN | chân 4, trên-trái | chân 3, trên-phải |
| DOUT | chân 1, dưới-phải | chân 1, dưới-trái |
| VDD 5 V | chân 2, dưới-trái | chân 4, trên-trái |
| GND | chân 3, trên-phải | chân 2, dưới-phải |

(Nhìn mặt trước, cạnh có cổng USB ở phía trên.)
