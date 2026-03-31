# DateWise Calendar

A sidebar calendar extension for VS Code / Antigravity that displays date-based file lists with Google Calendar integration and a quick command bar.

## Features

### Monthly Calendar
- Full month view with 6-week grid, today highlight, and weekend colors
- Navigate months with arrows, click month title to jump to today
- Color dots showing file types per date (Notes / Data / Images / Others / Event)
- Multi-date selection with Ctrl+Click

### Date-Based File Explorer
- Click a date to see all files matching `YYMMDD` or `YYYY-MM-DD` filename patterns
- Files grouped by type: Notes (.md, .canvas, .txt), Data (.xlsx, .csv, .json), Images, Others
- Markdown/Canvas files open in Obsidian, text files in editor, binaries in default app

### Google Calendar Integration
- View Google Calendar events directly in the sidebar (requires [gogcli](https://github.com/nicholasgasior/gogcli))
- Filter to show only selected calendars
- Events displayed with time and title under each date

### Command Bar
Quick input bar at the bottom for fast actions:

| Command | Action |
|---------|--------|
| `/memo` | Add memo to daily note |
| `/todo` | Add todo checkbox to daily note |
| `/ask` | Add question to daily note |
| `/idea` | Save idea to inbox |
| `/find` | Search files by name across workspace |
| `/grep` | Search file contents with line numbers |
| `MMDD` / `YYMMDD` | Jump to date |

- Slash command autocomplete with Tab
- Command history with Arrow Up/Down (up to 50)
- Auto-creates daily notes when needed

### Status Bar
- Calendar icon in the status bar for quick toggle access

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+Alt+B` (Win/Linux) | Toggle calendar sidebar |
| `Cmd+Option+B` (Mac) | Toggle calendar sidebar |

## Installation

### From Open VSX
Search for "DateWise Calendar" in the Extensions view (`Ctrl+Shift+X`).

### From VSIX
1. Download the `.vsix` file
2. `Ctrl+Shift+P` > "Extensions: Install from VSIX..." > select file
3. Restart IDE

### Move to Right Sidebar (recommended)
By default, the calendar appears in the left sidebar. To move it to the right:

1. Right-click the **Calendar** tab in the left sidebar
2. Select **"Move to Secondary Side Bar"**
3. Done — the position is saved automatically

## Requirements

- **VS Code** 1.80+ / Antigravity / any VS Code compatible editor
- **Obsidian** (optional) — for opening .md/.canvas files in Obsidian. Vault name must match the workspace folder name.
- **gogcli** (optional) — for Google Calendar integration

### Google Calendar Setup (optional)

Google Calendar events require [gogcli](https://github.com/nicholasgasior/gogcli). Without it, all other features work normally.

**macOS:**
```bash
brew install nicholasgasior/tools/gogcli
gog auth login
```

**Windows:**
1. Download `gog.exe` from [gogcli releases](https://github.com/nicholasgasior/gogcli/releases)
2. Place in `%LOCALAPPDATA%/gogcli/gog.exe`
3. Run `gog.exe auth login`

The extension auto-detects the binary path per platform. After login, calendar events appear automatically in the sidebar.

## Platform Support

| Platform | Status |
|----------|--------|
| Windows (x64) | Supported |
| macOS (Intel) | Supported |
| macOS (Apple Silicon) | Supported |
| Linux (x64) | Supported |

Pure JavaScript — no native dependencies, works on all platforms.

## License

MIT
