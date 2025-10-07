# WebSocket Protocol for Chat

**Endpoint**: `/ws/chats/{chat_id}`

## Connection
A client connects to the WebSocket endpoint with a valid chat ID. Authentication is handled via a session cookie or a token provided as a query parameter, established during the initial HTTP login.

## Incoming Messages (Client -> Server)

Messages from the client are sent as JSON objects with an `action` field and a `payload`.

### `join`
- **Description**: A user joins the chat. This is typically the first message sent.
- **Payload**: `{}` (empty)

### `leave`
- **Description**: A user leaves the chat.
- **Payload**: `{}` (empty)

### `send_message`
- **Description**: A user sends a message to the chat.
- **Payload**:
  ```json
  {
    "content": "Hello, world!"
  }
  ```

### `react`
- **Description**: A user adds a reaction to a message.
- **Payload**:
  ```json
  {
    "message_id": "message-ulid",
    "emoji": "👍"
  }
  ```

### `unreact`
- **Description**: A user removes a reaction from a message.
- **Payload**:
  ```json
  {
    "message_id": "message-ulid",
    "emoji": "👍"
  }
  ```

### `pin`
- **Description**: A moderator pins a message.
- **Payload**:
  ```json
  {
    "message_id": "message-ulid"
  }
  ```

## Outgoing Events (Server -> Client)

Events from the server are sent as JSON objects with an `event` field and a `payload`.

### `message_posted`
- **Description**: A new message was posted.
- **Payload**: The full message object.

### `reaction_added`
- **Description**: A reaction was added to a message.
- **Payload**: The reaction object.

### `reaction_removed`
- **Description**: A reaction was removed from a message.
- **Payload**: The reaction object that was removed.

### `pin_set`
- **Description**: A message was pinned.
- **Payload**: The message object that was pinned.

### `presence_update`
- **Description**: The list of online users has changed.
- **Payload**:
  ```json
  {
    "online_users": ["user1", "user2"]
  }
  ```
