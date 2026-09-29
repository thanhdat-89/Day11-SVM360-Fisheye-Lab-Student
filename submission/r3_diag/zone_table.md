# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 4 | 0 | 2 | 1 | 4 | SPURIOUS (2) |
| mid | 13 | 2 | 2 | 3 | 7 | SPURIOUS (2) |
| edge | 0 | 0 | 0 | 0 | 1 | — |

## Nhận xét

- `mid` là zone gãy nhiều nhất cho cả người và model: L có 2 missing + 2 spurious; M có 3 missing + 7 box thừa. `center` của L không missing nhưng có 2 spurious, còn M có 1 missing + 4 box thừa. `edge` không có reference nên không thể kết luận chất lượng, dù model có 1 box thừa.
- Trên ảnh, nhiều lỗi M đến từ việc tách người lái thành `Pedestrian` bên trong một `Bike`, nhầm `ThreeWheeler` thành `Car`/`Truck`, hoặc tạo nhiều box cho cùng vật. Với L, lỗi chính tập trung ở rider/box trùng và vật nhỏ sát ngưỡng H. IoU sweep ổn định từ 0.3 đến 0.5 nhưng tại 0.7, L ở `mid` giảm từ 11 xuống 9 matched và M giảm từ 10 xuống 8; điều này cho thấy một phần khác biệt do geometry chưa đủ chặt. Tuy nhiên slice chỉ có ba frame, không có reference ở `edge`, nên chưa đủ bằng chứng quy lỗi cho méo fisheye hay khái quát sang bốn camera SVM.
