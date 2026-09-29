# So sánh drivable

> Các số dưới đây là số của công cụ so sánh, không phải ngưỡng chấm.

Polygon BDD100K đổi từ toạ độ normalized sang pixel 1280×720. BDD không có tag needs_review.

Trùng từng đỉnh với reference: 0/15 shape (<= 0,5 px).

## bb5cc516-c98d1fbe.jpg

- direct: IoU 0.504; chỉ reference 17099 px; chỉ bạn 6655 px
- direct: vùng hình học khác reference (17099 px thiếu, 6655 px thừa) — gợi ý `geometry`
- alternative: IoU 0.612; chỉ reference 229 px; chỉ bạn 30499 px
- alternative: vùng hình học khác reference (229 px thiếu, 30499 px thừa) — gợi ý `geometry`
- mọi vùng: IoU 0.799; chỉ reference 1265 px; chỉ bạn 21091 px
- mọi vùng: vùng hình học khác reference (1265 px thiếu, 21091 px thừa) — gợi ý `geometry`

## be860305-899a96c3.jpg

- direct: IoU 0.597; chỉ reference 20342 px; chỉ bạn 9526 px
- direct: vùng hình học khác reference (20342 px thiếu, 9526 px thừa) — gợi ý `geometry`
- alternative: IoU 0.499; chỉ reference 324 px; chỉ bạn 38901 px
- alternative: vùng hình học khác reference (324 px thiếu, 38901 px thừa) — gợi ý `geometry`
- mọi vùng: IoU 0.736; chỉ reference 4043 px; chỉ bạn 31804 px
- mọi vùng: vùng hình học khác reference (4043 px thiếu, 31804 px thừa) — gợi ý `geometry`

## c068a67b-03b6e200.jpg

- direct: IoU 0.920; chỉ reference 3948 px; chỉ bạn 4949 px
- direct: vùng hình học khác reference (3948 px thiếu, 4949 px thừa) — gợi ý `geometry`
- alternative: IoU 0.323; chỉ reference 272 px; chỉ bạn 123573 px
- alternative: vùng hình học khác reference (272 px thiếu, 123573 px thừa) — gợi ý `geometry`
- mọi vùng: IoU 0.548; chỉ reference 4220 px; chỉ bạn 128522 px
- mọi vùng: vùng hình học khác reference (4220 px thiếu, 128522 px thừa) — gợi ý `geometry`

## c3cd6c82-b5d52beb.jpg

- direct: IoU 0.888; chỉ reference 1259 px; chỉ bạn 9118 px
- direct: vùng hình học khác reference (1259 px thiếu, 9118 px thừa) — gợi ý `geometry`
- alternative: IoU 0.296; chỉ reference 2489 px; chỉ bạn 106305 px
- alternative: vùng hình học khác reference (2489 px thiếu, 106305 px thừa) — gợi ý `geometry`
- mọi vùng: IoU 0.518; chỉ reference 3748 px; chỉ bạn 115423 px
- mọi vùng: vùng hình học khác reference (3748 px thiếu, 115423 px thừa) — gợi ý `geometry`

## c723ad21-efed33e5.jpg

- direct: IoU 0.863; chỉ reference 3300 px; chỉ bạn 17821 px
- direct: vùng hình học khác reference (3300 px thiếu, 17821 px thừa) — gợi ý `geometry`
- alternative: IoU 0.364; chỉ reference 4096 px; chỉ bạn 34339 px
- alternative: vùng hình học khác reference (4096 px thiếu, 34339 px thừa) — gợi ý `geometry`
- mọi vùng: IoU 0.722; chỉ reference 7396 px; chỉ bạn 52160 px
- mọi vùng: vùng hình học khác reference (7396 px thiếu, 52160 px thừa) — gợi ý `geometry`

## Dòng gợi ý cho comparison_log.csv

```csv
task,sample,object,difference,error_type,who_is_right,action,note
drivable,bb5cc516-c98d1fbe.jpg,direct,"direct: vùng hình học khác reference (17099 px thiếu, 6655 px thừa)",geometry,,,
drivable,bb5cc516-c98d1fbe.jpg,alternative,"alternative: vùng hình học khác reference (229 px thiếu, 30499 px thừa)",geometry,,,
drivable,bb5cc516-c98d1fbe.jpg,mọi vùng,"mọi vùng: vùng hình học khác reference (1265 px thiếu, 21091 px thừa)",geometry,,,
drivable,be860305-899a96c3.jpg,direct,"direct: vùng hình học khác reference (20342 px thiếu, 9526 px thừa)",geometry,,,
drivable,be860305-899a96c3.jpg,alternative,"alternative: vùng hình học khác reference (324 px thiếu, 38901 px thừa)",geometry,,,
drivable,be860305-899a96c3.jpg,mọi vùng,"mọi vùng: vùng hình học khác reference (4043 px thiếu, 31804 px thừa)",geometry,,,
drivable,c068a67b-03b6e200.jpg,direct,"direct: vùng hình học khác reference (3948 px thiếu, 4949 px thừa)",geometry,,,
drivable,c068a67b-03b6e200.jpg,alternative,"alternative: vùng hình học khác reference (272 px thiếu, 123573 px thừa)",geometry,,,
drivable,c068a67b-03b6e200.jpg,mọi vùng,"mọi vùng: vùng hình học khác reference (4220 px thiếu, 128522 px thừa)",geometry,,,
drivable,c3cd6c82-b5d52beb.jpg,direct,"direct: vùng hình học khác reference (1259 px thiếu, 9118 px thừa)",geometry,,,
drivable,c3cd6c82-b5d52beb.jpg,alternative,"alternative: vùng hình học khác reference (2489 px thiếu, 106305 px thừa)",geometry,,,
drivable,c3cd6c82-b5d52beb.jpg,mọi vùng,"mọi vùng: vùng hình học khác reference (3748 px thiếu, 115423 px thừa)",geometry,,,
drivable,c723ad21-efed33e5.jpg,direct,"direct: vùng hình học khác reference (3300 px thiếu, 17821 px thừa)",geometry,,,
drivable,c723ad21-efed33e5.jpg,alternative,"alternative: vùng hình học khác reference (4096 px thiếu, 34339 px thừa)",geometry,,,
drivable,c723ad21-efed33e5.jpg,mọi vùng,"mọi vùng: vùng hình học khác reference (7396 px thiếu, 52160 px thừa)",geometry,,,
```

Hãy điền `who_is_right`, `action`, `note`; loại lỗi chỉ là gợi ý.
