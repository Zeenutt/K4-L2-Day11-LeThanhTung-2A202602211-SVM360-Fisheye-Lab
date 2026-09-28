# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| B2-mid / `adasind_060000.jpg` | L vs R: 2 `MISSING` (R7 Pedestrian, R9 TW), 1 `IGNORE_SCOPE` (L6 ego), 1 `ATTRIBUTE` (L5 truncated). Zone table: **center** L missing 3 + spurious 1 — hầu hết dồn frame này. Model: nhiều `M_only` tách Bike/TW. | Frame đông nhất, ego thấy rõ, TW lớn + xe máy: cùng lúc R03/R04/R07 và tranh chấp “vệt ≥H có bắt box không”. Review trước để chốt ego_body vs lens_border và không box tay áo kẻ. | Ảnh gốc; `r1_craft/compare.html`; XML ignore `reason`; `screenshots/p6_060000.jpg`; findings R7+M6, R9, L6; selfqc L6. Không dùng teaching reference làm đáp án. |
| B2-dense (QA) / `adasind_069450.jpg` (+ đối chiếu `062370`, `117120`) | QA `L_only`: 2 `WRONG_CLASS` R04 (L3 Car→TW, L2 Bike→TW), 1 `SPURIOUS` R07 (L1/L8 ôm ego). Cùng slice QA còn R03 rider `062370` L8 và thiếu `lens_border` dưới (R08). | Lát cắt **người khác**, mật độ cao hơn B2-mid: kiểm xem lỗi ego + nhầm TW có lặp ngoài slice của mình trước khi kết luận guideline. Không phải camera thứ hai — vẫn một fisheye ADASIND. | `r2_qa/qa_overlay.html` mã `6C19-E975`; `qa_review.md`; findings r2_qa why trống; ảnh `adasind_069450.jpg`. Không mở R/M khi đọc lại QA. |

Giới hạn của kết luận từ ba frame ADASIND: B2-mid chỉ 060000 / 086220 / 102750, một camera, không track, không seam, không `parking_line` trên fisheye. `086220` L khớp R (compare.md không có MISSING/SPURIOUS in-scope) nên không đại diện “slice sạch”. FN/FP local-quality (3 và 1) so với R sửa tay, không phải tỷ lệ lỗi bốn camera. Zone `center` trên 060000 không có nghĩa vật gần xe.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: Mỗi `camera_id` có bình `normal` và oversample `hard` (126/200) để **bắt loại** glare, ego_body, vạch ô vs lối chạy, seam — giống lỗi đã thấy trên ADASIND chứ không nhân 3 frame thành 50k. Soát độ phủ: checklist hard-case theo camera (bảng `46_gold_set_plan.md`), không lấy chuỗi timestamp liền kề. 18–32 frame/tế bào không cho khoảng tin cậy; không có mẫu số 50k trong repo. Muốn tỷ lệ lỗi cần sample ngẫu nhiên theo camera sau khi guideline (kể cả R12) đóng băng — đó là vòng khác, không phải ngân sách 200 frame tìm lỗi này.
