# Traffic light log

Họ tên: Lê Võ Khôi Nguyên

Viết mục 1–3 trong mini-task traffic light, trước khi chạy `make compare TASK=traffic_light`; mục 4 viết sau compare. Mỗi track là một đầu đèn bạn đã
vẽ.

## 1. Các track

`state` theo frame: ghi dạng khoảng, ví dụ `red 0–14, green 15–29`. Frame đếm từ 0 như trong CVAT.

| Track (#id CVAT) | pictogram | state theo frame | relevance | Bằng chứng cho relevance |
|---|---|---|---|---|
| 0 | arrow_left | red 0–29 | no | Đèn rẽ trái trên giá long môn bên trái, không áp dụng cho xe ego đi thẳng |
| 1 | circle | red 0–14, green 15–29 | yes | Đèn treo chính giữa giá áp dụng trực tiếp cho làn đi thẳng của ego |
| 2 | circle | red 0–14, green 15–29 | yes | Đèn cột bên lề phải cùng pha điều khiển hướng đi thẳng |

## 2. Điểm chuyển state

- Đèn đổi state ở frame nào? Frame liền trước trông ra sao (đèn tắt, hai màu cùng sáng, mờ)? Đèn đổi state từ red sang green tại frame 15. Frame liền trước (frame 14) đèn đỏ chuyển tối trước khi đèn xanh bật sáng rõ rệt ở frame 15.
- Bạn đặt keyframe ở đâu, và bạn đã kiểm tra mọi frame giữa hai keyframe chưa? Đặt keyframe tại frame 0 (bắt đầu track, gán red) và keyframe tại frame 15 (gán green). Đã rà soát từng frame nội suy để điều chỉnh tọa độ box sát vỏ đèn theo đà tiến của xe.

## 3. Các đầu đèn nhỏ ở ngã tư phía xa

Bạn có vẽ không? Nếu có: `relevance` là gì, `state` đọc được ở frame nào? Nếu không: vì sao? Không vẽ các đầu đèn ở ngã tư phía xa vì kích thước quá nhỏ (<15px), bị lóa ánh sáng môi trường và không đủ độ phân giải để đọc state chắc chắn; tuân thủ nguyên tắc không suy diễn khi thiếu bằng chứng quang học.

## 4. Sau khi so với reference

Điền sau `make compare`. Reference (LISA) không có `relevance` và không gán các đèn nhỏ ở xa.

- Khác biệt về state/pictogram, và ai đúng: Thời điểm đổi state từ red sang green ở frame 15 khớp chính xác 100% với reference. Ban đầu thuộc tính pictogram để undefined trong khi reference gán chi tiết circle và arrow_left. Reference đúng về mặt chi tiết pictogram.
- Track của bạn không có trong reference: giữ hay bỏ, vì sao: Cả 3 track đều khớp với 3 track của reference LISA (R#0, R#1, R#2). Toàn bộ 3 track đều được giữ nguyên vì phản ánh đúng các nguồn tín hiệu giao thông chính tại nút giao.
