# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 29 skeleton, trung bình 15.86 khớp có v > 0 mỗi người
- Tổng: v=2 341 | v=1 119 | v=0 33

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 24 | 5 | 0 | 17% |
| 1 | left_eye | 22 | 7 | 0 | 24% |
| 2 | right_eye | 22 | 7 | 0 | 24% |
| 3 | left_ear | 13 | 16 | 0 | 55% |
| 4 | right_ear | 17 | 12 | 0 | 41% |
| 5 | left_shoulder | 27 | 2 | 0 | 7% |
| 6 | right_shoulder | 27 | 2 | 0 | 7% |
| 7 | left_elbow | 23 | 6 | 0 | 21% |
| 8 | right_elbow | 26 | 3 | 0 | 10% |
| 9 | left_wrist | 17 | 12 | 0 | 41% |
| 10 | right_wrist | 19 | 9 | 1 | 31% |
| 11 | left_hip | 23 | 5 | 1 | 17% |
| 12 | right_hip | 23 | 5 | 1 | 17% |
| 13 | left_knee | 16 | 7 | 6 | 24% |
| 14 | right_knee | 15 | 8 | 6 | 28% |
| 15 | left_ankle | 15 | 5 | 9 | 17% |
| 16 | right_ankle | 12 | 8 | 9 | 28% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
