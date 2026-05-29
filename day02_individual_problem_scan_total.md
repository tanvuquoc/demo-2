# Day 02 — Individual Problem Scan

## Case ví dụ: Hỗ trợ học viên trong lớp AI đông người

**Một học viên trong khóa AI Practical Competency Program**. Lớp có số lượng học viên lớn, trong khi TA/Lab Coach có hạn. Trong quá trình học và làm lab, học viên thường gặp vấn đề về cài đặt môi trường, API key, lỗi code, không hiểu yêu cầu bài nộp, hoặc chưa biết cách viết Problem Statement đúng. Các câu hỏi được gửi rải rác qua Discord/GitHub/tài liệu lớp, khiến TA phải xử lý nhiều câu hỏi lặp lại và nhiều câu hỏi thiếu thông tin.

---

# 01 — Individual Problem Scan

## Scan rộng

Mình scan **8 problems**, vượt mức tối thiểu 5.

| # | Lăng kính | Vấn đề quan sát được | Ai đang có pain point | Dấu hiệu thật |
|---|---|---|---|---|
| 1 | Lặp lại | Nhiều học viên hỏi trùng về deadline, link nộp bài, yêu cầu điểm danh | TA, học viên | Nhiều câu hỏi giống nhau trong group chat |
| 2 | Thiếu context | Học viên gửi lỗi code nhưng thiếu traceback, thiếu file, thiếu mô tả các bước trước đã làm | TA | TA phải hỏi lại nhiều vòng |
| 3 | Dữ liệu phân tán | Thông tin lớp nằm ở nhiều nơi: slide, GitHub, Discord, notebook | Học viên | Học viên mất nhiều thời gian để tìm và đối chiếu thông tin từ nhiều nguồn. Nếu dùng con số ước lượng như “khoảng 30 phút”, cần xác minh bằng quan sát/log thực tế |
| 4 | Feedback loop yếu | Sau khi AI/TA trả lời, không biết học viên đã giải quyết được vấn đề chưa | TA | Không có nút feedback, không có trạng thái “đã xử lý/chưa xử lý” |
| 5 | Ưu tiên mơ hồ | TA khó biết câu hỏi nào cần xử lý trước khi có nhiều học viên hỏi cùng lúc | TA, học viên | Nhiều câu hỏi quan trọng dễ bị trôi trong group chat |
| 6 | Phân loại kém | Câu hỏi của học viên bị trộn lẫn giữa lỗi kỹ thuật, kiến thức bài học, deadline, bài nộp, GitHub | TA, mentor | TA phải tự phân loại thủ công trước khi trả lời hoặc chuyển người phù hợp |
| 7 | AI có thể tốt hơn | Nhóm không biết nên chọn Rule, Workflow hay Agent cho bài toán | Nhóm, mentor | Có xu hướng làm luôn Agent dù bài toán chỉ cần Rule/Workflow |
| 8 | Tốn thời gian | TA phải đọc lại nhiều đoạn chat trước đó mới hiểu học viên đang mắc ở bước nào | TA, học viên | Câu hỏi nằm rải rác, thiếu mô tả bước đã làm; mất thời gian nối ngữ cảnh |

## Vì sao phần scan này mạnh?

- Có scan rộng trước khi hội tụ, không chỉ dừng ở đúng 5 vấn đề tối thiểu.
- Các vấn đề xuất phát từ bối cảnh học/làm lab thực tế: hỏi lỗi, tìm tài liệu, hỏi deadline, chọn cách dùng AI.
- Mỗi vấn đề đều có actor và dấu hiệu quan sát được.
- Nhiều vấn đề có thể đo được bằng log hoặc quan sát: số vòng TA hỏi lại, số câu hỏi lặp lại, thời gian phản hồi, tỷ lệ câu hỏi bị thiếu context.
- Các vấn đề chưa nhảy ngay vào “làm chatbot”, mà bắt đầu từ pain point và workflow hiện tại.

---

# 02 — Top 3 Problems

