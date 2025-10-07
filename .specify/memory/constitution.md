<!--
Sync Impact Report:
- Version change: None -> 1.0.0
- Added sections:
  - Core Principles:
    - Code Quality
    - Clean Architecture
    - Comprehensive Testing
    - Performance Standards
    - Security First
  - Structured Change Management
  - SOLID Principles
- Removed sections: None
- Templates requiring updates:
  - ✅ .specify/templates/plan-template.md
  - ✅ .specify/templates/spec-template.md
  - ✅ .specify/templates/tasks-template.md
- Follow-up TODOs:
  - TODO(RATIFICATION_DATE): Set initial ratification date
-->
# secret-chats Constitution

## Core Principles

### I. Code Quality
Code must adhere to PEP8 standards and be validated by ruff and mypy. Docstrings must follow Google style. A minimum of 95% type coverage is required, and circular dependencies are forbidden.

### II. Clean Architecture
The project follows the principles of Clean Architecture. The domain layer is implemented using dataclasses. Data Transfer Objects (DTOs) and domain models are strictly separated. Dependencies are managed using inversion of control.

### III. Comprehensive Testing
All code must be tested using pytest, with a minimum of 85% code coverage. Tests must include both unit and integration tests. Database interactions are tested using fixtures.

### IV. Performance Standards
Simple endpoints must have a 95th percentile (p95) response time of less than 100ms. The application must support at least 500 concurrent WebSocket connections on a local development machine.

### V. Security First
All user input must undergo basic validation. Rate limiting must be implemented for message publishing endpoints. The use of unsafe functions like 'eval()' or 'os.system()' is strictly prohibited.

## Structured Change Management

All changes must follow a strict workflow: 1. Specification -> 2. Plan -> 3. Tasks -> 4. Implementation.

## SOLID Principles

All code must strictly adhere to the SOLID principles of object-oriented design.

## Governance

This Constitution is the supreme governing document for this project. It dictates the non-negotiable principles and standards that all contributions must follow. Amendments to this Constitution require a formal proposal, review, and approval process. All pull requests and code reviews must verify compliance with these principles.

**Version**: 1.0.0 | **Ratified**: TODO(RATIFICATION_DATE): Set initial ratification date | **Last Amended**: 2025-10-06