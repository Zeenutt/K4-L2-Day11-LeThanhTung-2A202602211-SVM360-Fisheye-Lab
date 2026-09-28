# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `9e53d70c94ccd790148081852324a6197cfa502ae9e76bde01c12feae215e668`; slice `B2-mid`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_060000.jpg, adasind_086220.jpg, adasind_102750.jpg. Frame thiếu trong export: không.
TP=17; FP=1; FN=3; số lần đối chiếu=21; mean IoU của TP=0.873.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.810 | 0.952 | 0.905 |
| precision | 0.944 | 0.972 | 0.889 |
| recall | 0.850 | 0.826 | 0.667 |
| jaccard | 0.810 | 0.804 | 0.667 |
| dice | 0.895 | 0.887 | 0.800 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 4 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| Pedestrian | 3 | 0 | 1 | 0.952 | 1.000 | 0.750 | 0.750 | 0.857 |
| ThreeWheeler | 8 | 1 | 1 | 0.905 | 0.889 | 0.889 | 0.800 | 0.889 |
| Truck | 2 | 0 | 1 | 0.952 | 1.000 | 0.667 | 0.667 | 0.800 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_060000.jpg | 8 | 0 | 2 | 0.800 | 1.000 | 0.800 |
| adasind_086220.jpg | 5 | 0 | 0 | 1.000 | 1.000 | 1.000 |
| adasind_102750.jpg | 4 | 1 | 1 | 0.667 | 0.800 | 0.800 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|
| Bike | 4 | 0 | 0 | 0 | 0 |
| Pedestrian | 0 | 3 | 0 | 0 | 1 |
| ThreeWheeler | 0 | 0 | 8 | 0 | 1 |
| Truck | 0 | 0 | 0 | 2 | 1 |
| <extra> | 0 | 0 | 1 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
