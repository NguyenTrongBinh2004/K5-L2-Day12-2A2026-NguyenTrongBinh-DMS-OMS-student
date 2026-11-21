# Khai báo dùng AI — Nguyễn Trọng Bình

Nhắc lại: không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Gemini | Cách nạp file `labels_cabin_v1.json` vào CVAT, tạo task 22 ảnh cốt lõi và tóm tắt quy tắc gán nhãn theo Guideline Cabin v1.0 | Dùng để thiết lập project `Day12`, nắm quy tắc gọi ghế theo xe (`rear_right` bên trái ảnh OMS) và quy tắc xác định trái/phải trên ảnh DMS xoay 90° | Có, đối chiếu trực tiếp với `GUIDE.md` và kiểm tra số lượng nhãn hiển thị trên giao diện CVAT |
| 2 | Gemini | Cách sửa các lỗi `[ERROR]` và `[WARN]` từ script `cabin_check.py` (thiếu `frame_meta`, `light` trên ảnh SVIRO, lọc 22 ảnh bằng cờ `--only`) | Bổ sung tag `frame_meta`, chỉnh `light = unknown` cho `S01–S08` và chạy lại lệnh kiểm tra với `--only` | Có, chạy lại `python scripts/cabin_check.py check` đạt `0 lỗi, 0 cảnh báo` và kiểm tra file zip bằng `zipfile -l` |
| 3 | Gemini | Hướng dẫn cấu trúc nội dung các file báo cáo `ir_log.csv`, `class_list_v0.md`, `self_review.md` và đối chiếu câu hỏi trong `exit_ticket.md` | Tham khảo cách trình bày rõ ràng chức năng từng lớp DMS/OMS, tách bạch `IR_sim` với `real_IR` và kiểm tra lại công thức tính thời gian khung hình | Có, rà soát lại toàn bộ số liệu và ví dụ khung hình khớp với dữ liệu thực tế của bộ `G07` và `SUBMISSION.md` |