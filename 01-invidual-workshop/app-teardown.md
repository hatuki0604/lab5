# Workshop Teardown - MoMo Moni

## 1. Chọn sản phẩm để dùng thử

- **Sản phẩm:** MoMo
- **AI feature:** Moni - trợ lý tài chính, chatbot hỗ trợ phân tích chi tiêu
- **Cách truy cập:** app MoMo

## 2. Promise vs reality

### Product hứa gì?

- Giúp người dùng theo dõi chi tiêu và tự động nhận diện các loại giao dịch.
- Đưa ra gợi ý liên quan đến tài chính cá nhân hoặc tiết kiệm dựa trên lịch sử dòng tiền.
- Cho phép người dùng hỏi nhanh về các khoản chi trong quá khứ ngay trong ứng dụng.

### User nào được hứa sẽ được giúp?

- Người dùng đã sử dụng MoMo và có dữ liệu giao dịch trong ví.
- Người muốn biết nhanh mình đã tiêu bao nhiêu, tiêu vào nhóm nào và mức chi có thay đổi ra sao so với giai đoạn trước.
- Người kỳ vọng Moni hoạt động như một trợ lý tài chính cá nhân, không chỉ hiển thị số liệu mà còn giúp diễn giải ý nghĩa của số liệu đó.

### Tôi kỳ vọng AI làm được task nào?

- Trả lời đúng các câu hỏi về tổng chi tiêu, chi tiêu theo danh mục và so sánh giữa các tháng.
- Hiểu được những câu hỏi chưa rõ ràng như “từ khi dùng MoMo” và biết hỏi lại khi thiếu thông tin về thời gian.
- Chủ động đề xuất bước tiếp theo hữu ích, chẳng hạn như chỉ ra khoản chi bất thường hoặc gợi ý xem dữ liệu theo một khoảng thời gian khác.

### Khi dùng thật, điểm gãy xuất hiện ở đâu?

- Moni xử lý khá tốt với các câu hỏi cụ thể, có thể ánh xạ trực tiếp vào dữ liệu chi tiêu.
- Moni gặp khó khi câu hỏi bị mơ hồ về phạm vi hoặc mốc thời gian.
- Khi chưa chắc chắn, hệ thống chưa ưu tiên hỏi lại người dùng mà thường tự chọn một khoảng thời gian để trả lời.
- Nếu câu trả lời chưa đúng, người dùng phải tự nhận ra vấn đề và tự viết lại prompt từ đầu.

## 3. Evidence

### Observation cụ thể

- Sau khi người dùng chuyển tiền hoặc thanh toán thành công, app hiển thị khung thống kê theo tuần hoặc tháng. Điều này cho thấy Moni được thiết kế xoay quanh use case quản lý chi tiêu, đúng với thông điệp sản phẩm.
- Khi hỏi: `Tổng chi tiêu của tôi là bao nhiêu`, AI trả lời tương đối chính xác và có thể kèm theo phần so sánh với tháng trước.
- Sau mỗi lượt hội thoại, hệ thống hiện câu hỏi: `Tôi có hữu ích không?` với hai lựa chọn phản hồi là `có` và `không`.

### Prompt/input đã thử

- `Tổng chi tiêu của tôi là bao nhiêu`
- `Tổng chi tiêu của tôi từ lúc tôi dùng MoMo`

### Hành vi quan sát được

- Với câu hỏi rõ ràng, AI phản hồi nhanh, đưa ra số liệu cụ thể và đúng với chủ đề người dùng hỏi.
- Với câu hỏi `từ lúc tôi dùng MoMo`, AI không dừng lại để làm rõ mốc thời gian mà tự trả về một khoảng ngày do hệ thống lựa chọn.
- Có trường hợp phần mở đầu câu trả lời nhắc đến một mốc thời gian, nhưng phần kết quả bên dưới lại dùng một mốc ngày khác, khiến người dùng khó tin tưởng vào độ chính xác của output.

### Quote từ app

- `Tôi có hữu ích không?`

## 4. Bốn paths

| Path | Quan sát |
|---|---|
| Happy | Khi người dùng hỏi một câu ngắn và rõ như `Tổng chi tiêu của tôi là bao nhiêu`, Moni trả lời trực tiếp, có số liệu cụ thể và đôi khi bổ sung phần so sánh với tháng trước. |
| Low-confidence | Với các câu hỏi thiếu mốc thời gian như `từ lúc tôi dùng MoMo`, Moni chưa cho thấy trạng thái không chắc chắn. Hệ thống không hỏi lại và cũng không đưa các lựa chọn nhanh như `3 tháng gần đây`, `từ đầu năm`, hoặc `tùy chỉnh ngày`. |
| Failure | Khi AI tự suy đoán sai khoảng thời gian, người dùng chỉ có thể phát hiện bằng cách tự đọc kỹ và đối chiếu kết quả. Hệ thống không cảnh báo rằng câu trả lời đang dựa trên một giả định. |
| Correction | Khi người dùng muốn sửa lại câu hỏi, chưa có UI hoặc flow hỗ trợ chỉnh nhanh. Người dùng phải tự nhập prompt mới và chưa thấy dấu hiệu hệ thống ghi nhớ preference hoặc học từ lần sửa trước đó. |

