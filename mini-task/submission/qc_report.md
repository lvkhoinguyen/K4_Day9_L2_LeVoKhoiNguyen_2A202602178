# QC report

Họ tên: Lê Võ Khôi Nguyên · Chế độ: cá nhân
Guideline dùng: `GUIDE.md` + 4 card, bản phát ngày học.

Viết ở phút 205–225.

- **Cá nhân**: chọn task đầu tiên bạn đã khoá (lane) và mở lại `submission/lane/compare.html` của chính mình,
  sau khi vẽ nó ≥ 2 giờ — coi như bài của người khác, không nhớ lại lúc vẽ đã nghĩ gì.

## 1. Sample plan

Không đủ thời gian xem hết. Chọn **6 sample** và nói vì sao chọn. Lấy theo lát dễ lỗi (ngã tư, crosswalk, đêm/mưa,
lóa, biển nhỏ, điểm chuyển state), không lấy ngẫu nhiên.

| # | Task | Sample (ảnh / frame) | Lát (vì sao chọn) |
|---|---|---|---|
| 1 | lane | bb890202-d9d48310.jpg | Cao tốc nhiều làn có vạch đứt dài và xe SUV phía trước che khuất tầm nhìn |
| 2 | lane | c3cd6c82-b5d52beb.jpg | Đường thẳng ban ngày có vạch biên liền nét màu trắng bên phải |
| 3 | drivable | c068a67b-03b6e200.jpg | Đô thị có xe đỗ dày đặc sát mép đường hai bên dễ tô nhầm |
| 4 | drivable | bb5cc516-c98d1fbe.jpg | Thời tiết mưa làm mờ kính lái và giá đỡ gương che góc trên |
| 5 | traffic_sign | 00088.png | Cao tốc sương mù có biển chỉ dẫn lớn trên long môn và biển hạn chế tốc độ |
| 6 | traffic_sign | 00223.png | Đường dân cư có cụm biển hạn chế tốc độ kèm 2 biển phụ chữ nhật |

## 2. Lỗi tìm thấy

Ít nhất 1 lỗi geometry, 1 lỗi attribute và 1 ca cần vào decision log. Nếu không tìm thấy loại nào, ghi rõ "đã xem,
không có".

- `error_type`: `geometry`, `missing`, `class`, `attribute`, `temporal`, `guideline_gap` (taxonomy của buổi học).
- `severity` (quy ước của lab, không phải thang của doanh nghiệp):
  `critical` = đổi quyết định của ego (state/relevance sai, drivable lấn sang làn ngược chiều, mất lane ngay trước xe);
  `major` = sai attribute hoặc geometry mà model sẽ học theo; `minor` = lệch nhỏ, không đổi nghĩa.
- `action`: `accept`, `rework`, `escalate`.

| Task | Sample | Object | Mô tả lỗi | error_type | severity | action | Downstream sai gì nếu bỏ qua |
|---|---|---|---|---|---|---|---|
| lane | bb890202-d9d48310.jpg | vach_dut | Tách vạch đứt thành nhiều polyline rời rạc thay vì 1 đường liên tục qua tim | geometry | major | rework | Model dự đoán các đoạn đứt là chướng ngại vật hoặc đứt gãy làn |
| lane | c3cd6c82-b5d52beb.jpg | R3/B2_vach_bien | Chưa chọn laneTypes và laneStyle để sót __undefined__ | attribute | major | rework | Model không phân biệt được vạch ranh giới làn và lề đường |
| traffic_sign | 00088.png | B3_bien_bochum | Biển chỉ dẫn đường cao tốc 900m không thuộc 43 class GTSDB | guideline_gap | minor | escalate | Annotator ép class tùy tiện làm nhiễu dữ liệu huấn luyện |

## 3. Kết luận cho batch

- Accept / rework / escalate cả batch, và lý do: Accept with rework. Tổng thể các vùng drivable và bám lane được vẽ sát thực tế; cần rework các polyline bị cắt khúc ngắn ở task lane và bổ sung các thuộc tính chưa được gán trước khi release dữ liệu sang pipeline huấn luyện.
- Note cho người label (1–2 câu, nói cách sửa — với cá nhân thì viết cho chính mình): Luôn vẽ 1 polyline duy nhất bám theo tim của chuỗi vạch đứt cho đến khi gặp vật thể che khuất thì dừng lại ngay mép ngoài vật thể; tuyệt đối kiểm tra không để sót attribute mang giá trị undefined trước khi export bài.
- Known limitation phải ghi khi handoff (điều guideline chưa quyết): Chưa có quy chuẩn thống nhất về việc gắn nhãn biển phụ chữ nhật (bổ trợ thời gian, khoảng cách) và biển chỉ dẫn trên giá long môn khi đối chiếu với benchmark 43 class GTSDB.
