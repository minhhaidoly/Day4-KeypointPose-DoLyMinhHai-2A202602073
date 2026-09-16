# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Đỗ Lý Minh Hải   Nhóm: Cá nhân   Ngày: 16/9/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 47 |
| v=2 / v=1 / v=0 | 612 / 143 / 44 |
| Thời gian trung bình mỗi ảnh | 16.8 |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. `left_hip` — 62%
2. `right_hip` — 58%
3. `left_wrist` — 41%

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.781 | 0.826 |
| OKS@0.50 | 0.920 | 0.966 |
| OKS@0.75 | 0.740 | 0.793 |
| Lỗi `dao_trai_phai` | 2 | 0 |
| Lỗi `nham_nguoi` | 1 | 0 |
| Lỗi `xoa_khop_bi_che` | | |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- `train_04`, người #1: cả skeleton đảo trái/phải — đổi lại toàn bộ cặp left/right.
- `train_11`, người #0: xương vai–khuỷu kéo sang người bên cạnh — kéo về đúng cơ thể.
- `train_08`, người #2, `left_wrist`: trước để v=0 vì bị che — đặt lại chấm ước lượng, chuyển v=1.

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->

## 3. Kiểm chéo

Bạn cùng nhóm: ______

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| | | | | |
| | | | | |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

-

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.781 | 0.826 | 0.045 |
| pose_mAP50-95 | 0.740 | 0.793 | 0.053 |
| pose_precision | 0.800 | 0.850 | 0.050 |
| pose_recall | 0.760 | 0.810 | 0.050 |
| box_mAP50-95 | 0.900 | 0.950 | 0.050 |

### Trả lời năm câu hỏi ở cuối notebook


> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?
   `pose_mAP50-95` tăng từ 0.740 lên 0.793, cho thấy 20 ảnh của tôi đã giúp model cải thiện khả năng nhận diện khớp ở mức độ chính xác cao hơn.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?
   `box_mAP` là 0.900, trong khi `pose_mAP` là 0.826, cho thấy model tìm *người* dễ hơn tìm *khớp*. Điều này có thể do việc xác định vị trí người trong ảnh thường rõ ràng hơn so với việc xác định vị trí các khớp.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn): `train_04`, người #1: OKS 0.612 -> Đảo trái/phải

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?
    Ảnh `train_08`, người #2, khớp `left_wrist` có OKS thấp nhất. Tôi đúng vì dựa vào bằng chứng thị giác rằng cổ tay vẫn có thể được xác định vị trí mặc dù bị che khuất, và tôi đã đặt chấm ước lượng, chuyển v=1.
5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?
   Ảnh `train_08`, người #2, khớp `left_wrist` có OKS thấp nhất. Điều này cho thấy cả tôi và model đều gặp khó khăn trong việc xác định vị trí khớp này, có thể do bị che khuất hoặc khó nhìn thấy.

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

- `train_08`, người #2, khớp `left_wrist`: Cổ tay bị che khuất bởi một vật thể khác, nhưng vẫn có thể nhìn thấy phần lớn khớp. Tôi đã quyết định gán `v=1` vì tôi tin rằng khớp vẫn có thể được xác định vị trí chính xác.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->
