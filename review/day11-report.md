# Day 11: Road Elements & SVM — bản xem trước

Đây là bản tóm tắt để xem trên GitHub, không phải bài nộp. Báo cáo đầy đủ, ảnh minh chứng và các file bàn giao được giữ trên máy; bài chính thức gửi qua kênh coach chỉ định.

## Phạm vi

Đã gán nhãn 20 ảnh bắt buộc theo Road v1.0 trên CVAT: 12 ảnh front và 8 ảnh fisheye. Không làm ảnh extra. Bản xuất dùng định dạng CVAT for images 1.1; cả 20 ảnh đều có đủ bốn tag và ZIP nhãn không chứa ảnh gốc.

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 37 | 4 | 3 | 23 | 50 | 54 |
| fisheye | 8 | 9 | 6 | 11 | 9 | 6 | 10 |

## Tự kiểm

- Sáu polyline ở B05–B08 đã sửa `position` thành `other` vì đây là ảnh camera hai bên.
- A10 đã bổ sung `R1`; lần lint gần nhất vẫn nhắc kiểm chiều vẽ của polyline này.
- Lint báo 29 cảnh báo: 5 nặng, 21 chính và 3 nhẹ. Năm cảnh báo nặng đều là `QC1-02` ở A05, A06, A07 và A09; coach đã xác nhận ngoại lệ không có vạch sơn theo ghi nhận của học viên. Lint không thay thế kiểm ảnh hoặc chấm theo nhãn chuẩn.

## Ảnh minh chứng

Báo cáo đầy đủ trên máy có ảnh cấu hình Labels, front A03, fisheye B05 phóng to và đoạn XML của A01. Không đăng ảnh lên GitHub.

## Phiếu QC 1