Sau khi scan 8 vấn đề, mình chọn 3 vấn đề để phát triển thành Problem Cards. Ba vấn đề này được chọn vì có actor rõ, pain point cụ thể, có thể đo lường bằng chỉ số vận hành và có điểm can thiệp AI hợp lý.

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 | Học viên gửi lỗi code nhưng thiếu context | Pain rõ, xảy ra trực tiếp trong quá trình làm lab; TA phải hỏi lại nhiều vòng trước khi xử lý được | Cần kiểm chứng tỷ lệ câu hỏi thiếu context và số vòng hỏi lại trung bình |
| 2 | Câu hỏi của học viên bị phân loại kém | Nhiều loại câu hỏi bị trộn chung: lỗi kỹ thuật, kiến thức, deadline, bài nộp, GitHub; phù hợp với workflow phân loại/routing | Cần xác định bộ nhãn phân loại nào là đủ dùng |
| 3 | Thông tin lớp bị phân tán ở slide, GitHub, Discord, notebook | Học viên mất thời gian tìm thông tin và TA phải trả lời lại các thông tin đã có trong tài liệu | Cần xác định nguồn nào là chính thức và luôn được cập nhật |

---

# 03 — Problem Cards

## Problem Card #1 — Học viên gửi lỗi code nhưng thiếu context

**Problem 1 câu:**  
Trong quá trình làm lab, học viên thường gửi lỗi code/cài đặt nhưng thiếu traceback, file, đoạn code liên quan hoặc mô tả các bước đã làm, khiến TA phải hỏi lại nhiều vòng trước khi có thể hỗ trợ.

**Actor:**  
Học viên và TA/Lab Coach.

**Thời điểm / bối cảnh:**  
Khi học viên làm bài lab, chạy code local/Colab, cài thư viện, dùng API key hoặc chạy test.

**Current workflow:**

```text
1. Học viên gặp lỗi code/cài đặt
2. Học viên gửi ảnh lỗi hoặc mô tả ngắn lên group chat
3. TA đọc câu hỏi
4. TA phát hiện thiếu thông tin
5. TA hỏi lại: full traceback, code, file, folder, package, bước đã làm
6. Học viên bổ sung thông tin
7. TA phân tích lỗi
8. TA trả lời hướng xử lý
```

**Bottleneck:**  
Bước 4–6: câu hỏi ban đầu thiếu context nên TA chưa thể xử lý ngay, phải hỏi lại nhiều vòng.

**Impact:**  
Học viên chờ lâu hơn, TA mất thời gian thu thập thông tin thay vì xử lý vấn đề, các câu hỏi khác dễ bị chậm phản hồi.

**Success metric:**

- Giảm số vòng hỏi lại trung bình trước khi câu hỏi đủ thông tin.
- Tăng tỷ lệ câu hỏi có đủ traceback/code/file/môi trường ngay từ lần gửi đầu.
- Giảm thời gian từ lúc học viên hỏi đến lúc TA có thể bắt đầu xử lý.

**Non-AI alternative:**  
Tạo form/checklist bắt buộc học viên điền trước khi hỏi lỗi: ảnh lỗi, traceback, code, file, môi trường, bước đã thử.

**AI hypothesis:**  
AI có thể đóng vai trò intake assistant: kiểm tra câu hỏi đã đủ thông tin chưa, hỏi lại đúng phần còn thiếu, phân loại lỗi ban đầu và chỉ chuyển TA khi đã đủ context hoặc khi lỗi phức tạp.

**Quick gut:**  
Workflow + AI. Chưa cần Agent vì quy trình có các bước khá rõ.

### Draft current workflow

```text
CURRENT STATE — thời gian tổng: cần đo từ log thực tế

┌───────────────────────┐       ┌────────────────────────────┐       ┌──────────────────┐
│ 1 Học viên gặp lỗi     │ ───→  │ 2 Gửi ảnh lỗi / mô tả ngắn  │ ───→  │ 3 TA đọc câu hỏi │
│ ⏱ cần đo              │       │ ⏱ cần đo                   │       │ ⏱ cần đo         │
└───────────────────────┘       └────────────────────────────┘       └─────────┬────────┘
                                                                                  │
                                                                                  ▼
┌──────────────────────────────┐       ┌──────────────────────────────┐       ┌───────────────────────┐
│ 6 TA phân tích lỗi            │ ←───  │ 5 Học viên bổ sung context    │ ←───  │ 4 TA hỏi lại info thiếu │
│ ⏱ cần đo                     │       │ ⏱ cần đo                     │       │ ⏱ cần đo   🔴           │
└──────────────┬───────────────┘       └──────────────────────────────┘       └───────────────────────┘
               │
               ▼
┌───────────────────────┐
│ 7 TA trả lời           │
│ ⏱ cần đo              │
└───────────────────────┘

🔴 = Bottleneck: TA phải hỏi lại vì câu hỏi ban đầu thiếu context.
```

