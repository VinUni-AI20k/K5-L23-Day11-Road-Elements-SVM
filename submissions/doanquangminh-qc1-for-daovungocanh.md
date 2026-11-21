# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): daovungocanh        Người kiểm (học viên): doanquangminh (Đoàn Quang Minh)  
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `daovungocanh-front.zip`, `daovungocanh-fisheye.zip` (không nhận được manifest nên không có `revision`)  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 99 (75 shape + 24 tag)  

Ảnh đã kiểm: A03, A04, A08, A14 (front); B04, B06 (fisheye). Mẫu có đủ đèn và biển dày (A03, A08), vạch vàng đôi (A04, A14), ảnh đêm (A14), camera sau (B04) và camera bên (B06).

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 14 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 14 | 2 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 16 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 23 | 1 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 45 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 22 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 9 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

Cách đếm "Số mục kiểm": QC1-01, QC1-02 đếm theo ảnh; QC1-03 đến QC1-06 đếm theo polyline `lane`; QC1-07 đếm drivable (10), crosswalk (4) và road_curb (2); QC1-08 đếm đèn; QC1-09 đếm đèn cộng biển; QC1-10 đếm biển; QC1-11 đếm mọi hình trên ảnh B; QC1-12 đếm file.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-08 | A14 | traffic_light #10 | nặng | Đèn đang sáng **xanh** (bóng dưới sáng xanh ngọc) nhưng gán `color = red`, `facing = front` (đèn hướng về xe) |
| 2 | QC1-03 | B04 | lane #3 (R1) | nặng | Polyline nằm trên mép vỉa hè bên phải, không có vạch sơn. Đây là `road_curb`, không phải lane R1 |
| 3 | QC1-06 | A14 | lane #1 (L1) | chính | Vạch tim đường là vàng đôi nhưng gán `color = white` |
| 4 | QC1-05 | A14 | lane #3 (L2) | chính | Nét thứ hai của **cùng** vạch vàng đôi bị vẽ thành polyline riêng (L2, white). Vạch đôi phải là một polyline, `kind = double` |
| 5 | QC1-05 | A04 | lane #1 (L2) | chính | Nét thứ hai của vạch vàng đôi (lane #3, L1 yellow double) bị vẽ thành polyline riêng, gán L2 / white / single |
| 6 | QC1-07 | A08 | drivable #24 (direct) | chính | Polygon dừng ở mép trên vạch ngựa vằn (y ≈ 440), bỏ phần mặt đường qua crosswalk tới mép capô. Vùng lái thiếu nhiều |
| 7 | QC1-07 | A08 | drivable #25 (alternative) | chính | Cùng lỗi với #6: dừng ở mép trên crosswalk, không kéo tới mép capô |

Ảnh không phát hiện lỗi: **B06** (tag `fisheye_left` đúng với hậu tố MVL; lane #0 có `position = other`; drivable dừng ở mép thân xe; crosswalk một polygon). A03 không có lỗi chắc chắn, xem ca mơ hồ.

Ghi chú lint (`road_check lint`): QC1-02 "chưa có R1" ở A14 nằm trong mẫu. Đối chiếu ảnh: bên phải chỉ có mép đường (đã vẽ 2 road_curb), không có vạch sơn, nên không tính lỗi. Ngoài mẫu, lint còn báo QC1-02 ở A05, A06 và 3 biển thấp dưới 8 px ở A10 (nhẹ, không bắt buộc). A11 (ngoài mẫu) có cùng kiểu lỗi vạch vàng đôi bị vẽ thành hai polyline L1 + L2.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| B04 (cả B03) | Camera sau nhìn ngược chiều xe chạy: L1/R1 tính theo trái/phải của **ảnh** hay theo **hướng xe**? Lô này gán L1 ở bên trái ảnh | |
| A04, A14 | Nét thứ hai của vạch đôi vẽ thành lane riêng: tính QC1-05 (vạch bị tách, như cách `road_check` ghép) hay QC1-03 (vạch thừa, mức nặng)? Phiếu này tạm ghi QC1-05 | |
| A08 | Biển nhỏ "PASSENGER CARS ONLY" gắn phía trên biển chỉ dẫn lớn (traffic_sign #8): `information` hay `supplementary`? Lô gán information | |
| A03 | Checkpoint ghi A03 có đoạn vạch bị che (`occluded`). Lô không bật occluded ở lane nào, nhưng người kiểm không xác định được chắc vạch nào bị che | |

## Quyết định
Lỗi nặng: 2   Lỗi chính: 5 / 99 nhãn = 5,1 %   Lỗi nhẹ: 0   Ca chờ lead: 4  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): còn 2 lỗi nặng (QC1-08 sai màu đèn hướng về xe ở A14; QC1-03 vẽ lane trên mép vỉa hè ở B04), một lỗi nặng đã đủ Rework. Ngoài ra, tỉ lệ lỗi chính 5,1 % (5 / 99 nhãn đã kiểm, tính trên số nhãn chứ không trên số ảnh) vượt ngưỡng 5 %. Bốn ca mơ hồ không đổi được kết luận này, nên không chọn Hold.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
