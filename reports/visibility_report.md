# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 28 skeleton, trung bình 12.43 khớp có v > 0 mỗi người
- Tổng: v=2 326 | v=1 22 | v=0 128

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 21 | 0 | 7 | 0% |
| 1 | left_eye | 19 | 0 | 9 | 0% |
| 2 | right_eye | 21 | 1 | 6 | 4% |
| 3 | left_ear | 13 | 3 | 12 | 11% |
| 4 | right_ear | 16 | 3 | 9 | 11% |
| 5 | left_shoulder | 23 | 1 | 4 | 4% |
| 6 | right_shoulder | 27 | 0 | 1 | 0% |
| 7 | left_elbow | 25 | 0 | 3 | 0% |
| 8 | right_elbow | 23 | 1 | 4 | 4% |
| 9 | left_wrist | 20 | 3 | 5 | 11% |
| 10 | right_wrist | 16 | 4 | 8 | 14% |
| 11 | left_hip | 18 | 1 | 9 | 4% |
| 12 | right_hip | 22 | 0 | 6 | 0% |
| 13 | left_knee | 17 | 1 | 10 | 4% |
| 14 | right_knee | 19 | 0 | 9 | 0% |
| 15 | left_ankle | 14 | 2 | 12 | 7% |
| 16 | right_ankle | 12 | 2 | 14 | 7% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