### Draft future workflow

```text
FUTURE STATE — AI Intake Assistant cho lỗi code

┌──────────────────────────────┐       ┌──────────────────────────────┐       ┌──────────────────────────────┐
│ 1 Học viên mở form/chat       │ ───→  │ 2 AI kiểm tra đủ context?     │ ───→  │ 3 AI hỏi đúng phần còn thiếu │
│ Input: lỗi/code/ảnh nếu có    │       │ traceback/code/file/env?      │       │ nếu chưa đủ thông tin        │
│ ⏱ cần đo                     │       │ ⏱ tự động                    │       │ ⏱ tự động                   │
└──────────────────────────────┘       └──────────────┬───────────────┘       └──────────────┬───────────────┘
                                                        │                                      │
                                                        │ đủ context                           │ bổ sung xong
                                                        ▼                                      │
┌──────────────────────────────┐       ┌──────────────────────────────┐       ┌──────────────▼───────────────┐
│ 6 Guardrail: tự trả lời hay   │ ←───  │ 5 AI gợi ý tài liệu/cách xử lý│ ←───  │ 4 AI phân loại lỗi            │
│ chuyển TA?                   │       │ chỉ khi có cơ sở rõ           │       │ setup/API/path/test/runtime   │
│ ⏱ tự động                    │       │ ⏱ tự động                    │       │ ⏱ tự động                    │
└──────────────┬───────────────┘       └──────────────────────────────┘       └──────────────────────────────┘
               │
               │ case khó / không chắc
               ▼
┌──────────────────────────────┐       ┌──────────────────────────────┐
│ 7 TA xử lý với context đủ     │ ───→  │ 8 Học viên feedback           │
│ 🟢 Human boundary             │       │ đã xử lý / chưa xử lý / sai   │
│ ⏱ cần đo                     │       │ ⏱ cần đo                     │
└──────────────────────────────┘       └──────────────────────────────┘

🟢 = Human boundary: TA xử lý case khó, không chắc, hoặc liên quan đến bài nộp chính thức.
Fallback: nếu AI không xác định được lỗi hoặc không có nguồn chắc chắn → chuyển TA, không đoán.
Bottleneck mới: TA review case khó đã có đủ context, thay vì hỏi lại thông tin thiếu.
```

**Human boundary:**  
AI không tự kết luận các lỗi phức tạp nếu không chắc. AI phải chuyển TA khi thiếu thông tin, lỗi liên quan đến bài nộp chính thức, hoặc câu trả lời có rủi ro làm học viên sửa sai.

**Expected before/after impact cần validate:**

| Metric | Trước | Sau kỳ vọng | Ghi chú |
|---|---|---|---|
| Số vòng hỏi lại trước khi đủ context | Cần đo | Giảm | Target chính của workflow |
| Tỷ lệ câu hỏi đủ traceback/code/file ngay từ đầu | Cần đo | Tăng | AI hỏi bổ sung trước khi chuyển TA |
| Thời gian TA bắt đầu xử lý được lỗi | Cần đo | Nhanh hơn | Cần timestamp trước/sau |
| Tỷ lệ câu hỏi phải chuyển TA | Cần đo | Chỉ chuyển case khó | AI không thay TA hoàn toàn |
| Rủi ro AI trả lời sai | Có rủi ro khi dùng AI | Cần giảm bằng guardrail | Có HITL và fallback |

---

## Problem Card #2 — Câu hỏi của học viên bị phân loại kém

**Problem 1 câu:**  
Trong quá trình học và làm lab, câu hỏi của học viên bị trộn lẫn giữa nhiều loại như lỗi kỹ thuật, kiến thức bài học, deadline, bài nộp, GitHub hoặc API key, khiến TA phải tự phân loại thủ công trước khi biết nên trả lời, gửi tài liệu hay chuyển cho người phù hợp.

**Actor:**  
Học viên, TA/Lab Coach và mentor.

**Thời điểm / bối cảnh:**  
Khi lớp có nhiều học viên hỏi cùng lúc trên Discord/group chat trong quá trình học lý thuyết, làm lab, nộp bài hoặc xử lý lỗi kỹ thuật.

**Current workflow:**

