# ADR 0003: Tách bounded AI service khỏi Core API

- Status: Accepted
- Date: 2026-09-28

> Architecture decision only. Ranking, retrieval and RAG have not been implemented.

## Context

Team Formation Agent cần hard constraints, audit log và human approval; các phần
này là business logic. Semantic ranking, document retrieval và model evaluation
lại phù hợp với Python/model tooling và có vòng release khác.

## Decision

- Core API sở hữu agent state machine, quyền truy cập, hard constraints và action approval.
- AI service chỉ nhận dữ liệu tối thiểu đã được API cho phép.
- AI service trả structured suggestion, confidence, citation và model metadata.
- Core API phải validate output và có deterministic fallback.
- Mobile/web không được gọi AI service trực tiếp.
- AI service không có credential để gửi invitation hoặc sửa team membership.

## Consequences

- Có thể đánh giá hoặc thay model mà không làm thay đổi business rules.
- Cần version contract và distributed tracing giữa API và AI.
- Có thêm một service phải deploy và monitor.
- Khi AI lỗi, Core API phải dùng fallback đã được nhóm thiết kế thay vì làm hỏng luồng chính.
