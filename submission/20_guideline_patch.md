# Guideline patch

- **Rule mới đề xuất:** R12 — Với người và xe hai bánh chồng/tiếp xúc: gán một `Bike` nếu tư thế, vị trí tay/chân và quan hệ hình học cho thấy người đang ngồi hoặc điều khiển xe. Chỉ tách `Pedestrian` + `Bike` khi thấy bằng chứng người đứng ngoài và đang dắt xe. Nếu vật quá nhỏ hoặc bị che khiến không phân xử được, ghi `E5_unresolved` và đưa QA; không đồng thời tạo một `Bike` bao toàn bộ và một box người bên trong.
- **Áp dụng cho:** `Bike`, `Pedestrian`, rider ở `mid`/`edge`, đặc biệt ca nhỏ hoặc occluded; mở rộng cách thực thi R03.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R03 nêu kết quả cho rider và người dắt xe nhưng chưa nêu dấu hiệu quan sát hay cách xử lý ca nhỏ/mờ. Điều này dẫn đến `adasind_261480.jpg L4` bị box trùng và `adasind_265065.jpg L6/R5` bị tách rider sai.
- **`rules_version` mới:** v1.1.0.
- **Hiệu lực từ:** vòng annotation kế tiếp sau khi QA/Lab Coach phê duyệt; không hồi tố để thay đổi bản đã khóa ngoài quy trình rework.
