# Tự đánh giá — Nguyễn Trọng Bình · G07

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_ir.png | `frame_meta` | `wrong_class` | Thuộc tính `light` ban đầu chọn nhầm sang `day`/`night` thay vì `unknown` cho ảnh dựng SVIRO; đã chỉnh lại thành `unknown`. | Đã sửa |
| S04_rgb.png | `person` | `ok` | Kiểm tra lại quy tắc ghế tính theo chiều xe (camera nhìn ngược về sau nên trái ảnh là `rear_right`), xác nhận gán đúng. | Đã sửa (ok) |
| D03.png | `face13` | `flag` | Rà soát các điểm môi và khóe miệng bị chai nước che khuất, đảm bảo bật đầy đủ cờ `occluded`. | Đã sửa (ok) |
| D05.png | `hand` / `phone` | `ok` | Kiểm tra tay phải đưa lên gần tai nhưng không thấy rõ cạnh/màn hình điện thoại nên giữ đúng quy tắc không vẽ `phone`. | Đã sửa (ok) |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Quên gắn tag `frame_meta` trước khi vẽ box đầu tiên trên các khung hình (thiếu tag ở 16 ảnh ở lần kiểm tra đầu) và để thuộc tính `light` khác `unknown` trên ảnh dựng SVIRO (`S01–S08`).

Vì sao mình mắc: Tập trung vẽ ngay các bounding box đối tượng (`person`, `child_seat`, `face`) mà bỏ qua bước gắn tag cấp khung hình đầu tiên, đồng thời quên rằng ảnh SVIRO là ảnh tổng hợp 3D nên không có thời gian ngày/đêm thật.

Lần sau tránh bằng cách: Tuân thủ nghiêm ngặt thứ tự thao tác ở mục 4.3 của Guideline (gắn tag `frame_meta` ngay khi mở ảnh mới trước khi vẽ bất kỳ box nào) và chạy script `cabin_check.py` sớm tại các mốc Checkpoint A, B.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó: Ở các khung hình `D##` bị xoay ngang 90° (`D01`, `D02`), khi khởi tạo skeleton `face13` trên CVAT, mẫu điểm mặc định nằm thẳng đứng nên dễ nhầm lẫn trục trái/phải của hai mắt; qua rà soát theo Guideline §4.6, cần kéo lại toàn bộ các điểm sao cho `left_eye_*` có tọa độ `y` lớn hơn `right_eye_*` và đặt điểm nằm chính xác tại mép mí mắt thay vì giữa tròng mắt.