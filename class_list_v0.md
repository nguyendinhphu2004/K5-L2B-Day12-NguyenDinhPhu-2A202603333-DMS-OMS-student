# Danh sách lớp v0 — Nguyen Dinh Phu · G07

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (8 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_left, eye_right | open / closed / unknown | Phát hiện buồn ngủ: đo tỉ lệ thời gian mắt nhắm và tần suất chớp mắt. `unknown` cho phép model biết khi nào không đủ dữ liệu, thay vì báo nhầm | Có, trừ khi tròng kính phản xạ đèn LED hoặc bị tay che (D01, D04) |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện mất tập trung: tính thời gian tài xế không nhìn đường; phân biệt nhìn gương (an toàn) với nhìn đùi hay màn hình | Hướng đầu thì thấy; hướng mắt khó khi đeo kính hoặc mặt nhỏ |
| 3 | glasses | none / clear / sun / unknown | Chọn thuật toán đọc mắt phù hợp và hạ độ tin cậy khi có kính. Kính râm làm mất mắt, kính trong gây phản xạ | Một phần: kính râm có thể trông trong suốt trên NIR (D06) |
| 4 | face (box) | tọa độ hộp | Điều kiện đầu vào của mọi chức năng DMS: có mặt tài xế hay không, và cắt vùng mặt để xử lý tiếp | Có, trừ khi mặt quay đi hoặc bị che gần hết |
| 5 | face13 (13 điểm mặt) | tọa độ + cờ occluded / outside | Ước lượng tư thế đầu, độ mở mắt, ngáp (độ mở miệng). Cờ che giúp model không học điểm đoán | Có; điểm mắt thường bị che bởi phản xạ kính. Chỉ dùng khi mặt rộng từ 60 px |
| 6 | hand (whose, side, on_wheel) | driver / passenger; left / right; yes / no / unknown | Phát hiện tay rời vô lăng (cảnh báo khi chế độ hỗ trợ lái cần tay) và đếm tay để biết tài xế đang làm gì | Có; tay xa camera hoặc gần vùng tối khó thấy (D02) |
| 7 | phone (state) | held / mounted / lap | Phát hiện dùng điện thoại khi lái, một nguyên nhân mất tập trung phổ biến. `state` phân biệt cầm tay với đã gắn giá | Có nếu thấy cạnh hoặc màn hình; khó khi ngón tay che hết máy (D05) |
| 8 | seatbelt (trên person) | worn_correct / worn_incorrect / not_worn / unknown | Nhắc thắt dây an toàn và phát hiện đeo sai (dây dưới nách, sau lưng) | Có khi dây tối trên áo sáng; mất khi cả hai cùng tối |

## OMS (8 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person + seat | driver / front_passenger / rear_left / rear_middle / rear_right | Đếm người và biết ai ngồi ghế nào: nhắc thắt dây theo ghế, điều khiển túi khí theo ghế có người | Có (hình dáng cơ thể). Ghế gọi theo xe, camera nhìn ngược nên trái ảnh là phải xe |
| 2 | seatbelt (trên person) | not_worn / unknown (SVIRO không có worn_*) | Nhắc thắt dây cho hàng ghế sau | Một phần: dây mảnh, tối bị mất trên ảnh IR-sim tối |
| 3 | child_seat (seat, occupied) | occupied: no / unknown | Biết ghế nào có ghế trẻ em: tắt túi khí ghế trước khi có ghế trẻ em, kiểm tra ISOFIX | Có (hình dạng lớn, rõ) (S04, S06, S07) |
| 4 | infant_seat (seat, facing) | facing: rear / front | Ghế em bé quay ngược đặt ở ghế trước thì phải tắt túi khí; cũng là đầu vào cho cảnh báo quên trẻ trong xe | Có (hình dạng nôi xách, quai xách) |
| 5 | object (seat, type) | bag / box / cup / other | Phát hiện đồ bỏ quên khi xuống xe và vật nặng không cố định có thể gây nguy hiểm khi phanh gấp | Hình dạng thì có, màu thì mất (hộp carton ở S07 thành xám) |
| 6 | face (box, OMS) | tọa độ hộp | Phân biệt người thật với vật hay áp phích, hỗ trợ ước lượng tư thế ngồi và độ tuổi gần đúng | Có khi mặt hướng về camera; hay bị che bởi tóc, tay |
| 7 | seat (zone) | rear_left / rear_middle / rear_right | Gắn mọi phát hiện vào đúng vị trí ghế để cảnh báo đúng chỗ và không đếm trùng người | Có (vị trí ghế cố định theo xe) |
| 8 | frame_meta (modality, light, camera_blocked) | rgb / ir; day / night / unknown; yes / no | Chọn pipeline phù hợp (RGB hay IR), biết khi nào dữ liệu không đáng tin, và cảnh báo khi camera bị che | Có (độ sáng tổng thể, vùng đen toàn khung) |

## 2 câu hỏi leo thang

1. Câu hỏi: Guideline §3 ghi "bộ ảnh không có trẻ em ngồi, thấy hình giống trẻ em thì báo coach, không gán", nhưng có cảnh trẻ hoặc em bé đang ngồi trong ghế trẻ em, ghế em bé. Với những cảnh đó, có vẽ `person` cho trẻ không, và `child_seat`/`infant_seat` ghi `occupied` thế nào khi `occupied` không có giá trị `yes`?
   Khung ví dụ: G07 S01, S03, S05, S08 (cả `_rgb` và `_ir`).
   Bạn tạm gán thế nào và vì sao: Không vẽ `person` cho trẻ và không vẽ box nào ở 4 cảnh này, chỉ giữ tag `frame_meta`, theo hướng dẫn "không gán" của guideline và trao đổi với coach. Hệ quả là model sẽ không thấy ghế có trẻ, nên cần quy tắc chính thức trước khi dạy chức năng quên trẻ trong xe.
2. Câu hỏi: Với kính viền dày có tròng tối trên ảnh NIR, nên gán `glasses` là `clear`, `sun` hay `unknown`, khi guideline nói kính râm có thể trông trong suốt trên NIR nhưng cũng nói `unknown` khi không nhìn rõ vùng mắt?
   Khung ví dụ: G07 D06 (tròng tối, thấy một phần mắt qua kính), so với D01 (kính trong rõ, nhưng bị đốm phản xạ).
   Bạn tạm gán thế nào và vì sao: `glasses = unknown` và hai mắt `unknown` (điểm mắt bật `occluded`), vì không chắc là kính râm hay kính trong. Ghi `none` hoặc `clear` sai sẽ dạy model rằng người đeo kính không có kính, và ghi `sun` sai sẽ làm mất dữ liệu mắt hợp lệ.
