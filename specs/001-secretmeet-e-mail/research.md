# Research & Decisions

This document summarizes the key technical decisions for the SecretMeet project MVP.

## Backend
- **Language**: Python 3.11+
- **Runner**: `uv` for dependency management and execution.
- **Framework**: FastAPI for both REST API and WebSocket communication.
- **Server**: Uvicorn as the ASGI server.

## Frontend
- **Framework**: None (No SPA).
- **Library**: HTMX for dynamic partial updates.
- **Styling**: Plain CSS.
- **Scripting**: Minimal vanilla JavaScript for WebSocket client and UI glue.

## Database
- **Engine**: DuckDB for a file-based, serverless database suitable for an MVP.
- **Interaction**: Direct use of the `duckdb` Python API. An SQLAlchemy-compatible driver is a possible future extension if needed.

## Architecture
- **Pattern**: Clean Architecture with clear separation of layers: Domain, Application, Infrastructure, and Presentation.
- **Principles**: SOLID principles will be strictly followed.
- **Domain Layer**: Implemented with `dataclasses`, using `frozen=True` where appropriate for immutability.
- **Data Transfer**: Pydantic for DTOs at the API boundaries for validation.

## Testing
- **Framework**: `pytest`.
- **API Testing**: `httpx` for testing REST endpoints.
- **WebSocket Testing**: `pytest-asyncio`.
- **Code Coverage**: Minimum 85%.

## Tooling
- **Logging**: `loguru` for structured logging.
- **Linting & Formatting**: `ruff`.
- **Type Checking**: `mypy`.
- **Pre-commit hooks**: Will be used to enforce code quality checks.
