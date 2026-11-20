# Báo cáo cá nhân — Ngày 11
Họ tên: Nguyễn Thị Hồng Hạnh              Mã học viên: 2A202603272  
Phiên bản CVAT (Help → About): CVAT v2.82.0  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 2  
Thời điểm export (ngày giờ trên CVAT): 2026-11-20 18:24:37 UTC    Số lần nộp lại sau Rework: 1  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | Gồm lane (polyline), road_curb (polyline), crosswalk (polygon), drivable (polygon), traffic_light (rectangle), traffic_sign (rectangle). |
| Thuộc tính và giá trị | Đúng | Đầy đủ: lane (position, style, color, kind), drivable (area_type), traffic_light (color, type, facing, edge_zone), traffic_sign (group, facing, edge_zone). |
| 4 tag ảnh | Đúng | Đầy đủ 4 tag: camera, timeofday, weather, source; mỗi tag có một thuộc tính select tên `value`. |
Cách kết thúc polyline trên bản CVAT này: Bấm phím **N** trên bàn phím (hoặc click chuột đúp vào điểm cuối) để kết thúc vẽ polyline.  
Cách đặt tag ảnh trên bản CVAT này: Chọn công cụ **Tag** ở thanh công cụ bên trái, chọn label tag tương ứng (camera, timeofday, weather, source), bấm để gắn vào ảnh, sau đó vào bảng **Objects → Details** để chọn giá trị select `value` cho đúng với ảnh.  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 34 | 17 | 4 | 23 | 48 | 32 |
| front-extra (đã làm 4 / 4) | 4 | 12 | 5 | 5 | 7 | 9 | 14 |
| fisheye | 8 | 5 | 10 | 10 | 0 | 6 | 8 |
| fisheye-extra (đã làm 4 / 4) | 4 | 2 | 6 | 5 | 0 | 0 | 1 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05_b2576c8c-2de20b8a.jpg | lane | Vẽ vạch giả định hay bỏ qua L1/R1 | Không vẽ lane (chỉ gán drivable và road_curb) | Mặt đường không có vạch sơn phân làn, bên mép đường chỉ có bờ hè/rào chắn. Theo quy tắc 6 của guideline: "Không vẽ vạch mà ảnh không có". |
| A06_b8c66e31-37045eec.jpg | lane (R1) | Vẽ R1 hay chỉ vẽ L1 | Không vẽ R1 (chỉ có L1 và L2) | Phía bên phải xe là giao lộ mở rộng, vạch sơn bên phải hoàn toàn không tồn tại trên mặt đường. |
| A09_c7e6d5d1-c8af9fe3.jpg | lane (R1) | Vẽ R1 sát mép hay gán road_curb | Gán road_curb, không gán R1 | Mép phải đường là vỉa hè bê tông trực tiếp, không có vạch sơn kẻ đường nào ở vị trí R1. |
| A12_c0f978fa-9b4e623f.jpg | lane (L1) | Vẽ L1 hay bỏ qua | Không vẽ L1 | Vùng bên trái bị khuất bởi hàng xe đỗ sát và tim đường bị xoá mờ trong nút giao lộ. |
| B03_04267_RV.png | traffic_sign | Bật edge_zone hay tắt | Tắt edge_zone cho các biển ở trung tâm | Biển nằm ở vùng hiển thị rõ ràng, tâm bounding box nằm trong 80% bán kính ảnh fisheye. |
| B07_01216_MVR.png | crosswalk | Gán crosswalk hay gán lane position=other | Gán crosswalk (polygon) | Vạch kẻ trên ảnh camera sườn xe MVR là vạch ngựa vằn qua đường; theo mục 4 guideline: vạch ngựa vằn gán crosswalk, không gán lane. |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: trangtnh    Quyết định nhận được: Rework (hoặc Hold để giải trình QC1-02)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-02 đủ L1, R1 | 4 | Không đồng ý (đề xuất miễn trừ) | Đã đối chiếu CHECKPOINTS.md: ảnh A05, A06, A09, A12 thật sự không thấy vạch sơn trên đường. Không vẽ vạch bịa, ghi giải trình vào mục 3. |
| QC1-05 vạch đứt, che | 5 | Đồng ý | Đã rà soát lại các vạch đứt ở A04, A08, A09, A11; nguyên nhân do khi gán click tách thành nhiều polyline thay vì giữ 1 polyline liền từ gần ra xa. |
| QC1-11 fisheye | 6 | Đồng ý | Ghi nhận lỗi đặt ít điểm trên polyline cong ở B01, B03, B04, B06; cần bổ sung các điểm nút uốn theo cung tròn của thấu kính fisheye. |
| QC1-12 file | 1 | Đồng ý | B07 có điểm click đúp lặp toạ độ ở polygon crosswalk; đã kiểm tra và lưu ý thao tác click chuột. |

*Ghi chú lần nộp Revision 2:* Đã sao lưu bản Revision 1 vào thư mục `r1/`. Bản nộp Revision 2 gộp toàn bộ 4 ảnh front-extra (A13–A16) và 4 ảnh fisheye-extra (B09–B12) vào 2 file zip chính quy chuẩn (`nguyenthihonghanh-front.zip`: 16 ảnh, `nguyenthihonghanh-fisheye.zip`: 12 ảnh) để lấy tối đa +4 điểm thưởng theo Rubric.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| nguyenthihonghanh-front.zip | Có (mở tốt, đủ 16 ảnh) | 9 / 9 (A01) | 6 / 6 (A02) | Có (`camera = front`) |
| nguyenthihonghanh-fisheye.zip | Có (mở tốt, đủ 12 ảnh) | 8 / 8 (B01) | 5 / 5 (B02) | Có (`camera = fisheye_front`) |

