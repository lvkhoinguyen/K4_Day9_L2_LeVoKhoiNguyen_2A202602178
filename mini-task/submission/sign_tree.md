# Traffic sign tree

Họ tên: Lê Võ Khôi Nguyên · Chế độ: cá nhân

Viết sau mini-task traffic sign (phút ~155). Dựa vào những biển **bạn đã vẽ** trong 7 ảnh core, không chép danh sách
43 class.

## 1. Cây của bạn

Chỉ liệt kê class có trong ảnh core. Đếm số box của từng class. Class có 1 box trong cả batch là ứng viên "hiếm".

| family | class (`sign_class`) | Số box trong core | Phổ biến / hiếm | Ảnh ví dụ |
|---|---|---|---|---|
| prohibitory | 00 speed limit 20 | 1 | hiếm | 00054.png |
| prohibitory | 01 speed limit 30 | 2 | phổ biến | 00026.png, 00223.png |
| prohibitory | 02 speed limit 50 | 2 | phổ biến | 00073.png |
| prohibitory | 08 speed limit 120 | 2 | phổ biến | 00088.png |
| prohibitory | 09 no overtaking | 1 | hiếm | 00073.png |
| prohibitory | 10 no overtaking (trucks) | 3 | phổ biến | 00073.png, 00088.png |
| mandatory | 33 go right | 1 | hiếm | 00206.png |
| mandatory | 34 go left | 1 | hiếm | 00206.png |
| danger | 27 pedestrian crossing | 1 | hiếm | 00054.png |
| danger | 31 animals | 2 | phổ biến | 00073.png |
| other | 12 priority road | 1 | hiếm | 00054.png |
| other | 13 give way | 2 | phổ biến | 00206.png |
| other | unknown | 4 | phổ biến | 00088.png, 00223.png |

## 2. Hai quyết định merge/split

Mỗi quyết định: giữ tách hay gộp, vì sao, và cái giá nếu chọn sai (model downstream nhầm gì).

**Quyết định 1 — `09 no overtaking` và `10 no overtaking (trucks)`: tách hay gộp?**
Giữ tách biệt hoàn toàn. Biển 09 cấm mọi xe cơ giới vượt nhau, trong khi biển 10 chỉ cấm xe tải vượt xe khác còn xe con (ego vehicle) vẫn được phép vượt hợp pháp. Nếu gộp chung hai nhãn này, hệ thống lái tự động downstream của xe con sẽ hiểu nhầm lệnh cấm và không dám vượt xe chạy chậm trên cao tốc gây cản trở giao thông; hoặc ngược lại nếu áp dụng cho xe tải tự hành sẽ dẫn đến vi phạm luật giao thông nghiêm trọng.

**Quyết định 2 — nhóm `other` của GTSDB khi dùng ở Việt Nam.**
GTSDB xếp biển hết hạn chế (`06`, `32`, `41`, `42`) vào `other`. QCVN 41:2024/BGTVT xếp biển hết hiệu lực
(`DP.133`–`DP.135`) vào nhóm **biển báo cấm**. Cây của bạn theo cách nào, và cần rule gì để hai người label giống nhau?
Cây của tôi tuân thủ theo GTSDB trong bài lab này (xếp biển hết hạn chế và biển ưu tiên vào `other`). Tuy nhiên, khi chuyển giao sang triển khai tại Việt Nam theo QCVN 41:2024/BGTVT, cần rule đồng nhất: xây dựng bảng ánh xạ cố định (mapping table) quy định toàn bộ biển nhóm DP.133-DP.135 thuộc family `prohibitory`. Rule bắt buộc: Annotator phải tra cứu mã biển trên bảng quy ước chuẩn của dự án thay vì suy luận theo hình dáng trực quan.

## 3. Chính sách cho class hiếm và biển không đọc được

Khi gặp biển không có trong 43 class, hoặc quá nhỏ để đọc: bạn chọn `sign_family`, `sign_class`, `readable` thế nào?
Dẫn một box cụ thể (ảnh + vị trí) làm bằng chứng.
Chính sách:
- Nếu biển nằm ngoài 43 class GTSDB (biển phụ khoảng cách, thời gian, biển chỉ dẫn cao tốc): gán `sign_family = other`, `sign_class = unknown`, `readable = yes` (nếu đọc rõ ký tự/số) hoặc `uncertain`.
- Nếu biển thuộc 43 class nhưng quá nhỏ/mờ (<30px) không đủ chi tiết phân biệt chữ số: chọn `sign_family` theo hình dáng/màu sắc (ví dụ tròn viền đỏ -> `prohibitory`), gán `sign_class = unknown`, và đặt `readable = uncertain` hoặc `no`. Tuyệt đối không zoom rồi suy diễn class.
- Bằng chứng cụ thể: Biển phụ thời gian `7 - 18 h` trên ảnh `00223.png` gắn dưới biển tốc độ 30. Biển này có chữ số rõ ràng nhưng không nằm trong 43 class GTSDB, nên được gán `sign_family = other`, `sign_class = unknown`, `readable = yes`.

## 4. Dòng decision log tương ứng

Id của dòng trong `decision_log.csv` ghi rule ở mục 2 hoặc 3: DEC-03
