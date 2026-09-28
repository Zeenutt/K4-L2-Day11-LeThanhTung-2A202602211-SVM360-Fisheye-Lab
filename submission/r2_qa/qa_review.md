# QA review · B2-dense

Mã khóa: 6C19-E975

Soát mù trên `qa_overlay.html` + ảnh gốc + `docs/02-rules-vi.md`. Chưa mở teaching reference / model / worked. `why` để trống trên findings.

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_062370.jpg | L8 | R03 | Pedestrian (396,743)–(472,845) chồng L3 Bike trên xe máy giữa đường. Người đội mũ bảo hiểm đang ngồi trên xe → R03 một box Bike; không tách Pedestrian. |
| adasind_062370.jpg | L7 | R07 | Bike (0,1028)–(188,1640) ôm tay/ghi-đông/giày ego góc dưới-trái. Thân xe gắn camera phải là ignore `ego_body` (R07) không phải class động. L11 Pedestrian chồng cùng vùng. |
| adasind_062370.jpg | ignore_region | R08 | XML chỉ có 1 polygon `lens_border` (vành trên). R08 cần 2 polygon vành đen/frame; vành dưới không thấy hoặc đã gộp vào ego. |
| adasind_069450.jpg | L3 | R04 | Box `Car` (236,860)–(314,958) khớp xe ba bánh tối phía sau xe vàng L4. R04: auto-rickshaw = ThreeWheeler không phải Car. |
| adasind_069450.jpg | L2 | R04 | Box `Bike` (783,788)–(887,904) khớp xe đẩy/ba bánh xanh bên phải. R04: ThreeWheeler không phải Bike. |
| adasind_069450.jpg | L1 | R07 | Pedestrian (0,1083)–(234,1644) và L8 Bike chồng tay/ghi-đông/ống quần ego. R07: vẽ `ego_body` ôm phần nhìn thấy; không box ego thành Pedestrian/Bike. Polygon `reason=ego_body` ở đỉnh khung (y≈438) là vành kính không phải thân xe (R06/R08). |
| adasind_117120.jpg | L2 | R04 | Box `Bus` (421,891)–(462,942) cao 50 px: xe trắng nhỏ phía trước SUV. Không thấy minibus/xe buýt. R04: van/xe con = Car; Bus chỉ minibus/xe buýt. |
| adasind_117120.jpg | L6 | R07 | Bike (0,1042)–(326,1750) và L7 Pedestrian ôm tay áo kẻ/ghi-đông ego. Cùng R07 như hai frame kia. XML có 1 `lens_border` (trên) — thiếu polygon vành dưới (R08). |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
