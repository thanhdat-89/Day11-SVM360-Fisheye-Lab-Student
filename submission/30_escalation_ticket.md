# Escalation ticket

## Ticket 1

- **Frame:** `adasind_265065.jpg`, object `L9` (`Bike`, vùng mid, cao khoảng 43 px).
- **Ảnh chụp:** `submission/screenshots/adasind_265065_reference_audit.jpg`.
- **Expected impact:** Nếu teaching reference thiếu một `Bike` hợp lệ trên ngưỡng H, box của learner bị tính FP và precision/Jaccard của class `Bike` cùng thống kê zone `mid` bị lệch. Nếu vật thực ra không đủ điều kiện, việc không ghi lý do loại cũng khiến annotator khó tái lập quyết định.
- **Owner:** `qa`.
- **Recommendation:** Hai reviewer độc lập mở ảnh gốc, đo chiều cao và xác nhận đây có phải xe hai bánh nhìn thấy được hay không. Nếu hợp lệ, bổ sung box vào teaching reference và tăng version; nếu không hợp lệ, ghi exclusion reason/known issue để các vòng sau áp dụng nhất quán.
