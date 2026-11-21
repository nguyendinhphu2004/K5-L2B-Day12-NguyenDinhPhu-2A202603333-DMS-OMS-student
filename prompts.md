# Khai báo dùng AI — Nguyễn Đình Phú

Có dùng AI. Công cụ: **Claude Code** (trợ lý lập trình của Anthropic, chạy trên máy cá nhân, dùng các model Claude).

| #   | Công cụ     | Bạn hỏi gì (tóm tắt)                                                                                                  | Bạn dùng kết quả thế nào                                                                                                                | Bạn có kiểm lại không? Bằng gì?                      |
| --- | ----------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| 1   | Claude Code | Đọc repo bài lab, tóm tắt đề, guideline OMS, giải thích `phone.state`                                                 | Dùng để hiểu đề và guideline, không dán nguyên văn vào bài                                                                              | Đối chiếu lại với GUIDE.md, COMMON_ERRORS.md         |
| 2   | Claude Code | Khởi động lại CVAT local lỗi (đổi thư mục cài); tạo project `Day12` với 9 nhãn và task `Day12-G07` (22 ảnh) trên CVAT | Dùng đúng thao tác của AI                                                                                                               | Kiểm trên CVAT: đủ 9 nhãn, 22 ảnh                    |
| 3   | Claude Code | Soạn nháp `ir_log.csv`, `class_list_v0.md`, `TEAM.md`, `self_review.md`, `exit_ticket.md`, `prompts.md`               | Bản nháp do AI soạn; các phần cá nhân (`TEAM.md`, `self_review.md`, `exit_ticket.md`) cần mình đọc lại và chỉnh theo hiểu biết của mình | Đối chiếu với guideline, ảnh trên CVAT, và bài giảng |

Hai file `check_cpA.txt` và `check_cpB.txt` được chạy sau khi đã gán xong cả 22 ảnh, từ `export_final.zip` với `--only`, chứ không phải tại thời điểm checkpoint.
