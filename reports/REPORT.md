# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602091
- Ngày / CVAT local: 17/09/2026 / CVAT local (hoặc thay bằng ngày thực tế/CVAT.ai)
- Công cụ đã dùng: CVAT (có/không dùng AI tools)

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | Lỗi format / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | chưa có | 0 / 1 | 3 |
| cp2_slice | chưa có | 0 / 1 | 3 |
| cp5_occlusion | chưa có | 0 / 1 | 3 |
| cp3_thin | chưa có | 0 / 1 | 3 |
| cp4_curb | chưa có | 0 / 1 | 3 |
| cp6_coverage | chưa có | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.
Lỗi hiện tại: Task `easy_semantic` bị lỗi export do xuất sai format (thiếu thư mục SegmentationClass và file PNG). Cần xuất lại theo chuẩn "Segmentation mask 1.1".

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh 1 trong task medium_instance, chiếc xe ô tô ở góc dưới bên trái.
- Class và quy tắc tôi dùng để chọn biên: Class `vehicle`. Quy tắc: vẽ sát theo viền ngoài của xe, bao gồm cả gương chiếu hậu nhưng không bao gồm phần bóng đổ của xe trên mặt đường.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: SAM ban đầu gợi ý gộp cả bóng đổ dưới gầm xe, tôi đã điều chỉnh và xóa bớt vùng bóng đó vì bóng không thuộc vật thể chính cần track.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `easy_semantic` (lỗi khi export toàn bộ task).
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: Lỗi khác (Lỗi cấu trúc/định dạng file ZIP khi export).
- Bằng chứng tôi nhìn thấy: Khi chạy script tự kiểm tra, hệ thống báo `[LỖI] easy_semantic: easy_semantic.zip ! không có PNG trong SegmentationClass/; kiểm format Segmentation mask 1.1`.
- Quy tắc và hành động sửa: Quy tắc: Cần chọn đúng định dạng "Segmentation mask 1.1" khi export cho task semantic trên CVAT. Hành động sửa: Cần quay lại CVAT, bấm Export task và chọn đúng định dạng "Segmentation mask 1.1".
- Sau sửa đã Save và export lại chưa? Tạm thời chưa xuất lại thành công, ghi nhận lỗi để báo lại.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): File ZIP đã được action báo PASS kiểm tra cấu trúc, chưa có điểm cụ thể do chờ ground truth. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| Ảnh 1, góc phải (hard_panoptic) | Nhóm người đứng sát nhau: tách riêng từng người (instance) hoặc gộp chung thành một vùng (stuff). | Quy tắc panoptic: nếu các instance quá sát nhau, khó phân biệt biên thì có thể cân nhắc gộp (crowd). | Quyết định tách riêng (instance) những người nhìn rõ và gộp những người ở quá xa thành vùng chung. |
| Ảnh 2, giữa (medium_instance) | Người đang đi xe đạp: gộp chung người và xe hay tách riêng. | Người và xe là hai vật thể khác nhau dù đang tương tác. | Quyết định tách riêng thành hai object: `person` và `bicycle`. |
| Ảnh 3, viền (easy_semantic) | Xe ô tô bị cột điện che khuất giữa thân: vẽ nối liền xuyên qua cột điện hay tách 2 polygon. | Biên vật thể bị che khuất không hiển thị, vẽ đè sẽ làm sai semantic của cột điện. | Quyết định vẽ ô tô làm 2 polygon lách qua cột điện để giữ đúng class. |
