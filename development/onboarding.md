# Developer Onboarding

## Prerequisites

- Git và tài khoản có quyền đọc các repo trong organization.
- Node.js 24, npm 11.
- Python 3.12.
- Docker Desktop với Compose v2.
- Expo Go hoặc Android/iOS simulator nếu làm mobile.

## Clone

```bash
mkdir multition-workspace
cd multition-workspace
git clone https://github.com/Multition/multition-infra.git
./multition-infra/scripts/clone-all.sh
```

Mở `multition-infra/Multition.code-workspace` bằng VS Code.

## Install

```bash
cd multition-api && npm ci
cd ../multition-web && npm ci
cd ../multition-mobile && npm ci
cd ../multition-ai
python3.12 -m venv .venv
source .venv/bin/activate
pip install -e '.[dev]'
deactivate
cd ..
```

Copy `.env.example` thành `.env` tại `multition-infra`, `multition-api`,
`multition-ai`, `multition-web` và `multition-mobile`. Không commit `.env`.

## Start

```bash
cd multition-infra
docker compose -f compose.dev.yaml up -d postgres minio
```

Chạy AI, API, web và mobile ở các terminal riêng theo README của từng repo.

## Before opening a pull request

- Mobile: `npm run typecheck && npm run lint`.
- Web: `npm run lint && npm run typecheck && npm run build`.
- API: `npm run typecheck && npm test && npm run build`.
- AI: `ruff check . && mypy src && pytest`.
- Contracts (trong API repo): `npm run contracts:check`; commit generated types nếu thay đổi.
- Infra: `docker compose -f compose.dev.yaml config --quiet`.

Feature thay đổi payload phải bắt đầu bằng pull request sửa `multition-api/openapi/`.
Chạy `npm run contracts:sync` tại API repo để cập nhật types của mobile/web nếu
các repo đã được clone cạnh nhau. Mỗi client commit snapshot generated của mình,
nên clone riêng client vẫn cài dependencies và chạy kiểm tra được.
Không merge client dựa trên payload chưa được contract hóa.

## Làm việc hằng ngày

Vào đúng repo mình phụ trách trước khi chạy Git:

```bash
cd multition-mobile
git switch main
git pull --ff-only
git switch -c feat/your-feature
# Sửa code, chạy kiểm tra theo README.
git add path/to/changed-file
git commit -m "feat: describe your change"
git push -u origin feat/your-feature
```

Mở pull request từ nhánh feature vào `main`, nhờ thành viên khác review và kiểm
tra CI trước khi merge. Issue thuộc repo thực hiện công việc; GitHub Project ở
Organization có thể gom các issue của cả sáu repo. Không khởi tạo Git ở thư mục cha.
