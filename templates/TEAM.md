# TEAM — Ngày 12

Mã bộ ảnh: **G07** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Trọng Bình | 2A202603099 | có | Nguyễn Hoàng Diệu | 5 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- Không có (đã rà soát và thống nhất toàn bộ 22 khung hình theo Guideline Cabin v1.0).

## Cá nhân

### NguyenTrongBinh-2A202603099
- Phần mình làm (ngoài 22 ảnh của mình, ví dụ ai review ai, ai tổng hợp ca hỏi coach): Hoàn thành gán nhãn đủ 22 khung hình (S01–S08, D01–D06), đối chiếu review cùng Nguyễn Hoàng Diệu, lập log xử lý các ca bất đồng/mơ hồ trong `disagreement_log.csv`, chạy kiểm tra `cabin_check.py` đạt 0 lỗi và tổng hợp `ir_log.csv`, `class_list_v0.md`.
- Điều mình học được hôm nay: Nắm vững quy tắc gọi vị trí ghế theo chiều xe (camera OMS nhìn ngược về sau nên trái ảnh là `rear_right`), gọi trái/phải theo người trên ảnh DMS xoay 90° (`left_eye_*` có tọa độ `y` lớn hơn), và luôn chọn `unknown` hoặc bật cờ `occluded`/`outside` thay vì đoán mò khi bị bóng tối hoặc vật thể che khuất.