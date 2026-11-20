# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): trangtnh        Người kiểm (học viên): nguyenthihonghanh  
Ngày: 2026-11-20 / 2026-11-21                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): trangtnh-front.zip, trangtnh-fisheye.zip (revision 1)  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 80 (56 shapes + 24 tags)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 2 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 9 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 13 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 5 | 2 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 9 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 9 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 11 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 19 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 8 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 12 | 1 | chính |
| QC1-12 file | lỗi file | 2 | 2 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A04_b7a8e795-0ff55db2.jpg | lane | nặng | Bỏ sót vạch L1 sát bên trái xe (ảnh có vạch đôi L2 và vạch L1 rõ ràng nhưng chỉ gán L2 và R1). |
| 2 | QC1-02 | A07_b41ace08-c8468690.jpg | lane | nặng | Bỏ sót vạch L1 bên trái làn đang đi (mới chỉ gán R1 và R2, thiếu L1). |
| 3 | QC1-05 | A04_b7a8e795-0ff55db2.jpg | lane (position=R1) | chính | Vạch đứt bị tách thành 2 polyline riêng biệt thay vì nối liền 1 polyline xuyên suốt. |
| 4 | QC1-05 | A08_c0deebc1-16cfa791.jpg | lane (position=L1) | chính | Vạch đứt bị tách thành 2 polyline mang cùng position L1. |
| 5 | QC1-06 | A04_b7a8e795-0ff55db2.jpg | lane (position=L2) | chính | Sai thuộc tính color: vạch vàng đôi (kind=double) nhưng chọn color='white'. |
| 6 | QC1-11 | B03_04267_RV.png | traffic_sign id=6 | chính | Sai thuộc tính edge_zone: tâm hộp biển nằm trong 80% bán kính vòng tròn ảnh nhưng bật edge_zone='true'. |
| 7 | QC1-12 | B06_04068_MVL.png | crosswalk id=1 | nhẹ | Lỗi hình vẽ: có 2 điểm nút lặp liền nhau (click hai lần liên tiếp tại cùng toạ độ). |
| 8 | QC1-12 | B06_04068_MVL.png | drivable id=2 | nhẹ | Lỗi hình vẽ: có điểm nút lặp liền nhau (click hai lần). |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A07_b41ace08-c8468690.jpg | Mặt đường trời mưa ướt, vạch L1 phản quang mờ bên trái có được coi là đủ rõ để bắt buộc gán không? | Có, vạch L1 vẫn nhận diện được tim đường nên bắt buộc phải gán. |
| B06_04068_MVL.png | Vạch kẻ đường phía gương trái (MVL) có dạng vạch kẻ vạch qua đường, nên gán crosswalk hay lane position=other? | Theo guideline mục 4, vạch ngựa vằn gán crosswalk (polygon), không gán lane. |

## Quyết định
Lỗi nặng: 2   Lỗi chính: 4 / 80 nhãn = 5.0 %   Lỗi nhẹ: 2   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): Rework  
Lý do (theo luật của phiếu): Lô còn 2 lỗi nặng (QC1-02: bỏ sót vạch L1 ở ảnh A04 và A07 khi vạch còn thấy rõ). Theo luật quyết định tại mục 3 của thang mức lỗi Road v1.0: "Có ít nhất một lỗi nặng → Rework".

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
