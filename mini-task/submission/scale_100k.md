# Nếu scale lên 100k frames

Họ tên: Lê Võ Khôi Nguyên

Mỗi mini-task trả lời một câu: **"Nếu scale lên 100k frames, lỗi nào sẽ trở thành systematic defect?"** Viết ngay sau
khi ghi comparison log của task đó. Dựa vào một lỗi bạn **thật sự** gặp hôm nay.

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

- **Lỗi & Bằng chứng**: Task `traffic_sign`, ảnh `00088.png` (biển chỉ dẫn cao tốc Bochum 900m) và `00223.png` (biển phụ khoảng cách 300m, thời gian 7-18h). Lỗi ép các biển phụ và biển ngoài 43 class GTSDB vào các class có sẵn hoặc bỏ sót không gán nhãn, và xu hướng zoom đoán class biển ở quá xa thay vì để `unknown`.
- **Vì sao lặp lại có hệ thống**: Khi thiếu ontology chuẩn cho biển phụ và biển chỉ dẫn cao tốc, các annotator sẽ phân loại tùy tiện (người gán `other`, người ép vào `prohibitory` hoặc bỏ qua). Khi scale 100k frames, model sẽ học sai ngữ nghĩa nghiêm trọng (ví dụ nhầm số khoảng cách 300m trên biển phụ thành hạn chế tốc độ, hoặc nhận diện sai biển cấm).
- **Cách phát hiện sớm & Ngăn chặn**:
  - Oversample các lát cắt cao tốc, nút giao đô thị có nhiều biển báo phụ ghép cụm (stacked signs).
  - Tín hiệu QC: Kiểm tra tự động tỷ lệ box mang `sign_class = unknown` ở các box nhỏ (<32px) để phát hiện đoán mò, quét cảnh báo các box có attribute `__undefined__`.

## Traffic light

- **Lỗi & Bằng chứng**: Task `traffic_light`, chuỗi 30 frames `dayClip5`. Lỗi quên đặt cờ `outside` khi đầu đèn trôi ra khỏi biên khung hình (tạo ra ghost box nội suy sai) và lỗi gán sai `relevance` đối với xe ego.
- **Vì sao lặp lại có hệ thống**: Khi làm việc trên video tracking, annotator thường chỉ chú ý frame xuất hiện và keyframe chuyển màu đèn mà quên xử lý frame đèn biến mất ở rìa góc máy. Trên quy mô 100k frames, việc này làm model sinh ra dự đoán ảo ở mép ảnh và gán nhầm tín hiệu đèn của làn rẽ cho hướng đi thẳng của ego, dẫn tới quyết định điều khiển xe nguy hiểm (phanh gấp hoặc vượt đèn).
- **Cách phát hiện sớm & Ngăn chặn**:
  - Oversample các ngã tư lớn có nhiều cột đèn tín hiệu theo làn và các cảnh xe rẽ cua nhanh.
  - Tín hiệu QC: Tự động phát hiện các box track nằm sát mép ảnh (>95% width/height) mà không có keyframe `outside` ở frame kế tiếp; kiểm tra tính liên tục logic của trạng thái đèn (không thể chuyển trực tiếp từ red sang green mà không qua yellow trong 1 frame).