```text
1. Học viên gặp vấn đề hoặc có câu hỏi
2. Học viên gửi câu hỏi lên group chat
3. Nhiều câu hỏi thuộc nhiều chủ đề bị trộn lẫn trong cùng một kênh
4. TA đọc từng câu hỏi
5. TA tự xác định câu hỏi thuộc loại nào: FAQ, lỗi kỹ thuật, kiến thức, deadline, GitHub, bài nộp
6. TA trả lời nếu câu hỏi đơn giản
7. TA chuyển mentor hoặc người phụ trách nếu câu hỏi phức tạp
8. Học viên chờ phản hồi
```

**Bottleneck:**  
Bước 4–5 là nút thắt chính. TA phải đọc và phân loại thủ công từng câu hỏi trước khi xử lý. Khi số lượng câu hỏi lớn, câu hỏi quan trọng có thể bị trôi hoặc bị xử lý chậm.

**Impact:**  
Học viên phải chờ lâu hơn để được phản hồi. TA mất thời gian cho việc đọc, lọc và phân loại thay vì tập trung giải quyết vấn đề. Các câu hỏi phức tạp hoặc cần mentor có thể bị chuyển muộn. Group chat cũng trở nên khó theo dõi vì nhiều loại câu hỏi bị trộn chung.

**Success metric:**

- Tỷ lệ câu hỏi được phân loại đúng vào các nhóm chính.
- Thời gian từ lúc học viên gửi câu hỏi đến lúc câu hỏi được chuyển đúng người hoặc đúng luồng xử lý.
- Số lượng câu hỏi bị bỏ sót hoặc bị trôi trong group chat.
- Tỷ lệ câu hỏi TA phải phân loại thủ công.
- Tỷ lệ câu hỏi được xử lý đúng ngay từ lần phân luồng đầu tiên.

**Non-AI alternative:**  
Tạo form hoặc template bắt buộc học viên chọn loại câu hỏi trước khi gửi, ví dụ: lỗi kỹ thuật, kiến thức bài học, deadline, bài nộp, GitHub, API key, hoặc cần mentor. Ngoài ra có thể tạo các kênh riêng trên Discord cho từng loại câu hỏi.

**AI hypothesis:**  
AI có thể đóng vai trò router/phân luồng ban đầu. Khi học viên gửi câu hỏi, AI phân loại câu hỏi vào nhóm phù hợp, gắn nhãn mức độ ưu tiên, phát hiện câu hỏi thiếu context và đề xuất chuyển cho TA hoặc mentor nếu cần. Với câu hỏi đơn giản, AI có thể gợi ý tài liệu hoặc câu trả lời nháp để TA kiểm tra.

**Quick gut:**  
Workflow + Routing. Chưa cần Agent vì bài toán chủ yếu là phân loại đầu vào và chuyển đến nhánh xử lý phù hợp. Quy trình có thể định nghĩa trước bằng các nhóm câu hỏi rõ ràng.

### Draft current workflow

```text
CURRENT STATE — thời gian tổng: cần đo từ log thực tế

┌───────────────────────┐       ┌────────────────────────┐       ┌────────────────────────────┐
│ 1 Học viên có câu hỏi  │ ───→  │ 2 Gửi lên group chat    │ ───→  │ 3 Câu hỏi nhiều loại trộn   │
│ ⏱ cần đo              │       │ ⏱ cần đo               │       │ chung trong một kênh        │
└───────────────────────┘       └────────────────────────┘       └──────────────┬─────────────┘
                                                                                  │
                                                                                  ▼
┌───────────────────────┐       ┌────────────────────────┐       ┌────────────────────────────┐
│ 6 TA trả lời đơn giản  │ ←───  │ 5 TA tự phân loại       │ ←───  │ 4 TA đọc từng câu hỏi        │
│ ⏱ cần đo              │       │ thủ công   🔴           │       │ ⏱ cần đo                    │
└─────────────┬─────────┘       └──────────────┬─────────┘       └────────────────────────────┘
              │                                │
              │                                ▼
              │                 ┌────────────────────────┐
              │                 │ 7 Chuyển mentor nếu khó │
              │                 │ ⏱ cần đo               │
              │                 └──────────────┬─────────┘
              │                                │
              ▼                                ▼
┌──────────────────────────────┐
│ 8 Học viên chờ phản hồi       │
│ ⏱ cần đo                     │
└──────────────────────────────┘

🔴 = Bottleneck: TA phải đọc và phân loại thủ công trước khi xử lý.
```

