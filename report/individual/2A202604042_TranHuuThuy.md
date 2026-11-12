# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: **[2A202604042]**
- Ngày / CVAT local: **[12/11/2026]**
- Công cụ đã dùng: Polygon, Intelligent Scissors (OpenCV), công cụ Mask/Brush.**

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | chưa có | 0 / 2 | 30 |
| cp1_holes | chưa có | 0 / 1 | 3 |
| cp2_slice | chưa có | 0 / 1 | 3 |
| cp5_occlusion | chưa có | 0 / 1 | 3 |
| cp3_thin | chưa có | 0 / 1 | 3 |
| cp4_curb | chưa có | 0 / 1 | 3 |
| cp6_coverage | chưa có | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: **[SỬA cho đúng]** ảnh đường phố có cô gái mặc áo dài trắng băng qua đường, xe máy bên trái cô gái.
- Class và quy tắc tôi dùng để chọn biên: class `motorcycle`. Cô gái đứng chắn giữa xe nên xe bị chia thành hai phần (thân và bánh sau bên trái, bánh trước bên phải). Quy tắc của tôi là chỉ vẽ phần nhìn thấy, không đoán phần bị che, dừng mask đúng ở viền áo dài của cô gái, và hai phần vẫn là một instance.
- Nếu dùng gợi ý sau đó: **[ĐIỀN nếu có dùng SAM hoặc Scissors: vùng gợi ý sai/đúng, bạn sửa hay giữ, vì sao]**
- Nếu không dùng gợi ý: ghi "không dùng", vẫn giữ quyết định gán nhãn ở trên.
  
## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: medium_instance, ảnh đường phố có xe buýt hai tầng đỏ và taxi vàng, hàng xe đỗ bên trái và bên phải.
- Lỗi thuộc loại: thiếu-thừa vật (thiếu vật).
- Bằng chứng tôi nhìn thấy: sau khi bật màu theo instance, còn nhiều xe rõ hình dạng chưa có mask: các xe van bạc cạnh mask cam nhỏ bên trái, taxi vàng nhỏ phía xa, xe phủ bạt ở mép trái ảnh, các sedan đỗ bên phải giữa nhóm người đi bộ và hai mask đỏ ngoài cùng.
- Quy tắc và hành động sửa: quy tắc của tôi là mọi xe còn nhìn rõ hình dạng đều phải là một instance riêng, label `car`. Tôi dùng công cụ Mask (Brush) như các xe đã vẽ, tô từng xe còn thiếu rồi bấm Done để mỗi xe là một mask riêng, chỉ tô phần nhìn thấy, không gộp nhiều xe vào một mask. Xe chỉ còn là chấm quá nhỏ ở cuối đường thì tôi bỏ qua.
- Sau sửa đã Save và export lại chưa? **["Đã Save và export lại medium_instance.zip"]**

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. Ảnh đường phố áo dài, góc dưới bên trái | Bánh xe chỉ lộ một phần nhỏ: là `bicycle` hay `motorcycle`, hoặc quá nhỏ nên bỏ | Bánh dày, có vẻ cùng kiểu với các xe máy trong ảnh, nhưng hầu như không thấy thân xe | Câu hỏi cho coach: vật bị cắt gần hết ở mép ảnh có phải gán nhãn không? |
| 2. Ảnh đường phố áo dài, xe bán tải bạc ở giữa | `car` hay `truck` | Theo quy ước kiểu COCO, xe bán tải thường tính là `truck`, nhưng nhìn như xe con có thùng sau | Dùng `truck`, hỏi coach xác nhận quy ước của lớp |
| 3. Các ảnh có người và xe rất nhỏ ở xa | Gán nhãn từng xe/người nhỏ hay bỏ qua | Mức medium ưu tiên vật thể đủ lớn để thấy hình dạng; chấm nhỏ ở cuối đường khó vẽ chính xác | Bỏ qua vật thể quá nhỏ, áp dụng thống nhất cho mọi ảnh, hỏi coach ngưỡng kích thước tối thiểu |