## 5. Finding thành product decision

### Finding 1

Khi người dùng đưa ra câu hỏi có intent đúng nhưng thiếu thông tin về thời gian, ví dụ `Tổng chi tiêu của tôi từ lúc tôi dùng MoMo`, AI/product có xu hướng tự đoán khoảng thời gian thay vì hỏi lại. Điều này tạo ra câu trả lời nhìn có vẻ hợp lý, nhưng khó kiểm chứng và làm giảm niềm tin của người dùng vào kết quả.

Lỗi thuộc layer: `Intent + Data-tool + UX recovery`

Nên sửa bằng:

- Requirement: mọi truy vấn tổng hợp chi tiêu phải kiểm tra đủ tham số thời gian trước khi gọi dữ liệu.
- UX: nếu thiếu mốc thời gian, bot cần hỏi lại hoặc đưa quick replies để người dùng chọn.
- Fallback: nếu hệ thống buộc phải dùng giá trị mặc định, cần hiển thị rõ giả định đang được áp dụng.
- Test case: các câu như `từ lúc tôi dùng MoMo`, `chi tiêu gần đây`, `dạo này tôi tiêu bao nhiêu` phải đi qua low-confidence path thay vì trả lời ngay.

### Finding 2

Khi AI trả lời chưa đúng hoặc chưa đủ rõ, product gần như chỉ để người dùng tự xử lý bằng cách gõ lại prompt hoặc thoát khỏi flow chat. Điều này khiến trách nhiệm sửa lỗi bị đẩy sang người dùng và chưa tận dụng tốt context đã có trong cuộc hội thoại.

Lỗi thuộc layer: `UX recovery + Promise`

Nên sửa bằng:

- Requirement: mỗi kết quả trả lời nên có hành động sửa nhanh ngay trong giao diện.
- UX: bổ sung các lựa chọn như `Chọn lại khoảng thời gian`, `Xem theo tháng`, `So sánh tháng trước`.
- Human role/fallback: nếu truy vấn quá mơ hồ hoặc hệ thống thất bại hai lần liên tiếp, nên chuyển người dùng sang flow lọc dữ liệu truyền thống thay vì để họ tự thử nhiều prompt khác nhau.

## 6. Sketch as-is / to-be

### As-is

```text
User: "Cho tôi biết tổng chi tiêu từ khi dùng MoMo."
    ->
AI: Tự chọn mốc thời gian theo giả định của hệ thống
    ->
AI: Trả kết quả với khoảng ngày chưa rõ hoặc thiếu nhất quán
    ->
User: Tự đọc và tự phát hiện điểm sai
    ->
User: Gõ lại prompt từ đầu hoặc rời khỏi chat
```

Điểm gãy:

- Gãy ở bước hiểu intent vì nhu cầu của người dùng là đúng, nhưng câu hỏi thiếu tham số thời gian.
- Gãy ở bước recovery vì không có cơ chế sửa lỗi hoặc chọn lại thông tin ngay trong chat.

### To-be

```text
User: "Cho tôi biết tổng chi tiêu từ khi dùng MoMo."
    ->
AI: "Mình chưa rõ bạn muốn xem chi tiêu trong khoảng thời gian nào."
    ->
Quick replies: [Từ đầu năm] [3 tháng gần đây] [Từ khi mở ví] [Chọn ngày]
    ->
User chọn 1 option
    ->
AI truy vấn dữ liệu theo đúng khoảng thời gian đã chọn
    ->
AI trả kết quả + gợi ý hành động tiếp theo
    ->
Actions: [Đổi khoảng thời gian] [So sánh tháng trước] [Xem theo danh mục]
```

Path đã sửa:

- Low-confidence path được xử lý bằng bước hỏi lại thay vì để AI tự suy đoán.
- Failure path có khả năng phục hồi ngay trong cuộc trò chuyện.
- Correction path được hỗ trợ bằng quick replies và action chỉnh sửa nhanh.

## 7. Path mạnh nhất và yếu nhất

- **Mạnh nhất:** Happy path với các câu hỏi ngắn, rõ ràng và bám sát dữ liệu có sẵn.
- **Yếu nhất:** Low-confidence và Correction path, vì hệ thống chưa chuyển được ambiguity thành một flow làm rõ có kiểm soát.

## 8. Câu chốt cho SPEC

Finding này sẽ thay đổi SPEC ở điểm: mọi truy vấn chi tiêu có tham số thời gian chưa rõ phải được đưa qua bước làm rõ bằng quick-reply hoặc date picker trước khi AI được phép trả về kết quả tổng hợp.

## 9. Tự kiểm trước khi nộp

- [x] Có observation cụ thể.
- [x] Có đủ 4 paths.
- [x] Finding được viết thành product decision.
- [x] Có sketch as-is và to-be.
- [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC.
