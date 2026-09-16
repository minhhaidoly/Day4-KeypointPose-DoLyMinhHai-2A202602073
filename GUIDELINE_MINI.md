# Mini guideline - nhóm: ______  |  người gán: Đỗ Lý Minh Hải  |  ngày: 16/9/2026

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | Đặt điểm khớp ở vị trí ước lượng trên hông. | Vì hông vẫn có thể được xác định vị trí mặc dù bị che khuất. |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | Đặt điểm khớp ở vị trí ước lượng trên tai. | Vì tai vẫn có thể được xác định vị trí mặc dù bị che khuất. |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Đặt điểm khớp ở vị trí ước lượng trên hông. | Vì hông vẫn có thể được xác định vị trí mặc dù bị cắt. |
| Cổ tay nằm sau tay lái / sau thân mình | Đặt điểm khớp ở vị trí ước lượng trên cổ tay. | Vì cổ tay vẫn có thể được xác định vị trí mặc dù bị che khuất. |
| Hai người chồng lên nhau | Đặt điểm khớp ở vị trí ước lượng trên các khớp. | Vì các khớp vẫn có thể được xác định vị trí mặc dù bị chồng lên nhau. |
| Người nhỏ đến mức nào thì không gán nữa | Nếu người nhỏ hơn 1/4 khung hình thì không gán. | Vì không thể xác định được vị trí các khớp. |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_02`, người thứ `1`, khớp `hông`

- Mơ hồ ở chỗ nào: Hông của người mặc quần áo dài bị che khuất một phần bởi lớp vải.
- Bạn quyết thế nào: Đặt điểm khớp ở vị trí ước lượng trên hông.
- Vì sao: Vì hông vẫn có thể được xác định vị trí mặc dù bị che khuất.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu không đặt điểm khớp, model sẽ không học được cách xác định hông trong các trường hợp tương tự.

### Ca 2 - ảnh `train_03`, người thứ `2`, khớp `gối`

- Mơ hồ ở chỗ nào: Gối của người bị che khuất bởi chân của người khác.
- Bạn quyết thế nào: Đặt điểm khớp ở vị trí ước lượng trên gối.
- Vì sao: Vì gối vẫn có thể được xác định vị trí mặc dù bị che khuất.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu không đặt điểm khớp, model sẽ không học được cách xác định gối trong các trường hợp tương tự.
### Ca 3 - ảnh `train_02`, người thứ `3`, khớp `cổ tay`

- Mơ hồ ở chỗ nào: Cổ tay của người bị che khuất bởi tay lái.
- Bạn quyết thế nào: Đặt điểm khớp ở vị trí ước lượng trên cổ tay.
- Vì sao: Vì cổ tay vẫn có thể được xác định vị trí mặc dù bị che khuất.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu không đặt điểm khớp, model sẽ không học được cách xác định cổ tay trong các trường hợp tương tự.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `______` (bạn `___%` / họ `___%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**:
- Luật mới bổ sung vào mục 2 sau khi thống nhất:
