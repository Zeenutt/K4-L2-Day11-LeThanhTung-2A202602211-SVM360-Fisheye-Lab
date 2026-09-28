# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_060000.jpg
- L6 edge IGNORE_SCOPE
- L5+R1 center ATTRIBUTE
- R7 center MISSING
- R9 center MISSING
## adasind_086220.jpg
## adasind_102750.jpg
- L1 center SPURIOUS
- R5 center MISSING

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 9 | 6 | 3 | 1 |
| mid | 8 | 8 | 0 | 0 |
| edge | 3 | 3 | 0 | 0 |
