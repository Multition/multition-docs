# ADR 0002: Bounded Team Formation Agent

- Status: Accepted
- Date: 2026-09-28

> Architecture decision only. Agent behavior has not been implemented in the current scaffold.

## Decision

Agent được phép quan sát trạng thái, phát hiện gap, truy xuất candidate, áp dụng hard constraints, xếp hạng, giải thích và tạo action draft.

Agent không được tự động:

- Gửi invite/application.
- Thêm hoặc loại thành viên.
- Công khai CV/evidence.
- Bỏ qua eligibility, deadline hoặc privacy rules.
- Đánh dấu evidence là verified khi chưa có nguồn xác minh.

Các hành động ảnh hưởng đến con người dừng tại `AWAITING_HUMAN_APPROVAL`.

## Rationale

Bounded loop vẫn thể hiện agentic behavior nhưng giữ quyết định xã hội quan trọng cho người dùng và tạo điều kiện audit/evaluation.
