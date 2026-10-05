# AI Evaluation Plan

## Baseline recommendation

- Precision@3/5 do team leader đánh giá.
- Invite acceptance rate.
- Tỷ lệ shortlist được lưu hoặc mở evidence.
- Thời gian từ Team Blueprint đến shortlist hữu ích.
- Tỷ lệ hard constraint violation phải bằng 0 trong test suite.

## Competition intelligence

- Exact match/F1 cho deadline, team size và eligibility.
- Citation correctness theo gold question set.
- Refusal correctness khi tài liệu không chứa câu trả lời.
- Tỷ lệ field cần người dùng sửa trước khi publish.

## Agent reliability

- Schema validation pass rate.
- Tool-call success rate.
- Latency và token/cost trên mỗi run.
- Số vòng lặp trước khi dừng.
- Tỷ lệ action nhạy cảm bị chặn đúng tại human approval.

Không dùng nhận xét “AI trả lời hay” làm metric chính. Mỗi evaluation run phải lưu dataset version, policy/prompt version và denominator.
