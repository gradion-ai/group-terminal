## group_terminal.client.ChatClient

```python
ChatClient(username: str, host: str = 'localhost', port: int = 8723, **terminal_kwargs)
```

Bases: `MessageSender`

Terminal-based chat client for testing and demonstration purposes.

Provides a [Rich](https://github.com/Textualize/rich)-based terminal interface for interacting with a group of users and services connected to a ChatServer instance. Intended for testing and demonstration only, not for production use in applications. The client is typically started from the command line using: `python -m group_terminal.client --username <username>`.

Note

This client uses [termios](https://docs.python.org/3/library/termios.html) for terminal control and is Unix-specific. It will not work on Windows systems.

Initialize the chat client.

Parameters:

| Name       | Type  | Description                                    | Default       |
| ---------- | ----- | ---------------------------------------------- | ------------- |
| `username` | `str` | The name of the this client's user.            | *required*    |
| `host`     | `str` | The hostname or IP address of the chat server. | `'localhost'` |
| `port`     | `int` | The port number of the chat server.            | `8723`        |

### connect

```python
connect() -> bool
```

Connect to the chat server.

### join

```python
join()
```

Join a connected client until disconnected.
