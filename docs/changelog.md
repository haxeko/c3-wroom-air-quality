# Lịch sử phần cứng

| Bản | Thay đổi chính |
|---|---|
| v1–v3 | Board đầu tiên: 6 LED, OLED, header PMS5003, giắc SCD40 JST-SH |
| v4–v6 | SCD40 hàn trên board + LDO riêng AP2112K; lỗ vít M2 bốn góc; chỉ còn nút RESET, BOOT bằng jumper |
| v8 | USB-C chỉ cấp nguồn, bỏ USBLC6, bỏ D+/D− |
| v9–v13 | Bỏ SCD40 khỏi board, thay bằng giắc J4; J4 và J2B dùng JST-PH 2,0 mm 4 chân; còn 5 LED |
| v17–v19 | USB-C 6 chân; trở 0603 1%, tụ 0603/0805; **v19 = bản cũ 5 LED WS2812B-2020, header nạp xuyên lỗ, nút RESET** (không có trong repo) |
| v20 | 3 LED XL-1615; nút TS-1187A (JLC Basic); USB-C HX 16P do JLC hàn; F1 → 0 Ω; tụ 22 µF → 16 V; R8/R9 có hàn |
| v21 | LED dời vào giữa board; USB-C lồi 1 mm |
| v22 | LED dời sang trái, căn giữa theo cạnh ngắn; đảo thứ tự chân OLED (SDA, SCL, VCC, GND) |
| v23 | Header nạp J5 → 6 pad; USB-C lồi 1,2 mm; bỏ ESP khỏi BOM JLC |
| v24 | Pad nạp tròn; chữ "Villa Nest", to hơn và dời chỗ |
| **v25 (main)** | SW2 chuyển từ EN sang **IO10** (nút người dùng); CPL hiệu chỉnh J1 +180°, U6 +90° |
| **led2020** | Nhánh từ v25: JLC lắp 1 mặt, tự hàn 3 LED WS2812B-2020 |
