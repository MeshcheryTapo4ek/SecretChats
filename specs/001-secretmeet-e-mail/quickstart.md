# Quickstart

This guide walks through the primary user flow of creating an account, finding a chat, and sending a message.

## 1. Register
Send a `POST` request to `/auth/register` with your desired nickname.
```bash
curl -X POST -H "Content-Type: application/json" -d '{"nickname": "my-secret-name"}' http://localhost:8000/auth/register
```
The response will contain your one-time password. **Save this password!**

## 2. Login
Send a `POST` request to `/auth/login` with your nickname and password. This will set a session cookie.
```bash
curl -X POST -H "Content-Type: application/json" -d '{"nickname": "my-secret-name", "password": "your-one-time-password"}' http://localhost:8000/auth/login
```

## 3. Find a Chat
Send a `GET` request to `/chats` to see a list of available chat rooms.
```bash
curl http://localhost:8000/chats
```

## 4. Join a Chat
Connect to the WebSocket at `/ws/chats/{chat_id}` using a WebSocket client.

## 5. Send a Message
Once connected, send a JSON message to the WebSocket:
```json
{
  "action": "send_message",
  "payload": {
    "content": "Hello from the quickstart!"
  }
}
```
You should see your message broadcast to other users in the chat.
