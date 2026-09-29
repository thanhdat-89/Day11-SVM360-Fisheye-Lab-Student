# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn                           | Vì sao dễ sai                                                                   | Annotation space / calibration cần giữ                                                                                          | Cách review trước khi gọi là gold                                                                                  |
| --------- | ---------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| front     | Giao thông đông, rider và vật bị che     | Dễ thiếu vật, sai class hoặc vẽ một box cho nhiều vật                     | giữ ảnh fisheye gốc, đúng`camera_id`, timestamp và phiên bản calibration; không trộn box ảnh gốc với box trên BEV | ít nhất hai người review độc lập; bất đồng được đối chiếu với guideline và người phân xử thứ ba. |
| rear      | Vật nhỏ ở rìa, ánh sáng yếu khi lùi    | Dễ bỏ sót và đặt box sai hình học                                         | giữ ảnh fisheye gốc, đúng`camera_id`, timestamp và phiên bản calibration; không trộn box ảnh gốc với box trên BEV | ít nhất hai người review độc lập; bất đồng được đối chiếu với guideline và người phân xử thứ ba. |
| left      | Xe máy/người đi bộ sát xe và vùng seam | Méo fisheye mạnh, có thể xuất hiện đồng thời ở camera trước hoặc sau | giữ ảnh fisheye gốc, đúng`camera_id`, timestamp và phiên bản calibration; không trộn box ảnh gốc với box trên BEV | ít nhất hai người review độc lập; bất đồng được đối chiếu với guideline và người phân xử thứ ba. |
| right     | Vật sát lề, che khuất và vùng seam       | Khó phân biệt box hợp lệ trên hai camera với lỗi trùng                   | giữ ảnh fisheye gốc, đúng`camera_id`, timestamp và phiên bản calibration; không trộn box ảnh gốc với box trên BEV | ít nhất hai người review độc lập; bất đồng được đối chiếu với guideline và người phân xử thứ ba. |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule):khi đổi camera, vị trí/góc lắp, calibration, taxonomy hoặc phiên bản guideline.
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box:chưa tự ghép hai box chỉ vì chúng có vẻ là cùng một vật; cần timestamp đồng bộ, calibration và policy đầu ra
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera:agreement hoặc quality report trên một camera chỉ đo độ nhất quán của tập đó, không chứng minh đúng cho cả bốn camera
