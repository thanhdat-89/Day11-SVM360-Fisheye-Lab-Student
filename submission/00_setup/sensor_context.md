
# Sensor context

- **Rig:** Theo quan sát, camera fisheye hướng về phía trước và có vẻ được gắn hoặc mang trên một phương tiện hai bánh đang di chuyển. Một số frame cho thấy tay người lái và một phần phương tiện ở mép trái/phía dưới; dataset không cung cấp đủ thông tin để xác định chính xác vị trí và độ cao lắp camera.
- **`ego_body`:** Phần của phương tiện gắn camera, tay người lái hoặc tay lái xuất hiện chủ yếu dọc mép trái và vùng phía dưới frame. Chỉ vẽ `ego_body` tại frame thực sự nhìn thấy các phần này.
- **Vòng kính:** Vùng ảnh fisheye nằm gần giữa frame, trải gần hết chiều ngang và khoảng 80–85% chiều cao. Vành đen nằm bên ngoài vòng kính, rõ nhất ở phía trên, phía dưới và các góc ảnh.