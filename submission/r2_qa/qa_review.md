# QA review · B3-mid

Mã khóa: CB95-EEB9

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_128310.jpg | L1 | R04 | Vật thể màu đỏ ở vùng giữa ảnh có hình dạng xe ba bánh/auto-rickshaw nhưng box được gán `Car`; cần đổi hoặc xác minh lại class `ThreeWheeler`. |
| adasind_128310.jpg | L5 | R07;R09 | Box `Pedestrian` rất lớn ở góc dưới-trái bao phần người/phương tiện thuộc ego rig, trong khi frame đã có polygon `ego_body`; box này nằm sai phạm vi object cần gán. |
| adasind_140160.jpg | L3 | R05 | Box `Bike` chạm và bị cắt bởi biên phải của ảnh nhưng attribute đang là `truncated=false`; cần đặt `truncated=true`. |
| adasind_140160.jpg | L4 | R07;R09 | Box `Pedestrian` ở góc dưới-trái bao bàn chân/phần ego đã được phủ bởi `ignore_region` có `reason=ego_body`; không nên giữ box object trong vùng này. |
| adasind_230910.jpg | L13 | R07;R09 | Box `Pedestrian` lớn ở góc dưới-trái bao người điều khiển/phần ego rig và chồng vùng `ego_body`; đây không phải pedestrian độc lập trong cảnh. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