## 6. Ảnh chụp màn hình
1. Tab Labels của project: Đã kiểm tra trực tiếp trên CVAT, hiển thị đủ 6 shape labels và 4 image tags (camera, timeofday, weather, source) đúng cấu hình taxonomy.
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển): Ảnh A01 và A04 đã gán đủ drivable (direct, alternative), các lane L1/R1 từ đáy ảnh ra xa, bounding box đèn và biển sát mép.
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong: Ảnh B01 uốn cong theo độ méo của thấu kính fisheye WoodScape, các điểm nút bám sát vệt sơn.
4. Một đoạn XML có <polyline label="lane">: Đoạn trích từ file `annotations.xml` của task front:
```xml
<polyline label="lane" occluded="0" points="699.20,715.40;652.60,680.00;600.40,640.00;544.60,600.00;486.60,560.00" z_order="0">
  <attribute name="position">R1</attribute>
  <attribute name="style">solid</attribute>
  <attribute name="color">white</attribute>
  <attribute name="kind">single</attribute>
</polyline>
```

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
- Lỗi mắc nhiều nhất: **QC1-05 (vạch đứt bị tách polyline)** và **QC1-11 (polyline fisheye chưa đủ dày điểm theo cung)**.
- Cách tránh ở Ngày 20: Khi gặp vạch đứt (dashed lane), tuân thủ nguyên tắc "một vạch đứt là một polyline duy nhất" xuyên suốt từ điểm gần xe nhất đến điểm xa nhất thấy được, không ngắt quãng từng vệt sơn. Với ảnh fisheye, luôn zoom gần và đặt các điểm nút dày đặc ở vùng biên ngoài nơi ảnh có độ biến dạng góc rộng lớn nhất.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
- Vị trí đi vào model: Nhãn polyline vạch làn đi trực tiếp vào hàm mất mát (loss function) của các mô hình phát hiện làn đường theo dạng điểm/neo (như Ultra-Fast-Lane-Detection, CondLaneNet, hoặc mô hình phân loại đường SVM / Row-anchor).
- Phân tích tác hại của lỗi: Nếu vạch đứt bị cắt thành nhiều polyline rời rạc hoặc dừng sớm ở điểm gần xe (ví dụ không kéo sát mép đáy ảnh $y=720$), ma trận nhãn học dạng row-anchor tại hàng gần xe nhất sẽ mang giá trị "không có làn" (no-lane class). Khi đưa vào hệ thống hỗ trợ giữ làn (LKA - Lane Keeping Assist), model sẽ mất tín hiệu căn giữa làn ở cự ly ngay trước đầu xe (vùng mù cảm biến gần), dẫn tới việc xe tính toán sai độ lệch tâm (lateral offset) và đánh lái giật cục hoặc trôi làn gây mất an toàn nghiêm trọng.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | không có làn | 652.6 | 600.4 | 544.6 | 486.6 |
| x của bạn kia | 693.2 | 654.3 | 598.7 | 541.3 | 484.5 |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?  
   **Trả lời:** Hàng **y = 720** sẽ đổi thành "không có làn" (do vạch kết thúc sớm trước khi chạm tới đáy ảnh $y=720$, cụ thể polyline của chúng tôi bắt đầu ở $y=715.4$ nên tại $y=720$ không có giá trị nội suy).

2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?  
   **Trả lời:**  
   - Ở hàng $y=560$ (xa xe): Lệch nhau $|486.6 - 484.5| = \mathbf{2.1\text{ px}}$.  
   - Ở hàng $y=720$ (sát xe): Một bên có toạ độ $x = 693.2\text{ px}$, bên kia là "không có làn" (lệch trạng thái hoàn toàn).  
   - **Lệch ở hàng 720 ảnh hưởng LKA nhiều hơn** (theo slide 25 bài giảng): Vì hàng $720$ tương ứng với vùng mặt đường ngay sát đầu xe của chúng ta, quyết định trực tiếp góc đánh lái tức thời và vị trí tương đối của thân xe so với tim đường. Sai số hoặc mất làn ở cự ly gần sẽ gây dao động vô lăng lớn và nguy cơ lệch làn ngay lập tức.

3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?  
   **Trả lời:**  
   - Cách tính nội suy hình học thuần tuý theo trục $y$ của các đoạn thẳng không đổi về mặt toạ độ giao điểm $x$.  
   - Tuy nhiên, thứ tự mảng điểm bị đảo ngược ($p_0$ ở xa, $p_n$ ở gần). Các script tiền xử lý dữ liệu huấn luyện (như chuyển đổi sang định dạng TuSimple, CULane, hoặc script trích xuất điểm neo tuần tự theo chiều xe chạy) và các thuật toán tính hướng vector làn (lane direction vector) sẽ bị nhầm lẫn chiều xe chạy, dẫn đến việc mô hình học nhầm vector di chuyển ngược chiều hoặc script kiểm tra tự động (`road_check`) bắt lỗi QC1-04 (ngược chiều).
