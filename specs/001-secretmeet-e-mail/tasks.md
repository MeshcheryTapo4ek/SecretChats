# Tasks: SecretMeet Implementation

**Input**: Design documents from `/specs/001-secretmeet-e-mail/`

## Phase 3.1: Setup
- [ ] T001 [P] Create project structure in `src/` and `tests/` per the implementation plan.
- [ ] T002 [P] Initialize Python project with `uv init`, update `pyproject.toml`, and add dependencies: `fastapi`, `uvicorn`, `duckdb`, `pydantic`, `jinja2`, `python-multipart` (for forms), `loguru`.
- [ ] T003 [P] Add development dependencies: `pytest`, `httpx`, `pytest-asyncio`, `ruff`, `mypy`.
- [ ] T004 [P] Configure `ruff` and `mypy` in `pyproject.toml`.
- [ ] T005 [P] Configure `loguru` for structured JSON logging into rotating files and human readable at stdout in `src/infrastructure/logging.py`.
- [ ] T006 [P] Set up pre-commit hooks for `ruff` and `mypy`.
- [ ] T007 Initialize DuckDB database with `src/infrastructure/db/schema.sql`.

## Phase 3.2: Domain Layer
- [ ] T008 [P] Implement `User` entity and `Nickname`, `PasswordHash` value objects in `src/domain/entities/user.py` and `src/domain/value_objects/`.
- [ ] T009 [P] Implement `ChatRoom` entity and `ChatTitle`, `Money`, `DressCode` value objects in `src/domain/entities/chat.py` and `src/domain/value_objects/`.
- [ ] T010 [P] Implement `Message` entity in `src/domain/entities/message.py`.
- [ ] T011 [P] Implement `Reaction` entity in `src/domain/entities/reaction.py`.
- [ ] T012 [P] Implement `Category` entity in `src/domain/entities/category.py`.
- [ ] T013 [P] Implement `ThemeAsset` entity in `src/domain/entities/theme.py`.
- [ ] T014 [P] Implement `Archive` entity in `src/domain/entities/archive.py`.
- [ ] T015 [P] Implement domain events (`UserDisappeared`, `ChatArchived`) in `src/domain/events/`.
- [ ] T016 [P] Write unit tests for all domain entities and value objects in `tests/unit_domain/`.

## Phase 3.3: Application Layer
- [ ] T017 [P] Define repository interfaces (ports) for all entities in `src/application/ports/`.
- [ ] T018 [P] Define `Clock` and `IdProvider` interfaces in `src/application/ports/`.
- [ ] T019 [P] Implement `register_user` and `login_user` use cases in `src/application/use_cases/`.
- [ ] T020 [P] Implement `create_chat` use case in `src/application/use_cases/`.
- [ ] T021 [P] Implement `list_chats` and `filter_chats` use cases in `src/application/use_cases/`.
- [ ] T022 [P] Implement `post_message` use case in `src/application/use_cases/`.
- [ ] T023 [P] Implement `react_message` and `unreact_message` use cases in `src/application/use_cases/`.
- [ ] T024 [P] Implement `cleanup_expired` use case in `src/application/use_cases/`.
- [ ] T025 [P] Write unit tests for all application use cases in `tests/unit_application/`.

## Phase 3.4: Infrastructure Layer
- [ ] T026 [P] Implement DuckDB `UserRepo` in `src/infrastructure/repos/user_repo_duck.py`.
- [ ] T027 [P] Implement DuckDB `ChatRepo` in `src/infrastructure/repos/chat_repo_duck.py`.
- [ ] T028 [P] Implement DuckDB `MessageRepo` and `ReactionRepo` in `src/infrastructure/repos/`.
- [ ] T029 [P] Implement `Clock` and `IdProvider` services in `src/infrastructure/services/`.
- [ ] T030 Implement the daily cleanup job scheduler in `src/infrastructure/jobs/cleanup_task.py`.
- [ ] T031 [P] Write integration tests for all DuckDB repositories in `tests/integration/`.

## Phase 3.5: Presentation Layer (Tests First)
- [ ] T032 [P] Write contract test for `POST /auth/register` and `POST /auth/login` in `tests/int_api/test_auth.py`.
- [ ] T033 [P] Write contract test for `GET /categories` and `GET /themes/{category}` in `tests/int_api/test_themes.py`.
- [ ] T034 [P] Write contract tests for `GET /chats` and `POST /chats` in `tests/int_api/test_chats.py`.
- [ ] T035 [P] Write integration test for WebSocket `join`, `leave`, and `send_message` actions in `tests/int_ws/test_messaging.py`.

## Phase 3.6: Presentation Layer (Implementation)
- [ ] T036 Implement `auth` router in `src/presentation/api/auth.py`.
- [ ] T037 Implement `categories` and `themes` router in `src/presentation/api/themes.py`.
- [ ] T038 Implement `chats` router in `src/presentation/api/chats.py`.
- [ ] T039 Implement WebSocket endpoint and all actions in `src/presentation/ws/socket.py`.
- [ ] T040 [P] Create Jinja2 `base.html` and `index.html` templates in `src/presentation/templates/`.
- [ ] T041 [P] Create `chats.html` and `chat_room.html` templates with HTMX partials in `src/presentation/templates/`.
- [ ] T042 [P] Implement basic CSS in `src/presentation/static/css/main.css`.
- [ ] T043 Implement WebSocket client in `src/presentation/static/js/ws.js`.

## Phase 3.7: Polish & Finalize
- [ ] T044 Review and ensure all tests pass and meet 85% coverage.
- [ ] T045 Perform manual testing based on `quickstart.md` scenarios.
- [ ] T046 Write a comprehensive `README.md` for the project.
- [ ] T047 [P] Moderator can delete a chat (FR-010)
- [ ] T048 [P] Visual unread indicators (FR-012)

## Dependencies
- **TDD**: Test tasks (Phase 3.5) must be completed and failing before implementation tasks (Phase 3.6).
- **Layers**: Domain (3.2) -> Application (3.3) -> Infrastructure (3.4) -> Presentation (3.6).
- **Setup**: All setup tasks (3.1) must be complete before other phases.
