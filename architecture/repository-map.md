# Repository Map

| Repository | Deployable | Data ownership | Không được làm |
|---|---|---|---|
| `multition-mobile` | Expo app | Local session/cache | Truy cập DB hoặc AI trực tiếp |
| `multition-web` | Static web app | Local session/cache | Chứa business rules quan trọng |
| `multition-api` | Node scaffold | OpenAPI/types; PostgreSQL sau khi có schema | Nhúng provider-specific prompt khắp code |
| `multition-ai` | Python scaffold | Chưa sở hữu dữ liệu nghiệp vụ | Ghi team/invite/application trực tiếp |
| `multition-infra` | Compose/deploy config | Volumes/secrets references | Commit secret thật |
| `multition-docs` | Không | Product/architecture knowledge | Trở thành nguồn API contract thứ hai |

## Thứ tự triển khai một feature cross-repo

1. Sửa contract và example trong `multition-api/openapi/`.
2. Implement Core API/AI service và contract tests.
3. Chạy `npm run contracts:check` và `npm run contracts:sync` tại API repo; commit types trong mobile/web.
4. Implement UI.
5. Cập nhật architecture/product docs nếu behavior thay đổi.
6. Deploy dependency trước, client sau; giữ backward compatibility trong migration window.
