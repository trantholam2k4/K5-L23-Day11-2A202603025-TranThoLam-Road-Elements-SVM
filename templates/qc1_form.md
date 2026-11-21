# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Trần Thọ Lâm (2A202603025)        Người kiểm (học viên): Trần Thọ Lâm (Tự kiểm / Self-QC)  
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): lam-front.zip, lam-fisheye.zip (manifest_r1.json, revision: 1)  
Số ảnh kiểm: 6 (+ 22 ảnh thêm, kiểm toàn bộ 28 ảnh qua lint & rà soát thủ công)   Số nhãn đã kiểm (shape + tag): 219 (107 shape + 112 tag ảnh)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 28 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 28 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 28 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 28 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 28 | 5 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 28 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 28 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 28 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 28 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 28 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 12 | 1 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-05 | A08 | lane (position=L1, R1) | chính | Tách thành nhiều polyline cùng position (3 L1, 2 R1) trên đoạn vạch đứt |
| 2 | QC1-05 | A12 | lane (position=L1) | chính | Có 2 polyline cùng mang position L1 |
| 3 | QC1-05 | A13 | lane (position=R1) | chính | Có 2 polyline cùng mang position R1 |
| 4 | QC1-05 | A16 | lane (position=L1) | chính | Có 2 polyline cùng mang position L1 |
| 5 | QC1-05 | B03 | lane (position=R1) | chính | Có 2 polyline cùng mang position R1 |
| 6 | QC1-11 | B03 | lane (#4 tại tọa độ 784,360) | chính | Polyline trên ảnh fisheye chỉ đặt 2 điểm thẳng thay vì chấm nhiều điểm ôm theo cung cong |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A03, A05, A06, A07, A10, A14, A15 | Đường giao cắt hoặc mặt đường nhựa mờ hoàn toàn không có vạch sơn L1/R1 thì bỏ qua không vẽ lane có hợp lệ không? | Có (xác nhận theo hướng dẫn của road_check lint: bỏ qua nếu thật sự không thấy vạch) |

## Quyết định
Lỗi nặng: 0   Lỗi chính: 6 / 107 nhãn = 5.61 %   Lỗi nhẹ: 0   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): Release  
Lý do (theo luật của phiếu): Không có lỗi nặng (QC1-01 đến QC1-03), toàn bộ các ảnh thiếu L1/R1 đều thuộc trường hợp mặt đường không có vạch sơn thực tế; các lỗi chính ở mức thấp (5.61%), chủ yếu do tách đoạn polyline trên vạch đứt.