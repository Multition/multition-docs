# ADR 0001: Multi-repo với backend modular monolith

- Status: Accepted
- Date: 2026-09-28
- Updated: 2026-10-05 — chốt sáu repository, chuyển contracts vào Core API.

## Context

Mobile, web và API có pipeline/deployment khác nhau. Tuy nhiên, tách AI/RAG thành microservice ngay từ đầu làm tăng chi phí hợp đồng API, secret, monitoring và local development.

## Decision

- Dùng sáu repository độc lập cho mobile, web, Core API, AI, infra và docs.
- Giữ profile, competition, team, invitation, authorization và hard constraints trong Core API modular monolith.
- Tách AI service vì dùng Python/model tooling và cần evaluation/deployment độc lập.
- AI service không sở hữu business database và không tự thực hiện hành động lên người dùng.
- Dùng `multition-api/openapi/` làm nguồn OpenAPI/schema chuẩn giữa các repo.
- Generated types được commit trong từng client để clone và kiểm tra độc lập;
  chưa cần phát hành package contracts riêng.

## Consequences

- Mỗi app có CI/CD và release độc lập.
- Thay đổi cross-repo có thể cần nhiều pull request.
- Contract phải được review trước khi implement client hoặc service.
- Local development cần clone các repo thành thư mục sibling.
- Khi triển khai AI, Core API phải có fallback rõ ràng nếu AI service không sẵn sàng.