### Draft future workflow

```text
FUTURE STATE — AI Router cho câu hỏi học viên

┌──────────────────────────────┐       ┌──────────────────────────────┐       ┌──────────────────────────────┐
│ 1 Học viên gửi câu hỏi        │ ───→  │ 2 AI xác định intent chính    │ ───→  │ 3 AI kiểm tra đủ context?     │
│ vào form/chat hỗ trợ          │       │ FAQ/tech/kiến thức/deadline   │       │ thiếu thì hỏi bổ sung         │
│ ⏱ cần đo                     │       │ ⏱ tự động                    │       │ ⏱ tự động                    │
└──────────────────────────────┘       └──────────────────────────────┘       └──────────────┬───────────────┘
                                                                                                │
                                                                                                ▼
┌──────────────────────────────┐       ┌──────────────────────────────┐       ┌──────────────────────────────┐
│ 6 TA/mentor nhận queue        │ ←───  │ 5 Chuyển vào luồng phù hợp    │ ←───  │ 4 AI gắn nhãn ưu tiên         │
│ đã phân loại                  │       │ FAQ / Tech / Mentor / Review  │       │ Low / Medium / High / Human   │
│ 🟢 Human boundary             │       │ ⏱ tự động                    │       │ ⏱ tự động                    │
└──────────────┬───────────────┘       └──────────────────────────────┘       └──────────────────────────────┘
               │
               ▼
┌──────────────────────────────┐
│ 7 Học viên nhận trạng thái    │
│ trả lời / cần bổ sung / đã    │
│ chuyển TA                     │
└──────────────────────────────┘

🟢 = Human boundary: câu hỏi học thuật phức tạp, khiếu nại điểm, hoặc case AI không chắc phải chuyển người thật.
Fallback: nếu AI phân loại không chắc → gắn nhãn “needs review” và chuyển TA.
Bottleneck mới: TA xử lý queue đã được phân loại, thay vì đọc toàn bộ group chat thủ công.
```

**Human boundary:**  
AI không tự quyết định các câu hỏi học thuật phức tạp, không tự xử lý khiếu nại điểm, không tự đưa kết luận cuối cùng nếu câu hỏi có rủi ro cao. Các trường hợp AI không chắc, thiếu dữ liệu hoặc liên quan đến đánh giá chính thức phải được chuyển cho TA hoặc mentor.

**Expected before/after impact cần validate:**

| Metric | Trước | Sau kỳ vọng | Ghi chú |
|---|---|---|---|
| Tỷ lệ câu hỏi TA phải phân loại thủ công | Cần đo | Giảm | AI làm bước routing ban đầu |
| Thời gian chuyển câu hỏi đến đúng người/kênh | Cần đo | Nhanh hơn | Cần đo bằng timestamp |
| Tỷ lệ phân loại đúng | Chưa có | Cần đạt ngưỡng chấp nhận | TA gắn nhãn mẫu để kiểm tra |
| Số câu hỏi bị trôi/bỏ sót | Cần đo | Giảm | Cần queue/trạng thái xử lý |
| Rủi ro chuyển sai luồng | Có khi dùng AI | Cần giảm | Confidence threshold + human review |

---

## Problem Card #3 — Thông tin lớp bị phân tán ở nhiều nguồn

**Problem 1 câu:**  
Thông tin quan trọng của lớp như deadline, yêu cầu bài nộp, link GitHub, slide, notebook, hướng dẫn chạy code và quy định lab nằm rải rác ở nhiều nơi, khiến học viên mất thời gian tìm kiếm và TA phải trả lời lại các câu hỏi đã có trong tài liệu.

**Actor:**  
Học viên và TA/Lab Coach.

**Thời điểm / bối cảnh:**  
Khi học viên cần tìm thông tin để làm lab, nộp bài, chạy test, xem lại hướng dẫn hoặc kiểm tra yêu cầu deliverables.

**Current workflow:**

```text
1. Học viên cần tìm thông tin về bài học hoặc bài nộp
2. Học viên tìm trong slide
3. Học viên tìm tiếp trong GitHub
4. Học viên tìm trong Discord/group chat hoặc notebook
5. Nếu vẫn chưa chắc, học viên hỏi TA
6. TA tìm lại nguồn chính xác
7. TA trả lời lại cho học viên
8. Học viên làm tiếp bài lab hoặc chỉnh bài nộp
```

