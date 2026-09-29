# Nếu scale lên 100k frames

Họ tên: Lê Võ Khôi Nguyên

Mỗi mini-task trả lời một câu: **"Nếu scale lên 100k frames, lỗi nào sẽ trở thành systematic defect?"** Viết ngay sau
khi ghi comparison log của task đó. Dựa vào một lỗi bạn **thật sự** gặp hôm nay. Xoá mọi chữ `TODO` khi xong.

Mỗi câu trả lời có 3 phần: lỗi (và bằng chứng: task + sample), vì sao nó lặp lại có hệ thống thay vì ngẫu nhiên,
và cách phát hiện sớm (lát nào cần oversample, tín hiệu QC nào).

## Lane

- **Lỗi & Bằng chứng**: Task `lane`, ảnh `bb890202-d9d48310.jpg`. Lỗi tách một vạch đứt (dashed lane marking) thành nhiều đoạn polyline riêng lẻ và để sót thuộc tính `laneTypes`/`laneStyle`.
- **Vì sao lặp lại có hệ thống**: Annotator chưa nắm vững ontology sẽ mặc định coi mỗi vệt sơn đứt rời rạc là một instance độc lập thay vì một ranh giới làn liên tục. Điều này lặp lại trên toàn bộ các cảnh cao tốc nhiều làn, khiến model học sai cấu trúc làn đường (tưởng các nét đứt là vật cản hoặc vạch rời rạc).
- **Cách phát hiện sớm & Ngăn chặn**:
  - Oversample các lát dữ liệu cao tốc ban ngày và đường nhiều làn để audit sớm ở 500 frame đầu.
  - Tín hiệu QC: Kiểm tra tự động các polyline có độ dài quá ngắn nằm thẳng hàng, hoặc quét cờ cảnh báo attribute còn mang giá trị `__undefined__` trước khi lock task.

## Drivable area

- **Lỗi & Bằng chứng**: Task `drivable`, ảnh `c068a67b-03b6e200.jpg` và `bb5cc516-c98d1fbe.jpg`. Lỗi vẽ polygon vùng `alternative` quá rộng lấn vào khoảng trống giữa/sau các xe đỗ ven đường, hoặc kéo dài polygon qua các vùng bị che khuất bởi giá đỡ kính/vết nước mưa.
- **Vì sao lặp lại có hệ thống**: Annotator thường bị đánh lừa bởi màu sắc mặt nhựa đường ("thấy đường là tô") thay vì xét đến tính khả thi về mặt chức năng và an toàn giao thông. Khi scale 100k frames, lỗi này sẽ khiến hệ thống lái tự động hiểu nhầm lề đỗ xe là làn di chuyển được, tiềm ẩn nguy cơ va chạm nghiêm trọng.
- **Cách phát hiện sớm & Ngăn chặn**:
  - Oversample các lát dữ liệu đô thị có xe đỗ dày đặc (urban parking) và thời tiết mưa/chói sáng.
  - Tín hiệu QC: Kiểm tra độ giao cắt (intersection) giữa bounding box của xe tĩnh (parked car) và polygon drivable area để phát hiện ngay hiện tượng tô tràn vào bãi đỗ.

## Traffic sign

TODO

## Traffic light

TODO
