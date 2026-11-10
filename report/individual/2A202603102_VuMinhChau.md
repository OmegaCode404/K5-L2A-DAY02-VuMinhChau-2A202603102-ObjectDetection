# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Vũ Minh Châu
- MSSV: 2A202603102
- Email: vuminhchau.12cxm@gmail.com
- Lớp: L2A
- Link repo bài làm: https://github.com/OmegaCode404/K5-L2A-DAY02-VuMinhChau-2A202603102-ObjectDetection.git
- Link Colab đã chạy: https://colab.research.google.com/github/OmegaCode404/K5-L2A-DAY02-VuMinhChau-2A202603102-ObjectDetection/blob/main/notebooks/day2_annotation_to_yolo.ipynb

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train:
- Kết quả checker và lỗi đã xử lý:
- Danh sách ít nhất 10 ảnh đã rà bằng mắt:
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
- Commit khóa nhãn ban đầu:

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP |473 | |
| FP |636 | |
| FN |180  | |
| Precision |0.4265| |
| Recall |0.7243| |
| F1 |0.5369 | |
| mean_iou_of_matches |0.8509 | |
| passed | | |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: Google Colab, CPU; phiên bản Ultralytics và Torch không được lưu trong artifact phiên chạy.
- Các tham số thay đổi so với notebook nếu có và lý do: Không thấy thay đổi ở các tham số train được lưu; `args.yaml` khớp cấu hình notebook (YOLO26n, 50 epochs, imgsz=640, batch=-1, device=cpu, seed=20260909).
- Đường dẫn best checkpoint trong phiên chạy: `/content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt` (artifact kèm báo cáo: [assets/yolo26_runs/vehicle_annotation/weights/best.pt](./assets/yolo26_runs/vehicle_annotation/weights/best.pt)).

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision |0.43316317869565074 |
| Recall |0.24404697815220103 |
| mAP50 |0.2818891662319586 |
| mAP50–95 |0.20966121867198567 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. **Bus có recall thấp nhất.** Ma trận nhầm lẫn normalized của `vehicle_eval` không có dự đoán đúng bus ở ngưỡng đánh giá và cho thấy khoảng một nửa bus thật bị bỏ sót. `drive_058.jpg` là ảnh minh họa có xe bus trong cảnh giao thông; xem ảnh dự đoán tại [assets/eval_predictions/visuals/drive_058.jpg](./assets/eval_predictions/visuals/drive_058.jpg).
2. **Kiểm tra độ khít và vị trí của box**: box có bị lệch tâm, quá rộng/hẹp, hoặc không ôm sát biên vật thể không. mAP50 chỉ yêu cầu IoU đạt 0.50, còn mAP50–95 tính qua nhiều ngưỡng IoU cao hơn nên giảm mạnh có thể phản ánh box chưa chính xác dù đã phát hiện đúng vật thể.
3. **Truck bị nhầm thành car là dấu hiệu cần rà lại theo guideline.** Ma trận nhầm lẫn normalized cho thấy phần lớn mẫu truck thật bị dự đoán là car (0.80). Guideline phân biệt truck bằng khoang/thùng chở hàng và car bằng kiểu xe chở người thông thường; nên rà ảnh và box tương ứng để xác định có nhầm class hay không. Kết quả model chỉ gợi ý cần kiểm tra, không tự chứng minh nhãn gốc sai.
4. **Không dùng 10 ảnh eval để train** để giữ chúng làm dữ liệu chưa tham gia cập nhật trọng số, tránh rò rỉ dữ liệu và có đánh giá trên dữ liệu ngoài train. Trong notebook, 10 ảnh này được khai báo là `val`, dùng theo dõi/đánh giá trong quá trình train, chọn `best.pt`, rồi tính các chỉ số và tạo dự đoán. Vì cũng tham gia chọn checkpoint nên chúng là validation, không phải test set độc lập.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| | | | |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
