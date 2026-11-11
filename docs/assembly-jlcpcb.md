# Đặt hàng JLCPCB

## File cần upload

| Bản | Gerber | BOM | CPL | Lắp ráp |
|---|---|---|---|---|
| main | `hardware/production/main/gerber_jlcpcb.zip` | `bom_jlcsmt.xlsx` | `cpl_jlcsmt.xlsx` | Standard PCBA, **2 mặt** (3 linh kiện trên + 26 dưới) |
| led2020 | `hardware/production/led2020/gerber_jlcpcb.zip` | `bom_jlcsmt.xlsx` | `cpl_jlcsmt.xlsx` | **Chỉ mặt dưới** (26 linh kiện), có thể chọn Economic |

BOM/CPL theo đúng mẫu `Sample-BOM_JLCSMT.xlsx` / `JLCSMT_Sample_CPL1.xlsx` của JLC; bản CSV đi kèm để xem nhanh.

## Linh kiện không do JLC lắp
- Module **ESP32-C3-WROOM-02-N4** (U1): tự hàn, không có trong BOM.
- J2B, J4 (JST-PH 4 chân xuyên lỗ), J3 (4 lỗ OLED), J5 (chỉ là pad).
- Bản led2020: 3 LED WS2812B-2020 ở mặt trên.

## Hiệu chỉnh góc xoay trong CPL
Mô hình trong thư viện JLC khác hướng gốc so với footprint KiCad, nên CPL đã cộng thêm:

| Linh kiện | Mã JLC | Hiệu chỉnh | Kiểm tra trong ảnh xem trước |
|---|---|---|---|
| J1 USB-C HX 16P | C2927039 | +180° | Miệng cổng hướng ra ngoài, lồi khỏi mép board |
| U6 AP2112K-3.3 | C51118 | +90° | Chấm hồng nằm cạnh dấu ▲ in trên board |
| U2 AMS1117-3.3 | C6186 | 0° | Chấm hồng ở chân ngoài cùng cạnh dấu ▶, tab tản nhiệt trên pad lớn |

**Quy tắc chung:** chấm hồng (chân 1) trong ảnh xem trước của JLC phải nằm cạnh dấu tam giác/chấm in trên board. Nếu lệch, dùng nút xoay trong trang xem trước hoặc sửa CPL.

## Lưu ý khác
- Cổng USB-C lồi khỏi mép 1,2 mm: nếu JLC đề nghị thêm viền công nghệ (edge rails), nên đồng ý.
- Các linh kiện Extended (tốn phí nạp linh kiện mỗi loại): AP2112K, USB-C, LED XL-1615 (có thể là Preferred). Kiểm tra trên công cụ BOM của JLC.
- F1 là điện trở **0 Ω** (C17888) nối tắt, không dùng cầu chì.
- R8, R9 (4,7 kΩ kéo lên I2C) **có hàn**.
