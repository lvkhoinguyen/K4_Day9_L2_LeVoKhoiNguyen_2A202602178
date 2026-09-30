# So sánh traffic_light

> Các số dưới đây là số của công cụ so sánh, không phải ngưỡng chấm.

Track LISA dayClip5, 30 frame. LISA không gán nhãn đèn nhỏ ở ngã tư phía xa và không có relevance — box không khớp GT chưa chắc là thừa.

Trùng từng đỉnh với reference: 0/90 shape (<= 0,5 px).

## dayClip5--01606.jpg

- R#2/B#0: cả reference và bạn đều không đổi state
- R#2/B#0 pictogram, frame 0–29: bạn chưa chọn, reference arrow_left — gợi ý `attribute`
- B#0: relevance=chưa chọn (không so với GT)
- R#0/B#1: frame đổi state reference 15; bạn 15
- R#0/B#1 pictogram, frame 0–29: bạn chưa chọn, reference circle — gợi ý `attribute`
- B#1: relevance=chưa chọn (không so với GT)
- R#1/B#2: frame đổi state reference 15; bạn 15
- R#1/B#2 pictogram, frame 0–29: bạn chưa chọn, reference circle — gợi ý `attribute`
- B#2: relevance=chưa chọn (không so với GT)

## Dòng gợi ý cho comparison_log.csv

```csv
task,sample,object,difference,error_type,who_is_right,action,note
traffic_light,dayClip5--01606.jpg,R#2/B#0,"R#2/B#0 pictogram, frame 0–29: bạn chưa chọn, reference arrow_left",attribute,,,
traffic_light,dayClip5--01606.jpg,R#0/B#1,"R#0/B#1 pictogram, frame 0–29: bạn chưa chọn, reference circle",attribute,,,
traffic_light,dayClip5--01606.jpg,R#1/B#2,"R#1/B#2 pictogram, frame 0–29: bạn chưa chọn, reference circle",attribute,,,
```

Hãy điền `who_is_right`, `action`, `note`; loại lỗi chỉ là gợi ý.
