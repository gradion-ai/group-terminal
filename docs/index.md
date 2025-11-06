# Introduction

Group Terminal is a minimalistic, terminal-based group chat system designed for testing and prototyping AI service integrations. Most group chat systems require authentication, databases, and user management before you can test a single message handler or prototype collaboration of user groups with AI. Group Terminal eliminates this complexity by providing a minimal WebSocket-based chat server and [Rich](https://github.com/Textualize/rich)-powered terminal clients that let you focus on testing your integration logic rather than infrastructure setup.

The project delivers four capabilities to accelerate development workflows. A zero-configuration design means no authentication or database setup is required. Server-side message handlers let you build and test services that respond to group chat messages. The Rich-based terminal interface provides immediate visual feedback with configurable colors for different message types. Finally, the explicit testing-focused design ensures you spend time building features rather than maintaining production concerns like security or persistence.

!!! note
    Group Terminal uses [termios](https://docs.python.org/3/library/termios.html) for terminal control and is Unix-specific. It will not work on Windows systems.


## Installation

```bash
pip install group-terminal
```

## Quickstart

The included example demonstrates how to launch a chat server and register a message handler. The handler echoes back each received message with the pattern "I received '{message}' from {username}". This showcases a basic service integration pattern.

Here's the essential code:

```python title="examples/app.py"
--8<-- "examples/app.py:quickstart-imports"
--8<-- "examples/app.py:quickstart-chatapp"
--8<-- "examples/app.py:quickstart-main"
```

See the [complete example](https://github.com/gradion-ai/group-terminal/blob/main/examples/app.py) for full implementation details.

Start the server:

```bash
python examples/app.py
```

In separate terminals, launch two clients with different usernames:

```bash
python -m group_terminal.client --username alice
python -m group_terminal.client --username bob
```

The screenshots below show a conversation where `alice` sends "Hey everyone! How's it going?" and `bob` replies "Pretty good!". Notice the color coding: your own messages appear in orange, messages from other users in cyan, and agent responses in green. The message handler echoes each message back to all connected clients.

`alice`'s view:

![`alice`'s terminal view](images/client-alice.png)

`bob`'s view:

![`bob`'s terminal view](images/client-bob.png)
