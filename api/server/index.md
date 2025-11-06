## group_terminal.server.ChatServer

```python
ChatServer(host: str = 'localhost', port: int = 8723)
```

WebSocket-based group chat server for testing and demonstration purposes.

Manages client connections, message broadcasting, and custom message handlers. Supports multiple clients connecting with distinct usernames to participate in a shared chat session. Multiple connections with the same username are not allowed.

Example

Basic server with a message handler::

```text
async def handle_message(content: str, username: str):
    print(f"Received '{content}' from {username}")

server = ChatServer(host="0.0.0.0", port=8723)
server.add_handler(handle_message)
await server.start()
await server.join()
```

Initialize the chat server.

Parameters:

| Name   | Type  | Description                                                                                                       | Default       |
| ------ | ----- | ----------------------------------------------------------------------------------------------------------------- | ------------- |
| `host` | `str` | The hostname or IP address to bind the server to. Use "0.0.0.0" to accept connections from any network interface. | `'localhost'` |
| `port` | `int` | The port number to listen on for WebSocket connections.                                                           | `8723`        |

### add_handler

```python
add_handler(handler: MessageHandler)
```

Register a callback to handle incoming chat messages.

Handlers are called sequentially in the order that messages arrive from clients. This is the same order that messages appear in chat clients. For operations that preserve message arrival order (such as adding to a queue), perform them directly in the handler. For long-running message processing, delegate to background tasks to avoid blocking the message receiver loop.

Parameters:

| Name      | Type             | Description                                                                                                                                                  | Default    |
| --------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| `handler` | `MessageHandler` | Callback function that receives message content and username. Multiple handlers can be registered and will be called in registration order for each message. | *required* |

### start

```python
start()
```

Start the chat server asynchronously.

Returns immediately after launching the server task. The server runs in the background and begins accepting WebSocket connections.

### stop

```python
stop()
```

Stop the server gracefully.

Signals the server to shut down and waits for the server task to complete.

### join

```python
join()
```

Wait for the server to complete.

Blocks until stop is called from another task. If you have other means to keep your main coroutine alive, calling join is not necessary.

## group_terminal.server.MessageHandler

```python
MessageHandler = Callable[[str, str], Awaitable[None]]
```

Callback function for handling incoming chat messages.

Handlers receive messages in the order they arrive and are called sequentially. For long-running operations, implementations should delegate work to background tasks to avoid blocking the message receiver loop.

Parameters:

| Name       | Type  | Description                                   | Default    |
| ---------- | ----- | --------------------------------------------- | ---------- |
| `content`  | `str` | The message content sent by a user            | *required* |
| `username` | `str` | The username of the user who sent the message | *required* |
