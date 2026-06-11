# Getting Started

Follow the steps below after cloning the repository to set up and run the Journal Tracker MCP Server.

---

## 1. Clone the Repository

```bash
git clone https://github.com/pranitsawant80/MCP_servers.git
cd MCP_servers/Journal_Tracker_Server
```

Alternatively, open the project directly in VS Code:

```bash
code .
```

---

## 2. Install UV

First, verify whether UV is already installed:

```bash
uv --version
```

If UV is not installed, install it using one of the following methods.

### Windows

```bash
pip install uv
```

### macOS / Linux

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Verify the installation again:

```bash
uv --version
```

---

## 3. Install Project Dependencies

From the project root directory, run:

```bash
uv sync
```

This will:

* Create a virtual environment
* Install all dependencies listed in `pyproject.toml`
* Prepare the project for execution

Alternatively, you can install FastMCP manually:

```bash
uv add fastmcp
```

---

## 4. Verify Project Configuration

Normally, no changes are required.

The included `pyproject.toml` should already contain the required configuration:

```toml
[project]
name = "journal_tracker_server"
version = "0.1.0"
description = "Journal Tracker MCP Server"
requires-python = ">=3.12"

dependencies = [
    "fastmcp>=3.4.2"
]
```

You only need to modify this file if:

* You want to use a different Python version
* You want to add additional dependencies
* You want to rename the project

---

## 5. Test the MCP Server Locally

Before integrating with Claude Desktop, verify that the server runs correctly.

```bash
uv run journal_server.py
```

If the server starts without errors, proceed to the next step.

---

## 6. Configure Claude Desktop

### Open Claude Desktop Configuration

Navigate to:

**Claude Desktop → Profile → Settings → Developer → Edit Configuration**

Then open the configuration file.

---

### Windows Example

Replace the directory path with the location where **you cloned the repository**.

```json
{
  "mcpServers": {
    "journal-tracker": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\Users\\YourName\\Documents\\MCP_servers\\Journal_Tracker_Server",
        "run",
        "journal_server.py"
      ]
    }
  }
}
```

---

### If Claude Cannot Find UV

Some systems may not have `uv` available in the system PATH.

In that case, replace:

```json
"command": "uv"
```

with the full path to your `uv.exe`.

Example:

```json
"command": "C:\\Users\\YourName\\AppData\\Roaming\\Python\\Scripts\\uv.exe"
```

---

### Finding the UV Path

#### Windows

Open PowerShell:

```powershell
Get-Command uv
```

Example output:

```text
C:\Users\YourName\AppData\Roaming\Python\Scripts\uv.exe
```

---

#### macOS

```bash
which uv
```

Example output:

```text
/Users/yourname/.local/bin/uv
```

---

#### Linux

```bash
which uv
```

Example output:

```text
/home/yourname/.local/bin/uv
```

---

### macOS / Linux Example

```json
{
  "mcpServers": {
    "journal-tracker": {
      "command": "uv",
      "args": [
        "--directory",
        "/Users/yourname/MCP_servers/Journal_Tracker_Server",
        "run",
        "journal_server.py"
      ]
    }
  }
}
```

Only the project directory path needs to be changed.

---

## 7. Restart Claude Desktop

After saving the configuration:

1. Close Claude Desktop completely.(sometimes you may need to end task for claude desktop in task manager then will be able to see new server there.)
2. Reopen Claude Desktop.
3. Start a new chat.
4. Open the **Connectors** section.
5. You should see **journal-tracker** listed.
6. Enable the connector.

The Journal Tracker MCP Server should now be available to Claude.

---

## 8. Verify the Connection

Ask Claude:

```text
What tools are available?
```

You should see tools similar to:

* add_entry
* list_entries
* get_entry
* update_entry
* delete_entry
* summarize_days
* summarize_moods
* summarize_tags
* get_entries_for_summary
* get_statistics

---

## Troubleshooting

### Verify UV Installation

```bash
uv --version
```

### Verify Dependencies

```bash
uv sync
```

### Run the Server Directly

```bash
uv run journal_server.py
```

### Common Issues

#### Server Not Appearing in Claude

* Verify the JSON configuration is valid.
* Verify the project path is correct.
* Verify the path to `uv` is correct.
* Restart Claude Desktop completely.

#### "uv" Command Not Found

Use the full path to the UV executable in the Claude Desktop configuration.

#### Python Dependency Errors

Run:

```bash
uv sync
```

to reinstall all project dependencies.

---

## You're Ready!

Once connected, you can use Claude to:

* Create daily journal entries
* Track moods and ratings
* Review historical entries
* Generate summaries
* Analyze emotional trends
* Reflect on personal growth over time
