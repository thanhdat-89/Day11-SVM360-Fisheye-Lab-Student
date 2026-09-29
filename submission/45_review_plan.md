# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `B4-mid / adasind_265065.jpg` | Local quality: 3 FP, 2 FN; gồm rider bị tách, pedestrian thiếu và 2 ca nghi reference thiếu | Accuracy frame thấp nhất (0.545), đồng thời có cả lỗi annotator và bất đồng với reference nên ảnh hưởng trực tiếp `Bike`/`Pedestrian` | Ảnh gốc, `compare.html`, `model_compare.html`, crop `adasind_265065_reference_audit.jpg`, finding L4/L6/L9/R5/R7 và delta trước/sau |
| `B4-mid / adasind_261480.jpg` | Local quality: 1 FP; model có nhiều miss/extra quanh Bike và ThreeWheeler | Cụm vật sát nhau làm lộ lỗi box trùng/rider và model nhầm ThreeWheeler; đây là pattern cần kiểm trên nhiều frame hơn | Ảnh gốc, crop `adasind_261480_rider_duplicate.jpg`, finding L4 cùng các M-only/LR-noM và rule R03/R04 |

Giới hạn của kết luận từ ba frame ADASIND: đây chỉ là một camera, một slice ba frame và không có reference object ở zone `edge`. Các tỷ lệ không đại diện toàn dataset, không chứng minh nguyên nhân model-domain và không thể suy sang front/rear/left/right của hệ SVM thật.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: lập bảng theo `camera_id × normal/hard`, scene/route, block thời gian, ánh sáng và seam; khử gần-trùng bằng scene ID/timestamp rồi giới hạn số frame liên tiếp từ cùng clip. Soát đủ 8 ô và giữ danh sách frame bị loại/thay thế. Đây là mẫu có chủ đích theo rủi ro chứ không phải mẫu ngẫu nhiên xác suất, nên chỉ giúp tìm ca khó và kiểm rule; không dùng nó để ước lượng tỷ lệ lỗi của toàn bộ 50.000 frame.
