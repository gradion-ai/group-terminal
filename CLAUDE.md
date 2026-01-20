# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

```bash
uv sync                      # Install/sync dependencies
uv add <dep>                 # Add dependency (--dev for dev deps)
uv run invoke cc             # Run code checks (auto-fixes formatting, mypy errors need manual fix)
uv run invoke test           # Run all tests
uv run invoke ut             # Run unit tests only
uv run invoke it             # Run integration tests only
uv run invoke test --cov     # Run tests with coverage

# Single test file
uv run pytest -xsv tests/integration/test_[name].py

# Single test
uv run pytest -xsv tests/integration/test_[name].py::test_name

# Documentation
uv run invoke build-docs     # Build docs
uv run invoke serve-docs     # Serve docs at localhost:8000
```

**Note:** `invoke cc` only checks files under version control. Run `git add` on new files first.

## Key Modules and Classes

### group_terminal.server

`ChatServer`: WebSocket-based group chat server for testing and demonstration purposes that manages client connections, message broadcasting, and custom message handlers. The server supports multiple clients connecting with distinct usernames to participate in a shared chat session, but does not allow multiple connections with the same username.

`MessageHandler`: Type alias for callback functions that handle incoming chat messages. Handlers are called sequentially in message arrival order, and long-running operations should delegate work to background tasks to avoid blocking the message receiver loop.

### group_terminal.client

`ChatClient`: Terminal-based chat client for testing and demonstration purposes that provides a Rich-based terminal interface for `ChatServer` instances. This client uses termios for terminal control and is Unix-specific (will not work on Windows systems).

### group_terminal.terminal

`TerminalInterface`: Rich-based terminal UI component that handles input buffering, cursor management, and message display with configurable colors for different message types (self, others, agent). The interface provides basic text editing capabilities including cursor movement and backspace, with paste support for larger text inputs.