**Bottleneck:**  
Bước 2–5 là nút thắt chính. Tài liệu bị phân tán ở nhiều nguồn, học viên không biết nguồn nào là chính thức hoặc mới nhất. Điều này làm tăng thời gian tìm kiếm và tạo thêm câu hỏi lặp lại cho TA.

**Impact:**  
Học viên mất thời gian tìm thông tin thay vì tập trung làm bài. Một số học viên có thể hiểu sai yêu cầu nộp bài nếu lấy thông tin từ nguồn không đầy đủ hoặc không cập nhật. TA phải trả lời lại các câu hỏi mà thực ra đã có trong slide, GitHub hoặc notebook.

**Success metric:**

- Thời gian trung bình để học viên tìm được thông tin cần thiết.
- Số câu hỏi lặp lại liên quan đến deadline, link nộp bài, yêu cầu folder, GitHub hoặc notebook.
- Tỷ lệ câu trả lời có kèm nguồn chính thức.
- Tỷ lệ học viên tìm được đúng tài liệu mà không cần hỏi TA.
- Tỷ lệ câu trả lời bị báo sai hoặc thiếu nguồn.

**Non-AI alternative:**  
Tạo một trang FAQ hoặc landing page duy nhất chứa toàn bộ link quan trọng: slide, GitHub, notebook, deadline, yêu cầu nộp bài và hướng dẫn chạy test. Có thể ghim bài này trong Discord hoặc gửi lại sau mỗi buổi học.

**AI hypothesis:**  
AI có thể hoạt động như một lớp tra cứu tài liệu. Khi học viên hỏi, AI tìm trong nguồn chính thức như slide, GitHub, notebook hoặc FAQ, sau đó trả lời ngắn gọn kèm nguồn. Nếu không tìm thấy thông tin chắc chắn, AI không được đoán mà phải nói rõ chưa tìm thấy và chuyển câu hỏi cho TA.

**Quick gut:**  
Workflow + document search/RAG. Chưa cần Agent vì bài toán chủ yếu là tra cứu đúng thông tin từ nguồn chính thức, trả lời có nguồn và chuyển TA khi không chắc.

### Draft current workflow

```text
CURRENT STATE — thời gian tổng: cần đo từ log thực tế

┌──────────────────────────────┐       ┌───────────────────────┐       ┌───────────────────────┐
│ 1 Học viên cần tìm thông tin  │ ───→  │ 2 Tìm trong slide      │ ───→  │ 3 Tìm trong GitHub     │
│ deadline/repo/test/notebook   │       │ ⏱ cần đo              │       │ ⏱ cần đo              │
└──────────────────────────────┘       └───────────────────────┘       └───────────┬───────────┘
                                                                                     │
                                                                                     ▼
┌───────────────────────┐       ┌──────────────────────────────┐       ┌──────────────────────────────┐
│ 6 TA tìm nguồn chính   │ ←───  │ 5 Không chắc nên hỏi TA       │ ←───  │ 4 Tìm Discord/notebook        │
│ xác                    │       │ 🔴                            │       │ ⏱ cần đo                     │
└───────────┬───────────┘       └──────────────────────────────┘       └──────────────────────────────┘
            │
            ▼
┌───────────────────────┐       ┌──────────────────────────────┐
│ 7 TA trả lời           │ ───→  │ 8 Học viên tiếp tục làm bài   │
│ ⏱ cần đo              │       │ ⏱ cần đo                     │
└───────────────────────┘       └──────────────────────────────┘

🔴 = Bottleneck: học viên phải tìm qua nhiều nguồn và vẫn không chắc nguồn nào là chính thức.
```

### Draft future workflow

