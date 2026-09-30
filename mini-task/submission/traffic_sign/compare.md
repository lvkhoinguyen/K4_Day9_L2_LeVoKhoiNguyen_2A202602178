# So sánh traffic_sign

> Các số dưới đây là số của công cụ so sánh, không phải ngưỡng chấm.

Box GTSDB (43 class Đức). GT không có readable, truncated, relevant_to_ego — các attribute này tự đối chiếu bằng decision log.

Trùng từng đỉnh với reference: 0/24 shape (<= 0,5 px).

## 00026.png

- R1/B1: IoU 0.845
- R1/B1: sign_family: bạn other, reference prohibitory — gợi ý `class`
- R1/B1: sign_class: bạn chưa chọn, reference 01 speed limit 30 — gợi ý `class`
- readable, truncated, relevant_to_ego: GT không có, không so — tự đối chiếu bằng decision log
- B2: box bạn vẽ không có trong reference — gợi ý `guideline_gap`

## 00054.png

- R3/B3: IoU 0.839
- R3/B3: sign_family: bạn mandatory, reference other — gợi ý `class`
- R3/B3: sign_class: bạn chưa chọn, reference 12 priority road — gợi ý `class`
- R2/B4: IoU 0.798
- R2/B4: sign_family: bạn mandatory, reference prohibitory — gợi ý `class`
- R2/B4: sign_class: bạn 08 speed limit 120, reference 00 speed limit 20 — gợi ý `class`
- R1/B1: IoU 0.786
- R1/B1: sign_family: bạn mandatory, reference danger — gợi ý `class`
- R1/B1: sign_class: bạn chưa chọn, reference 27 pedestrian crossing — gợi ý `class`
- readable, truncated, relevant_to_ego: GT không có, không so — tự đối chiếu bằng decision log
- R4: bạn thiếu biển có trong reference — gợi ý `missing`
- B2: box bạn vẽ không có trong reference — gợi ý `guideline_gap`

## 00073.png

- R4/B4: IoU 0.805
- R4/B4: sign_family: bạn mandatory, reference danger — gợi ý `class`
- R4/B4: sign_class: bạn chưa chọn, reference 23 slippery road — gợi ý `class`
- R2/B1: IoU 0.803
- R2/B1: sign_family: bạn mandatory, reference prohibitory — gợi ý `class`
- R6/B6: IoU 0.755
- R6/B6: sign_family: bạn mandatory, reference prohibitory — gợi ý `class`
- R6/B6: sign_class: bạn chưa chọn, reference 09 no overtaking — gợi ý `class`
- R3/B3: IoU 0.673
- R3/B3: sign_family: bạn mandatory, reference prohibitory — gợi ý `class`
- R3/B3: sign_class: bạn chưa chọn, reference 09 no overtaking — gợi ý `class`
- R5/B5: IoU 0.671
- R5/B5: sign_family: bạn mandatory, reference prohibitory — gợi ý `class`
- R5/B5: sign_class: bạn chưa chọn, reference 02 speed limit 50 — gợi ý `class`
- readable, truncated, relevant_to_ego: GT không có, không so — tự đối chiếu bằng decision log
- R1: bạn thiếu biển có trong reference — gợi ý `missing`
- B2: box bạn vẽ không có trong reference — gợi ý `guideline_gap`

## 00088.png

- R4/B1: IoU 0.858
- R4/B1: sign_family: bạn mandatory, reference prohibitory — gợi ý `class`
- R1/B2: IoU 0.849
- R1/B2: sign_family: bạn mandatory, reference prohibitory — gợi ý `class`
- R1/B2: sign_class: bạn chưa chọn, reference 10 no overtaking (trucks) — gợi ý `class`
- R2/B5: IoU 0.801
- R2/B5: sign_family: bạn chưa chọn, reference prohibitory — gợi ý `class`
- R2/B5: sign_class: bạn chưa chọn, reference 10 no overtaking (trucks) — gợi ý `class`
- R3/B4: IoU 0.770
- R3/B4: sign_family: bạn mandatory, reference prohibitory — gợi ý `class`
- readable, truncated, relevant_to_ego: GT không có, không so — tự đối chiếu bằng decision log
- B3: box bạn vẽ không có trong reference — gợi ý `guideline_gap`

## 00206.png

- R4/B3: IoU 0.853
- R4/B3: sign_family: bạn mandatory, reference other — gợi ý `class`
- R4/B3: sign_class: bạn chưa chọn, reference 13 give way — gợi ý `class`
- R5/B2: IoU 0.832
- R5/B2: sign_family: bạn mandatory, reference other — gợi ý `class`
- R5/B2: sign_class: bạn chưa chọn, reference 13 give way — gợi ý `class`
- R1/B1: IoU 0.754
- R1/B1: sign_class: bạn chưa chọn, reference 34 go left — gợi ý `class`
- R2/B4: IoU 0.695
- R2/B4: sign_class: bạn chưa chọn, reference 33 go right — gợi ý `class`
- readable, truncated, relevant_to_ego: GT không có, không so — tự đối chiếu bằng decision log
- R3: bạn thiếu biển có trong reference — gợi ý `missing`

## 00223.png

- R1/B1: IoU 0.672
- R1/B1: sign_family: bạn mandatory, reference prohibitory — gợi ý `class`
- R1/B1: sign_class: bạn chưa chọn, reference 01 speed limit 30 — gợi ý `class`
- readable, truncated, relevant_to_ego: GT không có, không so — tự đối chiếu bằng decision log
- B2: box bạn vẽ không có trong reference — gợi ý `guideline_gap`
- B3: box bạn vẽ không có trong reference — gợi ý `guideline_gap`

