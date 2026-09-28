# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B2 | ATTRIBUTE | 1 |
| center | B2 | MISSING | 10 |
| center | B2 | SPURIOUS | 11 |
| center | B2 | WRONG_CLASS | 1 |
| center | C0 | SPURIOUS | 1 |
| edge | B2 | IGNORE_SCOPE | 1 |
| edge | B2 | MISSING | 1 |
| edge | B2 | SPURIOUS | 3 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B2 | MISSING | 5 |
| mid | B2 | SPURIOUS | 10 |
| mid | B2 | WRONG_CLASS | 2 |
| unknown | C0 | STRUCTURE | 1 |

## Top defects
- SPURIOUS: 25 (ví dụ frame adasind_019560.jpg)
- MISSING: 16 (ví dụ frame adasind_060000.jpg)
- WRONG_CLASS: 4 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: Số **SPURIOUS 25** / **MISSING 16** phần lớn không phải “vẽ thừa / thiếu 25–16 box trên nhãn L”. Trên B2, `center` SPURIOUS 11 và MISSING 10 cộng `mid` SPURIOUS 10 chủ yếu là ô `M_only` và `LR_noM` (model YOLO26m trên fisheye: tách rider khỏi Bike, gọi ThreeWheeler thành Car/Truck, box phủ gần hết frame). `why=E4_model_domain` vì cùng pattern trên cả ba frame 060000 / 086220 / 102750, không gán E4 từ một box. Phần L thật sự lệch R nằm ở `center`: R7+M6 Pedestrian, R9 ThreeWheeler, R5+M8 Truck (`MISSING`), L1 ThreeWheeler `102750` (`SPURIOUS`, E5), và L6 Pedestrian `060000` `IGNORE_SCOPE` (ôm ego). Tôi **không** coi teaching reference là gold: ba box R kia trên ảnh không đọc được class rõ nên giữ nhãn L (`keep_with_reason` / E0 khi chốt P5). `WRONG_CLASS` C0 L7+R3 (Car vs ThreeWheeler mép trái) và QA B2-dense L2/L3 `069450` (Car/Bike vs TW) là lỗ hổng R04, không phải zone “xa”.
- Cách sửa và ai nhận việc (`owner`): `ai_team` — không nhét box model vào L; pre-label fisheye cần lọc ignore và gộp rider (R03). `annotator` — không box tay/ghi-đông ego thành Pedestrian/Bike (R07), như L6 `060000` và các ca QA L7 `062370`, L1 `069450`, L6 `117120`. `data_ops` / `qa` — không bắt copy R7/R9/R5; chấm độc lập trên ảnh. `guideline` — bổ sung luật “H≥40 chưa đủ nếu không đọc được class” (`20_guideline_patch.md`). Ca L1 `102750` TW vs Truck để `escalate` (ticket).
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `submission/screenshots/p6_060000.jpg` + `r1_craft/compare.html` (R7 15×42 px, R9 sát đuôi TW lớn, L6 ego); `submission/screenshots/p6_102750.jpg` + findings R5+M8 / L1; `r3_diag/zone_table.md` (L missing 3 và spurious 1 ở center; M thừa 8+10 ở center/mid); `local_quality.md` TP=17 FP=1 FN=3 trên R chứ không phải trên gold; `qa_review.md` R03/R04/R07; rule R01 R03 R04 R07 R09.
