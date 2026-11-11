# Hàn LED WS2812B-2020 (bản led2020 và bản cũ)

## Vị trí chân trên board
Nhìn mặt trước, cạnh có cổng USB ở phía trên, mỗi LED:

| Góc | Chân | Chức năng |
|---|---|---|
| Trên-trái | 4 | VDD (5 V) |
| Trên-phải | 3 | DIN |
| Dưới-trái | **1** | DOUT, góc có dấu chân 1 in trên board |
| Dưới-phải | 2 | GND |

## Xác định chân GND trên LED bằng đồng hồ
Ký hiệu chấm/mũi tên trên LED khác nhau giữa các hãng, nên đo để chắc chắn.

**Đồng hồ có chế độ diode (▶|):**
1. Úp LED lên băng dính, mặt chân hướng lên.
2. Que đỏ đặt lên một chân, que đen lần lượt chạm 3 chân còn lại.
3. Cả 3 lần đều hiện khoảng 0,4–0,9 → chân đặt que đỏ là **GND**. Có lần hiện OL → đổi chân khác.

**Đồng hồ không có chế độ diode (ví dụ Hioki 3280-10F):** dùng thang **Ω**. Que đỏ trên GND thì cả 3 lần đều **có số** (kΩ–MΩ); chân khác sẽ có lần báo **OF**. Không dùng chế độ thông mạch (chỉ kêu dưới khoảng 50 Ω).

Đặt LED **mặt sáng hướng lên**, chân GND vào pad **dưới-phải**; ba chân còn lại tự đúng.

## Cách hàn
- Chân nằm dưới thân LED: dùng **kem hàn + máy khò** 300–320 °C, gió nhỏ, khò từ phía trên.
- **Không** dùng bàn gia nhiệt từ dưới (mặt dưới có linh kiện JLC đã hàn).
- Hàn LED1 trước, chạy thử, rồi mới hàn LED2, LED3.

```cpp
#include <Adafruit_NeoPixel.h>
Adafruit_NeoPixel led(3, 3, NEO_GRB + NEO_KHZ800);   // 3 LED, IO3 (bản cũ: 5 LED)
void setup() { led.begin(); led.setBrightness(20); led.setPixelColor(0, led.Color(255, 0, 0)); led.show(); }
void loop() {}
```
LED1 sáng đỏ là đúng hướng. Không sáng hoặc nóng → rút USB ngay, kiểm tra lại.
