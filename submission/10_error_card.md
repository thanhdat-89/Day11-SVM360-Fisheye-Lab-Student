# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B3 | WRONG_CLASS | 1 |
| center | B4 | MISSING | 1 |
| center | B4 | SPURIOUS | 8 |
| center | C0 | MISSING | 1 |
| center | C0 | SPURIOUS | 2 |
| edge | B3 | ATTRIBUTE | 1 |
| edge | B3 | IGNORE_SCOPE | 3 |
| edge | B4 | SPURIOUS | 1 |
| edge | C0 | WRONG_CLASS | 1 |
| mid | B4 | MISSING | 6 |
| mid | B4 | SPURIOUS | 11 |

## Top defects
- SPURIOUS: 22 (ví dụ frame adasind_019560.jpg)
- MISSING: 8 (ví dụ frame adasind_019560.jpg)
- IGNORE_SCOPE: 3 (ví dụ frame adasind_128310.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: `SPURIOUS` đứng đầu với 22 finding, nhưng phần lớn là box model (`E4_model_domain`) tách rider thành `Pedestrian`, nhầm `ThreeWheeler` thành `Car`/`Truck`, hoặc phát hiện trùng. Với nhãn L, ca nổi bật là `adasind_261480.jpg L4`: một box `Bike` nhỏ chồng trong `L6`, phù hợp `E1_annotator_error`. Một số box L-only ở `adasind_265065.jpg` lại có vật thật trên ảnh, nên không mặc định là lỗi annotator.
- Cách sửa và ai nhận việc (`owner`): annotator xóa box trùng, gộp rider + xe theo R03 và bổ sung pedestrian bị thiếu; kết quả rework đưa `mid` từ 2 missing/2 spurious xuống 0/0. `ai_team` cần audit lỗi tách rider và nhầm ThreeWheeler trên nhiều frame trước khi kết luận lệch miền. `qa` cần xác minh ca reference có thể thiếu `L9` trước khi cập nhật teaching reference.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `submission/screenshots/adasind_261480_rider_duplicate.jpg`, `submission/screenshots/adasind_265065_reference_audit.jpg`, các dòng `r1_craft`/`r3_diag` tương ứng trong `findings.csv`, R01/R03/R04 và `submission/rework/delta.md`.
