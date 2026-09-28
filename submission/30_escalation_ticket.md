# Escalation ticket

## Ticket 1

- **Frame:** `adasind_102750.jpg` (slice B2-mid) — `object_ref` L1 (`L_only` ThreeWheeler ~ (422,936) cao 47 px) và R5+M8 (`RM_noL` Truck ~ (333,903)–(366,953)). Cùng nhóm xe xa giữa làn, không phải ego.
- **Ảnh chụp:** `submission/screenshots/p6_102750.jpg` (ảnh gốc); đối chiếu box: `submission/r1_craft/compare.html`, `submission/r3_diag/model_compare.html`.
- **Expected impact:** `local_quality.md` đang đếm FP=1 (L1 vs R) và FN=1 Truck (R5) trên frame này. Nếu bắt copy R: thêm Truck có thể tăng matched vs R nhưng gán sai class (R04). Nếu xóa L1: mất một xe xa mà M cũng thấy (M6 Truck cùng chỗ). Teaching reference sửa tay; ba frame không đủ để chọn TW vs Truck. Ảnh hưởng review gold giả lập bốn camera: cùng kiểu “vệt xa” sẽ xuất hiện trên mọi `camera_id`.
- **Owner:** `qa` (adjudicator độc lập với annotator B2-mid); `guideline` nhận nếu cần chốt R12; không giao `ai_team` vì đây không phải sửa trọng số model.
- **Recommendation:** Không lấy R làm đáp án. Hai reviewer độc lập soi ảnh gốc, ghi class hoặc “không box / unreadable”. Quyết định ghi vào `40_decision_log.csv`. Cho đến khi có adjudicator: giữ L1, không thêm R5 in-scope (v2 có box Truck cao 37 px < H nên R01 đã loại khỏi phép so). Không undistort để “nhìn rõ hơn”.
