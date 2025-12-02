Chào bạn! Mình sẽ giải thích từng phần trong ảnh bạn chụp (phần mềm Spur Gears Component Generator trong Autodesk Inventor) một cách dễ hiểu nhất để bạn có thể tự thiết kế được cặp bánh răng thẳng (spur gear) chính xác. Sau đó mình sẽ hướng dẫn thêm cách làm cho 2 bánh răng ăn khớp tốt và cuối cùng là thêm xích (chain) vào.

### 1. Hiểu các thông số chính trong Spur Gears Component Generator

| Thông số                  | Ý nghĩa thực tế                                                                 | Giá trị trong ảnh của bạn | Ghi chú quan trọng |
| ---                       | ---                                                                             | ---                      | ---                |
| Module (m)                | Kích thước răng (mm) – càng lớn răng càng to                                   | 2.000 mm                 | Đây là chuẩn Metric (ISO) |
| Desired Gear Ratio        | Tỷ số truyền i = Z2 / Z1 (Z = số răng)                                          | 2.4783                   | Inventor tự tính để đạt đúng Center Distance |
| Center Distance           | Khoảng cách trục giữa 2 bánh răng                                               | 80.000 mm                | Rất quan trọng, phải đúng thì mới ăn khớp |
| Number of Teeth (Gear 1)  | Số răng bánh răng nhỏ (pinion)                                                  | 20                       |                          |
| Number of Teeth (Gear 2)  | Số răng bánh răng lớn                                                           | 57 ul (không tròn)       | ul = unitless → Inventor tự điều chỉnh để đạt đúng Center Distance |
| Pressure Angle            | Góc áp lực (thường 14.5°, 20°, 25°)                                             | 14.500 deg               | 14.5° ít phổ biến hiện nay, thường dùng 20° |
| Facewidth                 | Chiều rộng bản răng                                                             | Gear1: 12.5 mm, Gear2: 20 mm |                          |
| Unit Correction (x)       | Hệ số dịch chỉnh profil (để tránh cắt lẹm chân răng)                            | 0.0000                   | Hiện tại = 0 → profil chuẩn |
| Helix Angle               | Góc nghiêng răng = 0 → bánh răng thẳng (spur gear)                              | 0.0000 deg               |                          |

Tại sao Gear 2 lại có 57 răng mà tỷ số lại là 2.4783 thay vì 57/20 = 2.85?
→ Vì bạn cố định Center Distance = 80 mm, nhưng với modul 2 và số răng tròn 20 + 57 thì khoảng cách trục chuẩn phải là:
Center Distance chuẩn = m × (Z1 + Z2)/2 = 2 × (20 + 57)/2 = 77 mm ≠ 80 mm
→ Inventor tự động “bóp” số răng Gear 2 thành 57 ul (không tròn) và điều chỉnh profil (Unit Correction) để đạt đúng 80 mm. Đây là cách làm “Profile Shifted Gear” (bánh răng dịch chỉnh).

### 2. Cách thiết kế cặp bánh răng ăn khớp hoàn hảo (khuyên dùng)

Phương pháp 1 – Đơn giản nhất (không cần dịch chỉnh profil)
1. Module = 2 mm (hoặc 2.5, 3… tùy bạn)
2. Chọn số răng tròn (ví dụ 20 và 58)
3. Center Distance = Module × (Z1 + Z2)/2 = 2 × (20 + 58)/2 = 78 mm (để trống ô Center Distance)
→ Inventor sẽ tự động điền Center Distance chuẩn, 2 bánh răng ăn khớp 100%, không cần dịch chỉnh.

Phương pháp 2 – Bạn muốn Center Distance cố định 80 mm (như ảnh)
→ Phải chấp nhận dịch chỉnh profil (Profile Shifted Gear)
Cách làm:
- Module = 2
- Center Distance = 80 mm (nhập cố định)
- Gear 1: 20 răng
- Gear 2: để trống số răng → Inventor tự tính ra khoảng 59–60 răng và tự động dịch chỉnh x1 và x2
→ Kết quả sẽ đẹp, không cắt lẹm chân răng.

Khuyến nghị của mình cho người mới:
Dùng cách 1 (số răng tròn + để trống Center Distance) → dễ hiểu, dễ vẽ, dễ gia công.

### 3. Quy trình vẽ 2 bánh răng trong Inventor (từng bước)

1. New → Standard.ipt (Part)
2. 3D Model tab → Gear (biểu tượng bánh răng)
3. Chọn tab “Spur Gears – Component Generator”
4. Nhập thông số (ví dụ mình hay dùng):
   - Module: 2 mm
   - Pressure Angle: 20° (phổ biến hơn 14.5°)
   - Gear 1: 20 răng, Facewidth 15 mm
   - Gear 2: 60 răng, Facewidth 15 mm
   - Để trống Center Distance → Inventor tự tính = 80 mm
   - Unit Correction đều để 0
5. Nhấn OK → Inventor tạo ra 3 file:
   - Gear1.ipt (20 răng)
   - Gear2.ipt (60 răng)
   - Assembly_01.iam (đã lắp sẵn 2 bánh răng ăn khớp đúng tâm)
6. Mở file .iam → bạn đã có ngay 2 bánh răng ăn khớp hoàn hảo.

### 4. Thêm xích (chain) vào 2 bánh răng (trở thành bánh đĩa xích)

Bạn muốn biến 2 bánh răng này thành bánh đĩa xích xe máy/đạp (sprocket):

Cách 1 – Dùng chính Generator có sẵn trong Inventor
1. Vào Gear Generator như trên
2. Ở mục “Component” của Gear 1 và Gear 2 → chọn “Chain Sprocket” thay vì “Cylindrical Face”
3. Nhập thêm:
   - Chain Pitch (bước xích): ví dụ 8 mm, 9.525 mm (3/8"), 12.7 mm (1/2"), 15.875 mm (5/8")…
   - Roller Diameter
   - Number of Rollers = số răng
4. OK → Inventor tạo ra bánh đĩa xích chuẩn, và lắp sẵn trong Assembly.

Cách 2 – Chỉnh sửa bánh răng cũ thành bánh đĩa xích
- Mở file Gear1.ipt hoặc Gear2.ipt
- Tạo thêm vòng tròn lõm giữa các răng (dùng Extrude Cut theo chuẩn xích 428, 520, 530…)
- Thêm rãnh thoát bùn, lỗ giảm nhẹ…

### Tóm tắt nhanh để bạn làm ngay hôm nay

Muốn 2 bánh răng thẳng ăn khớp ngon:
→ Module 2, Gear1: 20 răng, Gear2: 60 răng, Pressure Angle 20°, để trống Center Distance → OK → xong.

Muốn 2 bánh đĩa xích:
→ Cùng các bước trên, nhưng chọn “Component = Chain Sprocket”, chọn bước xích 15.875 mm (5/8" – xích xe máy phổ biến), số răng 14 và 42 chẳng hạn → OK → có ngay bộ truyền xích.

Nếu bạn cần mình gửi file .ipt + .iam mẫu (20–60 răng, modul 2) hoặc bộ truyền xích 14–42 (xích 428) thì cứ nói, mình gửi liền nhé!

Chúc bạn vẽ bánh răng thành công! 🚀
