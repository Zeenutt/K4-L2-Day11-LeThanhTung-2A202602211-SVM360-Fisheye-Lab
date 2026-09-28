# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 6 | 6 | 3 | 3 | 1 | 1 |
| mid | 8 | 8 | 0 | 0 | 0 | 0 |
| edge | 3 | 3 | 0 | 0 | 0 | 0 |

## Findings action=rework

Ba ca từng gắn `rework` đã đổi sang `keep_with_reason` trên `findings.csv` (R7+M6, R9, R5+M8). Lần máy so v2 với R vẫn ra **chưa sửa** — đúng vì không có box in-scope mới khớp R. Chạy lại `python3 lab11.py rework` sẽ để mục này trống; không tự đổi số bảng.

## Giới hạn phép so và thay đổi thật

Bảng trên do `python3 lab11.py rework` đếm L trước/sau so với teaching reference, **không** phải gold. Center matched 6→6, missing 3→3, spurious 1→1: **không cải thiện** và không bị sửa tay trên markdown.

Thay đổi XML thật: `r1_craft` 19 box → v2 20 box (`lock2` `DBD9-DB40`). Box mới là Truck trên `adasind_102750.jpg` (334.64,915.64)–(367.26,952.86), cao 37 px **< H=40** nên R01 loại khỏi `scoped` — không thành matched với R5. Không thêm R7 (Pedestrian 15×42) hay R9 (TW `R_only`). Quyết định giữ: trên ảnh không đọc được đúng class/vật; R có thể E0. Spurious 1 vẫn là L1 ThreeWheeler `102750` (E5, ticket). `mid`/`edge` không đổi vì không đụng nhãn in-scope ở đó.
