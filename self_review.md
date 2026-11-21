# Tự đánh giá — Nguyễn Đình Phú · G07

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng                                | Loại lỗi  | Ghi chú                                                                                             | Đã sửa?                        |
| --- | ---------------------------------------- | --------- | --------------------------------------------------------------------------------------------------- | ------------------------------ |
| S01 | ghế bên trái (`infant_seat`, rear_right) | `missing` | bỏ sót ghế này ở cả `_rgb` và `_ir`; chỉ ra và đã thêm. Sau đó S01 bị bỏ nhãn vì có trẻ em          | Đã sửa, rồi bỏ cảnh theo coach |
| S02 | người lớn rear_left (`person` + `face`)  | `ok`      | Review chéo cho thấy thiếu box `face`; giữ vì người lớn OMS cần `face` (§4.2), ghế gọi theo xe đúng | Không cần sửa                  |
| D05 | điện thoại                               | `missing` | Có điện thoại cầm ở tay gần mặt mà không vẽ `phone`                                                 | Đã thêm `phone` (held)         |
| D06 | bàn tay                                  | `missing` | Đầu tiên chỉ đánh nhãn 1 bàn tay (left); thêm bàn tay còn lại (right)                               | Đã thêm                        |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Bỏ sót đối tượng (`missing`). Bản đầu thiếu ghế `infant_seat` ở S01, thiếu `phone` ở D05 và thiếu một `hand` ở D06. Cả ba lần đều là vật hoặc bộ phận bị che một phần hoặc nằm sát mép, không phải vật nổi bật.

Vì sao mình mắc: Chưa tăng sáng nên chưa thấy rõ ràng

Lần sau tránh bằng cách: Ảnh tối thì bật tăng sáng

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: **D04, `hand.side`**. Mình gán ngược trái/phải cho 2 bàn tay; Lê Vĩnh Khải gán đúng. Trên ảnh D## xoay 90°, tay bên trái của tài xế nằm ở phía y lớn hơn, nhưng hai tay ở D04 chồng lên nhau nên mình nhìn theo vị trí trên màn hình.

Mình học được gì từ dòng đó: Quy tắc "y lớn hơn là bên trái" không chỉ áp dụng cho mắt mà cho cả tay. Khi hai tay chồng nhau, so tâm box theo trục y rồi mới chọn `side`. Đã sửa trong `export_final_v2.zip`.