```text
FUTURE STATE — AI Document Search / RAG Assistant

┌──────────────────────────────┐       ┌──────────────────────────────┐       ┌──────────────────────────────┐
│ 1 Học viên nhập câu hỏi       │ ───→  │ 2 AI xác định loại thông tin  │ ───→  │ 3 AI tìm trong nguồn chính    │
│ deadline/repo/test/slide      │       │ deadline/deliverable/test     │       │ thức: slide/GitHub/FAQ        │
│ ⏱ cần đo                     │       │ ⏱ tự động                    │       │ ⏱ tự động                    │
└──────────────────────────────┘       └──────────────────────────────┘       └──────────────┬───────────────┘
                                                                                                │
                                                                                                ▼
┌──────────────────────────────┐       ┌──────────────────────────────┐       ┌──────────────────────────────┐
│ 6 Chuyển TA xác nhận nếu cần  │ ←───  │ 5 Guardrail kiểm tra độ chắc  │ ←───  │ 4 Trả lời ngắn gọn kèm nguồn  │
│ deadline/điểm/quy định        │       │ có nguồn? có mâu thuẫn?       │       │ nếu có nguồn rõ               │
│ 🟢 Human boundary             │       │ ⏱ tự động                    │       │ ⏱ tự động                    │
└──────────────┬───────────────┘       └──────────────────────────────┘       └──────────────┬───────────────┘
               │                                                                      │
               ▼                                                                      ▼
┌──────────────────────────────┐                                       ┌──────────────────────────────┐
│ 7 Log câu hỏi mới để cập nhật │                                       │ Học viên nhận câu trả lời      │
│ FAQ / tài liệu                │                                       │ có nguồn rõ                    │
└──────────────────────────────┘                                       └──────────────────────────────┘

🟢 = Human boundary: thông tin quan trọng nhưng không có nguồn rõ phải chuyển TA xác nhận.
Fallback: nếu không tìm thấy nguồn chính thức hoặc nguồn mâu thuẫn → không bịa, báo chưa đủ thông tin và chuyển TA.
Bottleneck mới: duy trì nguồn tài liệu chính thức và cập nhật FAQ.
```

**Human boundary:**  
AI không được tự bịa deadline, yêu cầu bài nộp, quy định lab hoặc link nộp bài nếu không tìm thấy trong nguồn chính thức. Với thông tin quan trọng như deadline, tiêu chí chấm, điều kiện nộp bài hoặc thay đổi quy định, AI chỉ nên trả lời khi có nguồn rõ ràng; nếu không, phải chuyển TA xác nhận.

**Expected before/after impact cần validate:**

| Metric | Trước | Sau kỳ vọng | Ghi chú |
|---|---|---|---|
| Thời gian học viên tìm thông tin | Cần đo | Giảm | Cần hỏi user hoặc đo log |
| Số câu hỏi lặp lại về link/deadline/yêu cầu nộp bài | Cần thống kê | Giảm | Dùng log group chat |
| Tỷ lệ câu trả lời có nguồn chính thức | Chưa ổn định | Tăng | AI bắt buộc kèm nguồn |
| Tỷ lệ câu trả lời sai/thiếu nguồn | Cần đo | Giảm | Có nút báo sai |
| Rủi ro AI bịa quy định | Có khi dùng AI | Cần giảm | RAG + guardrail + TA xác nhận |

---

# 04 — Lý do chọn Problem #1 để đưa ra bàn luận với nhóm

Mình đề xuất chọn **Problem #1 — Học viên gửi lỗi code nhưng thiếu context** để đưa ra bàn luận với nhóm.

Lý do:

1. **Pain cụ thể nhất:** tình huống rất rõ — học viên gặp lỗi, gửi thiếu thông tin, TA phải hỏi lại.
2. **Actor rõ:** học viên và TA/Lab Coach.
3. **Bottleneck rõ:** thiếu context ở câu hỏi ban đầu.
4. **Metric dễ đo:** số vòng hỏi lại, tỷ lệ câu hỏi đủ context, thời gian đến khi TA xử lý được.
5. **AI can thiệp hợp lý:** AI không thay TA hoàn toàn, chỉ hỗ trợ intake, hỏi lại, phân loại và chuyển TA khi cần.
6. **Rủi ro kiểm soát được:** có human boundary và fallback rõ ràng.
7. **Có thể mở rộng từ #1 sang #2 và #3:** sau khi câu hỏi đủ context, AI có thể phân loại câu hỏi; nếu cần tài liệu, AI có thể tra cứu nguồn chính thức.

Một hướng hội tụ cho nhóm có thể là:

> **AI Intake Assistant cho câu hỏi lab: giúp học viên gửi câu hỏi đủ context, phân loại vấn đề, gợi ý tài liệu phù hợp và chuyển TA khi cần.**

Tuy nhiên, khi pitch với nhóm, nên giữ trọng tâm là **thiếu context khi hỏi lỗi code**, vì đây là pain sắc nhất và dễ bảo vệ nhất.
