# For Users Cloning This Repository

After cloning this repository, follow these steps:

## 1. Clone the Repository

```bash
git clone https://github.com/pranitsawant80/MCP_servers.git
cd MCP_servers/Journal_Tracker_Server
```

Or open the project directly in VS Code:

```bash
code .
```

---

## 2. Install UV

Verify UV is installed:

```bash
uv --version
```

If not installed:

### Windows

```bash
pip install uv
```

### macOS/Linux

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

---

## 3. Install Dependencies

From the project root:

```bash
uv sync
```

or

```bash
uv add fastmcp
```

This will create the virtual environment and install all required packages.

---

## 4. Verify pyproject.toml

Normally no changes are required.

The included `pyproject.toml` already contains the required configuration:

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

Only modify this file if:

* You want a different Python version.
* You want to add additional dependencies.
* You want to rename the project.

---

## 5. Run the Server

Test locally before connecting to Claude Desktop:

```bash
uv run journal_server.py
```

If the server starts successfully, proceed to the next step.

---

## 6. Update Claude Desktop Configuration

This is the most important step.

Open your Claude Desktop configuration file:

### Windows

go to claude desktop>profile>setting>developer>editconfiguration> edit file 

Replace the project path with the location where YOU cloned the repository.

### Example (Windows)

```json
{
  "mcpServers": {
    "journal-tracker": {
      "command": "uv",
      "args": [
        "--directory",
        "C:\\Users\\YourName\\Documents\\MCP_servers\\Journal_Tracker_Server", #path to the directory where we have journal_server.py file 
        "run",
        "journal_server.py"
      ]
    }
  }
}
```

note: for getting path to uv file we can give following comman.
Windows
Get-Command uv
Example output:
C:\Users\YourName\AppData\Roaming\Python\Scripts\uv.exe

macOS
which uv
Example output:
/Users/yourname/.local/bin/uv

### Example (macOS/Linux)

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

Only the path needs to be changed.

---

## 7. Restart Claude Desktop

After saving the configuration:

1. Close Claude Desktop completely.
2. Reopen Claude Desktop.
3. Start a new chat.

Claude should automatically detect the Journal Tracker MCP server.

---

## 8. Verify the Server is Connected

Ask Claude:

```text
What tools are available?
```

You should see tools such as:

* add_entry
* list_entries
* get_entry
* update_entry
* delete_entry
* summarize_days
* summarize_moods
* get_entries_for_summary

---

## VS Code Users

If using VS Code:

1. Open the cloned folder.
2. Open the integrated terminal.
3. Run:

```bash
uv sync
```

4. Test:

```bash
uv run journal_server.py
```

5. Configure Claude Desktop with your local project path.

No additional VS Code configuration is required.
