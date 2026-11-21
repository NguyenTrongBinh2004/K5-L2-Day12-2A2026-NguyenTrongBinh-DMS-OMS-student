# Danh sách lớp v0 — Nguyễn Trọng Bình · G07

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat`, `seatbelt`) | `seat`: driver / front_passenger; `seatbelt`: worn_correct / worn_incorrect / not_worn / unknown | Xác định sự hiện diện của tài xế và giám sát trạng thái thắt dây an toàn đúng quy cách để phát cảnh báo an toàn | Có (nhận diện được hình dáng cơ thể và dải dây đai, nhưng dễ mất chi tiết trên nền áo tối) |
| 2 | `face` (`eye_left`, `eye_right`) | `open` / `closed` / `unknown` | Phát hiện tình trạng buồn ngủ, nhắm mắt kéo dài hoặc mất tập trung của tài xế | Có (trừ khi bị đốm phản xạ đèn LED IR hoặc đeo kính râm cản tia hồng ngoại) |
| 3 | `face` (`gaze_zone`) | `road` / `mirror_l` / `mirror_r` / `mirror_c` / `cluster` / `center` / `lap` / `other` | Theo dõi vùng nhìn để phát hiện tài xế rời mắt khỏi mặt đường quá thời gian an toàn | Có (xác định qua hướng đầu và vị trí đồng tử dưới nguồn sáng NIR) |
| 4 | `face` (`glasses`) | `none` / `clear` / `sun` / `unknown` | Nhận biết tài xế có đeo kính hay không để điều chỉnh độ tin cậy của mô hình theo dõi mắt | Có (tuy nhiên một số tròng kính râm có thể trông trong suốt trên ảnh NIR) |
| 5 | `face13` (13 điểm mốc khuôn mặt) | 13 tọa độ điểm (mắt, mũi, miệng) kèm cờ `occluded` / `outside` | Ước lượng góc quay đầu (yaw, pitch, roll), độ mở mắt và hành vi ngáp của tài xế | Có (nhưng các điểm vùng cằm/miệng dễ bị che khuất trong bóng tối sâu hoặc sau vật thể) |
| 6 | `hand` (`whose`, `side`, `on_wheel`) | `whose`: driver/passenger; `side`: left/right; `on_wheel`: yes/no/unknown | Giám sát việc tài xế có giữ tay trên vô lăng hay đang thực hiện thao tác gây xao nhãng | Có (nhận diện rõ qua hình dạng bàn tay và vị trí tương đối so với vô lăng) |
| 7 | `phone` (`state`) | `held` / `mounted` / `lap` | Phát hiện hành vi cầm hoặc sử dụng điện thoại khi lái xe để kích hoạt cảnh báo mất tập trung | Có (thấy khung máy và màn hình sáng, nhưng dễ nhầm với vật tối màu nếu bị che khuất) |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat`, `seatbelt`) | `seat`: front_passenger / rear_left / rear_middle / rear_right; `seatbelt`: worn_correct / worn_incorrect / not_worn / unknown | Đếm số lượng hành khách theo từng ghế để điều khiển bung túi khí thông minh và nhắc nhở thắt dây an toàn | Có (hình dáng người rõ, nhưng khó phân biệt dây đai trên trang phục tối màu) |
| 2 | `face` (khuôn mặt hành khách) | Bounding box khuôn mặt người lớn | Xác nhận sự hiện diện của người ngồi thật (phân biệt với đồ vật lớn) và hỗ trợ ước lượng tư thế ngồi | Có (nhận diện được đường nét khuôn mặt dù mất thông tin màu sắc) |
| 3 | `child_seat` (`seat`, `occupied`) | `seat`: vị trí ghế; `occupied`: no / unknown | Nhận diện ghế trẻ em lắp trên xe để điều chỉnh chế độ túi khí và theo dõi an toàn trẻ em | Có (nhận diện tốt qua cấu trúc khung đặc trưng của ghế trẻ em) |
| 4 | `infant_seat` (`seat`, `facing`) | `seat`: vị trí ghế; `facing`: rear / front | Phát hiện nôi xách em bé và hướng quay của nôi nhằm kích hoạt cảnh báo chống bỏ quên trẻ trên xe (CPD) | Có (nhận diện rõ hình dáng nôi và hướng quay về trước hoặc sau) |
| 5 | `object` (`seat`, `type`) | `seat`: vị trí ghế; `type`: bag / box / cup / other | Phân biệt hành lý/đồ vật đặt trên ghế với hành khách thực để tránh báo động giả nhắc thắt dây an toàn | Có (thấy rõ hình khối vật thể nhưng mất đặc trưng màu sắc và chất liệu bề mặt) |
| 6 | `frame_meta` (`camera_blocked`) | `yes` / `no` | Phát hiện ống kính camera cabin bị che khuất hoặc bám bẩn để hệ thống chủ động báo lỗi cảm biến | Có (nhận biết qua vùng ảnh bị che mờ hoặc tối đen bất thường) |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: Khi tài xế đưa tay áp sát vùng tai/má như đang nghe điện thoại nhưng bàn tay che kín toàn bộ vật thể (không lộ cạnh, góc hay màn hình điện thoại), guideline có cho phép gán nhãn `phone` dựa trên ngữ cảnh tư thế tay hay bắt buộc bỏ qua?
   Khung ví dụ: `G07 D05` (`D05.png`)
   Bạn tạm gán thế nào và vì sao: Tạm thời không vẽ box `phone`, chỉ gán box `hand` (`whose = driver`, `side = right`, `on_wheel = no`) vì Guideline Cabin v1.0 mục 4.7 quy định chỉ vẽ `phone` khi nhìn thấy rõ ít nhất một cạnh, góc hoặc màn hình điện thoại.
2. Câu hỏi: Đối với ảnh DMS trong vùng tối sâu khiến một bên mắt hoặc nửa dưới khuôn mặt chìm hoàn toàn vào bóng tối không thể xác định vị trí chính xác (như khi tài xế cúi gập người hoặc bị vật thể che khuất), các điểm `face13` tại vùng tối đen đó nên gắn cờ `occluded` (ước lượng vị trí) hay `outside` (không đoán được)?
   Khung ví dụ: `G07 D06` (`D06.png`) và `G07 D03` (`D03.png`)
   Bạn tạm gán thế nào và vì sao: Tạm thời đặt các điểm bị che nhưng còn ước lượng chắc chắn vị trí giải phẫu (như vùng môi sau chai nước ở `D03`) với cờ `occluded`, còn các điểm chìm hẳn trong vùng tối đen không thể xác định chính xác (vùng cằm và miệng ở `D06`) thì bật cờ `outside` theo hướng dẫn mục 4.6.