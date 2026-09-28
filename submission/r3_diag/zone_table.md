# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 9 | 3 | 1 | 5 | 8 | MISSING (3) |
| mid | 8 | 0 | 0 | 4 | 10 | — |
| edge | 3 | 0 | 0 | 2 | 0 | — |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: L lệch R chủ yếu ở **center** (missing 3, spurious 1); `mid`/`edge` L missing=spurious=0. M gãy rộng hơn: missing (`LR_noM`+`R_only`) 5/4/2 theo center/mid/edge, thừa (`LM_noR`+`M_only`) **8 center + 10 mid**. Cột “lỗi L chính” MISSING (3) trùng ba ca R7/R9/R5 — không cộng các dòng `LR_noM` (đó là model thiếu).
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: M thừa ở center/mid khớp fisheye + R03/R04 (tách rider, TW→Car/Truck, M5 `102750` box gần full frame). L missing 3 ở center là tranh chấp “vệt xa / R sửa tay”, không chứng minh vật gần xe (zone không phải khoảng cách). `ego_body` sai (L6, polygon dưới gán ego) làm đục don't-care nhưng không giải thích 8+10 box M. Giới hạn: 3 frame một camera, R không phải gold, không suy bốn camera SVM.
