# Feature Specification: SecretMeet — Anonymous Meeting and Chat Service

**Feature Branch**: `001-secretmeet-e-mail`
**Created**: 2025-10-06
**Status**: Draft
**Input**: User description: "Создай спецификацию проекта SecretMeet — сервиса для организации анонимных встреч и тематических чатов..."

---

## ⚡ Quick Guidelines
- ✅ Focus on WHAT users need and WHY
- ❌ Avoid HOW to implement (no tech stack, APIs, code structure)
- 👥 Written for business stakeholders, not developers

---

## Clarifications

### Session 2025-10-06
- Q: How should the optional "age" parameter mentioned during chat creation be handled? → A: It's a specific target age range (e.g., "25-35").
- Q: What should the rate limit be for sending messages within a single chat? → A: 10 messages per minute.
- Q: What is the expected scale of the application in the first 6 months? → A: ~1,000 daily active users, ~100 new chats per day.
- Q: What level of observability is required for the MVP? → A: Structured (JSON) logging for all application events.
- Q: How should the application visually communicate errors to the user? → A: Simple browser alerts.

---

## User Scenarios & Testing *(mandatory)*

### Primary User Story
A user wants to find or create anonymous, interest-based social events without revealing their personal identity. They log in with a temporary username, browse themed event chats, and can join an existing one or create their own to coordinate a private meeting.

### Acceptance Scenarios
1.  **Given** a new user visits the site, **When** they enter a unique username, **Then** the system creates an account, shows a one-time password, and logs them in.
2.  **Given** an existing user enters their username, **When** they provide the correct password, **Then** they are logged into their account.
3.  **Given** a logged-in user selects a main category (e.g., "Board Games"), **Then** the UI theme changes dynamically and relevant sub-filters appear.
4.  **Given** a user filters the list of chats, **When** they click on a chat, **Then** they successfully enter the chat room.
5.  **Given** a user is in the system, **When** they create a new chat with all required details (name, time, participants, etc.), **Then** the new chat appears in the public list for others to see.
6.  **Given** a user account has been inactive for 7 days, **When** the daily cleanup job runs, **Then** the account is permanently deleted.
7.  **Given** a chat has had no new messages for 7 days, **When** the daily cleanup job runs, **Then** the chat is deleted.
8.  **Given** a chat's event has passed, **When** the daily cleanup job runs, **Then** the chat is archived.

### Edge Cases
- What happens if a user tries to register a username that is already taken? (System should ask for a password).
- What happens if a user forgets their one-time password? (They cannot recover it and must create a new account).
- How does the system handle a chat creator leaving the chat? (The chat remains, but without a moderator).
- What happens when a chat reaches its maximum number of participants? (No new users can join).

## Requirements *(mandatory)*

### Functional Requirements
- **FR-001**: System MUST allow users to create an account with a unique username.
- **FR-002**: System MUST generate a secure, random password for new accounts and display it only once.
- **FR-003**: System MUST authenticate returning users via their username and password.
- **FR-004**: System MUST display a list of high-level event categories on the main page.
- **FR-005**: System MUST dynamically change the UI theme (colors, background) based on the selected category.
- **FR-006**: System MUST provide filtering options for the chat list, including type, number of people, dress code, budget, date range, and location.
- **FR-007**: System MUST allow users to join any public chat that is not full.
- **FR-008**: System MUST allow users to create new chats, specifying attributes like name, time, participant limit, theme, budget, description, and an optional target age range.
- **FR-009**: The creator of a chat (moderator) MUST be able to kick users from the chat and delete any message.
- **FR-010**: The chat moderator MUST be able to delete the chat itself.
- **FR-011**: System MUST support real-time messaging with text and emoji reactions within chats.
- **FR-012**: System MUST provide visual indicators (e.g., a badge count) for unread messages in the user's chats.
- **FR-013**: System MUST automatically delete user accounts after 7 days of inactivity. The user's name will be marked as "disappeared".
- **FR-014**: System MUST automatically delete active chats if there is no message activity for 7 days.
- **FR-015**: System MUST automatically archive chats for 1 year once the event date has passed.
- **FR-016**: The main page MUST display active chats sorted by the time remaining until the event.
- **FR-017**: The system MUST use simple browser alerts to communicate errors (e.g., network issues, failed actions) to the user.

### Non-Functional Requirements
- **NFR-001**: The user interface MUST be minimalist, clean, and intuitive.
- **NFR-002**: The application MUST use WebSockets for real-time message exchange.
- **NFR-003**: The p95 response time for basic API endpoints MUST be under 100ms.
- **NFR-004**: The application MUST be a self-contained MVP with no external API dependencies for core functionality.
- **NFR-005**: The user interface MUST be responsive and fully functional on mobile devices.
- **NFR-006**: A daily background process (cron job) MUST handle the cleanup of old accounts and chats.
- **NFR-007**: System MUST limit users to sending a maximum of 10 messages per minute within a single chat.
- **NFR-008**: The system architecture SHOULD be designed to handle approximately 1,000 daily active users and the creation of 100 new chats per day within the first 6 months.
- **NFR-009**: All application events MUST be logged to stdout in a structured (JSON) format.

### Key Entities *(include if feature involves data)*
- **User**: Represents a temporary, anonymous user with a unique username and a one-time password.
- **Chat**: Represents a themed event chat room with attributes such as name, event time, maximum participants, budget, dress code, description, and an optional target age range.
- **Message**: A single message within a chat, containing text content and associated emoji reactions.
- **Theme**: Defines the visual appearance (color palette, background images, quotes) associated with a main category.

---

## Review & Acceptance Checklist
*GATE: Automated checks run during main() execution*

### Content Quality
- [ ] No implementation details (languages, frameworks, APIs)
- [ ] Focused on user value and business needs
- [ ] Written for non-technical stakeholders
- [ ] All mandatory sections completed

### Requirement Completeness
- [ ] No [NEEDS CLARIFICATION] markers remain
- [ ] Requirements are testable and unambiguous
- [ ] Success criteria are measurable
- [ ] Scope is clearly bounded
- [ ] Dependencies and assumptions identified

---

## Execution Status
*Updated by main() during processing*

- [ ] User description parsed
- [ ] Key concepts extracted
- [ ] Ambiguities marked
- [ ] User scenarios defined
- [ ] Requirements generated
- [ ] Entities identified
- [ ] Review checklist passed

---