## Dòng gợi ý cho comparison_log.csv

```csv
task,sample,object,difference,error_type,who_is_right,action,note
traffic_sign,00026.png,R1/B1,"R1/B1: sign_family: bạn other, reference prohibitory",class,,,
traffic_sign,00026.png,R1/B1,"R1/B1: sign_class: bạn chưa chọn, reference 01 speed limit 30",class,,,
traffic_sign,00026.png,B2,B2: box bạn vẽ không có trong reference,guideline_gap,,,
traffic_sign,00054.png,R3/B3,"R3/B3: sign_family: bạn mandatory, reference other",class,,,
traffic_sign,00054.png,R3/B3,"R3/B3: sign_class: bạn chưa chọn, reference 12 priority road",class,,,
traffic_sign,00054.png,R2/B4,"R2/B4: sign_family: bạn mandatory, reference prohibitory",class,,,
traffic_sign,00054.png,R2/B4,"R2/B4: sign_class: bạn 08 speed limit 120, reference 00 speed limit 20",class,,,
traffic_sign,00054.png,R1/B1,"R1/B1: sign_family: bạn mandatory, reference danger",class,,,
traffic_sign,00054.png,R1/B1,"R1/B1: sign_class: bạn chưa chọn, reference 27 pedestrian crossing",class,,,
traffic_sign,00054.png,R4,R4: bạn thiếu biển có trong reference,missing,,,
traffic_sign,00054.png,B2,B2: box bạn vẽ không có trong reference,guideline_gap,,,
traffic_sign,00073.png,R4/B4,"R4/B4: sign_family: bạn mandatory, reference danger",class,,,
traffic_sign,00073.png,R4/B4,"R4/B4: sign_class: bạn chưa chọn, reference 23 slippery road",class,,,
traffic_sign,00073.png,R2/B1,"R2/B1: sign_family: bạn mandatory, reference prohibitory",class,,,
traffic_sign,00073.png,R6/B6,"R6/B6: sign_family: bạn mandatory, reference prohibitory",class,,,
traffic_sign,00073.png,R6/B6,"R6/B6: sign_class: bạn chưa chọn, reference 09 no overtaking",class,,,
traffic_sign,00073.png,R3/B3,"R3/B3: sign_family: bạn mandatory, reference prohibitory",class,,,
traffic_sign,00073.png,R3/B3,"R3/B3: sign_class: bạn chưa chọn, reference 09 no overtaking",class,,,
traffic_sign,00073.png,R5/B5,"R5/B5: sign_family: bạn mandatory, reference prohibitory",class,,,
traffic_sign,00073.png,R5/B5,"R5/B5: sign_class: bạn chưa chọn, reference 02 speed limit 50",class,,,
traffic_sign,00073.png,R1,R1: bạn thiếu biển có trong reference,missing,,,
traffic_sign,00073.png,B2,B2: box bạn vẽ không có trong reference,guideline_gap,,,
traffic_sign,00088.png,R4/B1,"R4/B1: sign_family: bạn mandatory, reference prohibitory",class,,,
traffic_sign,00088.png,R1/B2,"R1/B2: sign_family: bạn mandatory, reference prohibitory",class,,,
traffic_sign,00088.png,R1/B2,"R1/B2: sign_class: bạn chưa chọn, reference 10 no overtaking (trucks)",class,,,
traffic_sign,00088.png,R2/B5,"R2/B5: sign_family: bạn chưa chọn, reference prohibitory",class,,,
traffic_sign,00088.png,R2/B5,"R2/B5: sign_class: bạn chưa chọn, reference 10 no overtaking (trucks)",class,,,
traffic_sign,00088.png,R3/B4,"R3/B4: sign_family: bạn mandatory, reference prohibitory",class,,,
traffic_sign,00088.png,B3,B3: box bạn vẽ không có trong reference,guideline_gap,,,
traffic_sign,00206.png,R4/B3,"R4/B3: sign_family: bạn mandatory, reference other",class,,,
traffic_sign,00206.png,R4/B3,"R4/B3: sign_class: bạn chưa chọn, reference 13 give way",class,,,
traffic_sign,00206.png,R5/B2,"R5/B2: sign_family: bạn mandatory, reference other",class,,,
traffic_sign,00206.png,R5/B2,"R5/B2: sign_class: bạn chưa chọn, reference 13 give way",class,,,
traffic_sign,00206.png,R1/B1,"R1/B1: sign_class: bạn chưa chọn, reference 34 go left",class,,,
traffic_sign,00206.png,R2/B4,"R2/B4: sign_class: bạn chưa chọn, reference 33 go right",class,,,
traffic_sign,00206.png,R3,R3: bạn thiếu biển có trong reference,missing,,,
traffic_sign,00223.png,R1/B1,"R1/B1: sign_family: bạn mandatory, reference prohibitory",class,,,
traffic_sign,00223.png,R1/B1,"R1/B1: sign_class: bạn chưa chọn, reference 01 speed limit 30",class,,,
traffic_sign,00223.png,B2,B2: box bạn vẽ không có trong reference,guideline_gap,,,
traffic_sign,00223.png,B3,B3: box bạn vẽ không có trong reference,guideline_gap,,,
```

Hãy điền `who_is_right`, `action`, `note`; loại lỗi chỉ là gợi ý.
