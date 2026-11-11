# Phần cứng

| Thư mục | Nội dung |
|---|---|
| `kicad/main/` | Project KiCad bản chính v25 (`pm25.kicad_pro`) |
| `kicad/led2020/` | Project KiCad bản led2020 (`pm25_LED2020.kicad_pro`) |
| `kicad/lib/` | Thư viện dùng chung: `PM25.kicad_sym` (ký hiệu ESP32-C3-WROOM-02, USB-C 16P, XL-1615) và `PM25.pretty` (footprint USB-C HX 16P, LED XL-1615, nút TS-1187A, pad nạp) |
| `production/<bản>/` | Gerber + drill, BOM, CPL đúng mẫu JLCPCB (xlsx) và bản CSV |
| `docs/<bản>/` | Sơ đồ nguyên lý PDF, layout PDF, BOM đầy đủ (kèm linh kiện tự hàn, không gồm module ESP), tọa độ đầy đủ |
| `mechanical/` | Đường viền board DXF để vẽ vỏ |
| `cost/` | Kho giá linh kiện và BOQ giá thành 1 sản phẩm |

Mở bằng **KiCad 7 trở lên**. Bảng thư viện (`fp-lib-table`, `sym-lib-table`) trong mỗi project trỏ tới `../lib`, nên giữ nguyên cấu trúc thư mục khi sao chép.

Quy tắc thiết kế: đường tín hiệu 0,15–0,2 mm, nguồn 0,3–0,5 mm; via 0,6/0,3 mm; khoảng cách 0,2 mm; đồng cách mép board 0,3 mm; GND đổ hai mặt có via khâu.

Khi sửa board: xuất lại Gerber/BOM/CPL vào `production/<bản>/`, PDF vào `docs/<bản>/`, ghi thay đổi vào `docs/changelog.md` ở thư mục gốc. Nhớ giữ hiệu chỉnh góc CPL (J1 +180°, U6 +90°) – xem `docs/assembly-jlcpcb.md`.
