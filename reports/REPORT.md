# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Phan Ngọc Hòa   Nhóm: ______   Ngày: 16/09/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | 341 / 119 / 33 |
| Thời gian trung bình mỗi ảnh | 4 phút |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. left_ear=57%
2. right_ear=43%
3. left_wrist=43%

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

Không, đây chỉ là những khớp **hay bị che nhất** chứ không phải khớp **khó xác định vị trí giải phẫu nhất**. Tai và cổ tay có tỷ lệ `v=1` cao do thường xuyên bị tóc, mũ bảo hiểm hoặc tay lái che khuất, nhưng vị trí của chúng rất dễ suy đoán nhờ gióng theo trục mắt-mũi hoặc hướng đi của cẳng tay. Ngược lại, khớp khó gán nhất là hông: dù không bị vật cản ngoài che nhưng luôn bị quần áo che lấp mốc xương thực sự, khiến việc xác định tâm xoay ổ cối theo chiều dọc thân người dễ bị lệch nhất.

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.941 | 0.941 |
| OKS@0.50 | 0.966 | 1 |
| OKS@0.75 | 0.966  | 1 |
| Lỗi `dao_trai_phai` | 0 | 0 |
| Lỗi `nham_nguoi` | 0 | 0 |
| Lỗi `xoa_khop_bi_che` | 0 | 0 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

Bị thiếu một người ở train_13.jpg người do quá mờ. Nên chỉ cần vẽ thêm

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.

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
| pose_mAP50 | 0.8450 | 0.8450 | 0.0000 |
| pose_mAP50-95 | 0.6853 | 0.6908 | +0.0055 |
| pose_precision | 0.9734 | 0.9792 | +0.0058 |
| pose_recall | 0.8462 | 0.8462 | 0.0000 |
| box_mAP50-95 | 0.8119 | 0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?

   Tăng 0.0055 (từ 0.6853 lên 0.6908). 20 ảnh hơi giống tập test nên model khớp tốt hơn một chút. Mức tăng nhỏ, chưa đủ kết luận model “giỏi hơn hẳn”; chỉ cho thấy nhãn của tôi không phá hỏng hoàn toàn kiến thức gốc.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?

   Sau fine-tune, box_mAP50-95 = 0.8041, pose_mAP50-95 = 0.6908, chênh 0.1133. Model tìm người dễ hơn tìm khớp. Ô chữ nhật chỉ cần bao đúng thân; 17 khớp phải đúng từng điểm, còn bị che, trùng người, và dễ đảo trái/phải.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):

   Ảnh `test_03`: model **lệch nhẹ** — cổ tay người đứng sau bị lệch xíu khỏi tay lái do bị che khuất một phần. Không phải trượt hẳn vì vẫn nhận diện đúng người và đúng vùng khớp.

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?

   `train_12` OKS 0.797, thấp nhất. Tôi đúng: người ngồi nghiêng, tôi gắn các khớp chân theo trục cẳng chân nhìn thấy và đối chiếu khớp với gold; model đoán trượt khớp gối và cổ chân xuống thấp theo tỉ lệ đứng thẳng thông thường.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?

   Có, cùng `train_12`. Ảnh góc chụp nghiêng, chân bị che và phối cảnh gập. Cả người và máy đều dễ lệch nhẹ khớp gối / cổ chân. Đây là ca khó của dữ liệu, không chỉ lỗi thao tác của tôi.

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

Ảnh `train_06`, người lái xe, khớp `left_hip`. Phần hông bị trang phục dài che hết, không thấy da hay nếp khớp, nhưng hông chắc chắn còn trong khung — tôi nhìn thấy hai gối và hai vai. Theo luật lớp, bị che mà còn trong ảnh thì đặt chấm ước lượng trên đường vai–gối và để `v=1`, không Outside. Nếu để `v=0`, khớp này bị loại khỏi điểm OKS và model sẽ học rằng “hông mặc quần = không có khớp”.
