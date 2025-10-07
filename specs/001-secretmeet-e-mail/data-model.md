# Data Model

This document describes the core entities and their relationships for the SecretMeet project.

## Entities

### User
- **description**: Represents a temporary, anonymous user.
- **attributes**:
    - `id`: ULID/UUID (Primary Key)
    - `nickname`: `Nickname` (Value Object, unique)
    - `password_hash`: `PasswordHash` (Value Object)
    - `created_at`: `datetime`
    - `last_seen_at`: `datetime`

### ChatRoom
- **description**: A public chat for a specific event or topic.
- **attributes**:
    - `id`: ULID/UUID (Primary Key)
    - `title`: `ChatTitle` (Value Object)
    - `creator_id`: `ULID/UUID` (Foreign Key to User)
    - `category_id`: `ULID/UUID` (Foreign Key to Category)
    - `max_participants`: `int`
    - `event_time`: `datetime`
    - `budget`: `Money` (Value Object, optional)
    - `dress_code`: `DressCode` (Value Object, optional)
    - `age_limit`: `int` (optional)
    - `description`: `str`
    - `created_at`: `datetime`

### Message
- **description**: A message posted in a chat room.
- **attributes**:
    - `id`: ULID/UUID (Primary Key)
    - `chat_id`: `ULID/UUID` (Foreign Key to ChatRoom)
    - `user_id`: `ULID/UUID` (Foreign Key to User)
    - `content`: `str`
    - `created_at`: `datetime`
    - `is_pinned`: `bool`

### Reaction
- **description**: An emoji reaction to a message.
- **attributes**:
    - `id`: ULID/UUID (Primary Key)
    - `message_id`: `ULID/UUID` (Foreign Key to Message)
    - `user_id`: `ULID/UUID` (Foreign Key to User)
    - `emoji`: `str`

### Category
- **description**: A topic for chats (e.g., Sports, Board Games).
- **attributes**:
    - `id`: ULID/UUID (Primary Key)
    - `name`: `str`
    - `parent_id`: `ULID/UUID` (optional, for sub-categories)
    - `level`: `int`

### ThemeAsset
- **description**: Visual assets associated with a category.
- **attributes**:
    - `id`: ULID/UUID (Primary Key)
    - `category_id`: `ULID/UUID` (Foreign Key to Category)
    - `type`: `str` (e.g., 'color_palette', 'background_image', 'quote')
    - `value`: `str`

### Archive
- **description**: An archived chat room.
- **attributes**:
    - `id`: ULID/UUID (Primary Key)
    - `chat_id`: `ULID/UUID`
    - `archived_at`: `datetime`
    - `content`: `JSON` (serialized chat history)

## Value Objects
- **Nickname**: A validated username string.
- **PasswordHash**: A securely hashed password string.
- **ChatTitle**: A validated chat title string.
- **Money**: Represents a budget with currency.
- **DressCode**: A validated dress code string.
- **TimeWindow**: Represents a date/time range.

## Relationships
- A `User` can create many `ChatRooms`.
- A `ChatRoom` has one `Creator` (`User`).
- A `ChatRoom` belongs to one `Category`.
- A `ChatRoom` has many `Messages`.
- A `Message` has many `Reactions`.
- A `Message` belongs to one `User` and one `ChatRoom`.
- A `Reaction` belongs to one `User` and one `Message`.
