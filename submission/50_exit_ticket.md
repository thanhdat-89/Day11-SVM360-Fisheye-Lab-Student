# Exit ticket

Đọc `docs/10-svm360-reading-vi.md` trước khi trả lời câu 1–2. Các câu về zone, `why`, rework, parking và sampling
đã nằm trong file tương ứng nên không hỏi lại ở đây.

1. Một vật ở vùng seam giữa hai camera thật xuất hiện với hai box khác nhau: đó là lỗi `DUPLICATE` hay cần một quy
   tắc riêng? Vì sao? Hai box có thể hợp lệ vì mỗi camera ghi một observation riêng trong annotation space của nó. Chỉ gọi `DUPLICATE` sau khi policy đầu ra quy định phải hợp nhất và có timestamp đồng bộ, calibration/extrinsic cùng phép chiếu cho thấy chúng là một vật. Nếu chưa có các bằng chứng đó, giữ hai box kèm `camera_id` và đưa ca seam vào policy riêng.
2. Một vật đi qua nhiều frame trên cùng camera: khi nào giữ cùng track ID, khi nào thêm keyframe hoặc trạng thái
   Outside? Nêu bằng chứng sẽ cần trước khi nối track qua hai camera. Giữ cùng track ID khi identity còn liên tục qua thời gian và chuyển động/hình dạng phù hợp; thêm keyframe khi geometry hoặc attribute thay đổi đáng kể; đặt Outside khi vật rời trường nhìn hoặc không còn được quan sát theo guideline. Muốn nối qua hai camera cần timestamp đồng bộ, calibration/extrinsic, vùng seam/FOV, chuỗi chuyển động tương thích và policy identity/output; chỉ giống class hay gần vị trí ảnh là chưa đủ.
3. Nhìn lại cả buổi: một chỗ bạn tin nhãn mình đúng nhưng reference hoặc người soát nghĩ khác (dẫn frame/`object_ref`),
   bạn đã xử lý thế nào, và nếu làm lại slice này bạn sẽ đổi gì trong cách làm? Ở `adasind_265065.jpg L9`, tôi giữ box `Bike` vì ảnh cho thấy xe hai bánh đỗ sát lề và box cao hơn H, dù teaching reference không có. Tôi ghi `E0_reference_defect`, giữ nhãn có lý do và mở escalation cho QA thay vì sửa theo reference một cách máy móc. Nếu làm lại, tôi sẽ zoom và đo H cho toàn bộ vật nhỏ ngay trong self-QC, đồng thời ghi screenshot/object_ref trước khi khóa để phân xử nhanh hơn.
