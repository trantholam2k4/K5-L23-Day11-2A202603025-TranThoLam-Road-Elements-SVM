# Báo cáo cá nhân — Ngày 11
Họ tên: Trần Thọ Lâm               Mã học viên: 2A202603025  
Phiên bản CVAT (Help → About): CVAT 2.x (Local Docker WSL)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 21/11/2026 10:42 & 10:49 (UTC 03:05 & 03:49)    Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | Đủ 6 nhãn (`lane`, `road_curb`, `crosswalk`, `drivable`, `traffic_light`, `traffic_sign`) đúng hình học polyline/polygon/box |
| Thuộc tính và giá trị | Đúng | Đầy đủ thuộc tính (`position`, `style`, `color`, `kind`, `state`, `type`, `facing`) đúng giá trị chuẩn |
| 4 tag ảnh | Đúng | Đủ 4 tag trên toàn bộ 28 ảnh: `camera`, `timeofday`, `weather`, `source` |
Cách kết thúc polyline trên bản CVAT này: Bấm phím `N` hoặc nhấp đúp chuột trái (hoặc bấm nút `Done` trên thanh công cụ) sau khi đặt điểm cuối cùng.  
Cách đặt tag ảnh trên bản CVAT này: Chọn công cụ `Tag` (biểu tượng thẻ) ở thanh công cụ bên trái, chọn tên tag (`camera`, `timeofday`, `weather`, `source`) và bấm `Add tag`, sau đó chọn giá trị ở mục `Details` bên cột Objects.  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 28 | 0 | 4 | 19 | 1 | 0 |
| front-extra (đã làm 4 / 4) | 4 | 8 | 0 | 7 | 10 | 0 | 0 |
| fisheye | 8 | 3 | 0 | 7 | 12 | 1 | 0 |
| fisheye-extra (đã làm 4 / 4) | 4 | 0 | 0 | 3 | 4 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A03, A05, A06, A07, A10, A14, A15 | lane | Cố ước lượng vẽ vạch ảo L1/R1 hay bỏ qua | Không gán vạch L1/R1 không tồn tại | Đường qua giao lộ hoặc mặt nhựa mờ không có vạch sơn thực tế; guideline cấm bịa vạch khi không nhìn thấy |
| A04 | lane | Vạch vàng đôi bên trái là L1 hay L2 | L1 (`color=yellow`, `kind=double`, `style=solid`) | Nắp capo xe đặt ở làn sát vạch vàng đôi nên vạch vàng đôi là ranh giới trái trực tiếp (L1) của ego-lane |
| B03 | lane | Chấm 2 điểm đầu cuối hay chấm nhiều điểm trung gian | Cần chấm nhiều điểm theo cung | Ảnh fisheye bị méo góc rộng (barrel distortion), nối 2 điểm thẳng sẽ làm lệch polyline khỏi tâm vạch cong |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Trần Thọ Lâm (Tự kiểm / Self-QC)  Quyết định nhận được: Release  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-05 | 5 | Đồng ý | Chưa (đã giải trình do tách đoạn vạch đứt) |
| QC1-11 | 1 | Đồng ý | Chưa (ghi nhận lưu ý chấm thêm điểm cong trên fisheye) |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| lam-front.zip | Có | A01: 7 / 7 | A02: 3 / 3 | Có |
| lam-fisheye.zip | Có | B01: 3 / 3 | B02: 2 / 2 | Có |

## 6. Ảnh chụp màn hình
1. Tab Labels của project.![alt text](<Screenshot 2026-11-21 110110.png>)
2. Một ảnh camera trước đã gán đủ (ví dụ ảnh `A12` có đủ `lane`, `drivable`, `crosswalk`, `traffic_light`).![alt text](<Screenshot 2026-11-21 110209.png>)
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong (ví dụ `B03`).![alt text](<Screenshot 2026-11-21 110254.png>)
4. Một đoạn XML có `<polyline label="lane">` (mở `annotations.xml` trong `lam-front.zip`).![alt text](<Screenshot 2026-11-21 110320.png>)

## 7. Tự đánh giá
Lỗi mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Lỗi mắc nhiều nhất là **QC1-05** (tách vạch đứt thành nhiều polyline rời cùng `position`, hoặc nhân bản polyline trên CVAT mà quên đổi thuộc tính `position` từ `L1` sang `R1`/`L2`). Cách tránh ở Ngày 20: luôn nối xuyên suốt một `position` thành một polyline liên tục dọc theo vạch đứt, và kiểm tra ngay cột `Objects` bên phải sau mỗi khi nhân bản đối tượng.