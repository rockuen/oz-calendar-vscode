# Changelog

## [1.4.5] - 2026-06-13

### Changed
- `openMarkdownIn: editor` now opens files through VS Code's **default editor association** (`vscode.open`) instead of forcing the built-in text editor. Custom editors registered for a file type (e.g. an installed Markdown editor extension) are honored, and any future extension association is respected automatically. `/grep` line jumps still apply when a file opens in a text editor; open failures fall back to the OS default app.

## [1.4.4] - 2026-05-28

### Added
- **One-click gogcli setup** from the sidebar. When gogcli is missing the panel now offers three actions instead of a bare GitHub link:
  - `🚀 자동 설치` — downloads the matching release asset from [openclaw/gogcli](https://github.com/openclaw/gogcli) for the current platform/arch, extracts it, drops `gog`/`gog.exe` into a standard location, and prompts to run `gog auth login`. Backed by the new command `ozCalendar.installGogcli`.
  - `📁 경로 지정` — opens a file picker so users who already have gogcli installed elsewhere can register it. Backed by the new command `ozCalendar.setGogPath` and the new setting `ozCalendar.gogPath`.
  - `📖 가이드` — opens the upstream gogcli README.
- New setting `ozCalendar.gogPath` (string, empty by default). When set, overrides automatic binary detection.
- Configuration change listener: editing `ozCalendar.gogPath` invalidates the gogcli detection cache and refreshes the sidebar immediately.

### Changed
- gogcli binary detection is now dynamic (`resolveGogPath()`), checking `ozCalendar.gogPath` first, then a per-platform candidate list (`/opt/homebrew/bin`, `/usr/local/bin`, `~/.gogcli/bin`, `%LOCALAPPDATA%\gogcli\gog.exe`). Network calls cap redirects and time out, and release asset names are validated before download.

### Fixed
- Upstream gogcli repository URL corrected to `openclaw/gogcli` across README, INSTALL guide, and the sidebar guide link (was a placeholder).

## [1.4.3] - 2026-05-07

### Added
- **`Calendar: 단축키 변경` command + status bar tooltip link.** VSCode does not let an extension dynamically register a keybinding entered into its `settings.json` — keybindings are manifest-only. Instead, this release adds a one-click path to the *standard* Keyboard Shortcuts editor, pre-filtered to this extension. Two surfaces:
  - Command Palette (`Ctrl+Shift+P` → `Calendar: 단축키 변경`).
  - Status bar `$(calendar) Calendar` tooltip — now a markdown tooltip with a `$(keyboard) 단축키 변경하기` link. Hover the icon and click straight through to the rebind page.
- New command id: `ozCalendar.changeShortcut`.

### Changed
- Status bar tooltip now reads the actual current shortcut (`Ctrl+Shift+B` on Win/Linux, `Cmd+Shift+B` on Mac) instead of the stale `Ctrl+Alt+B` text that was left over after the v1.4.2 keybinding move. README "Keyboard Shortcuts" table updated to match, with a build-task collision note + new "Customize Shortcut" section pointing at the new command.

## [1.4.2] - 2026-05-07

### Changed
- **Calendar focus shortcut moved to `Ctrl+Shift+B` / `Cmd+Shift+B`** (was `Ctrl+Alt+B` / `Cmd+Alt+B`). Note this collides with VSCode's default *Run Build Task* binding — workflows that don't use build tasks gain a more reachable shortcut; workflows that do can override the keybinding back via user `keybindings.json`.

## [1.4.1] - 2026-04-27

### Fixed
- Date extraction now matches 8-digit `YYYYMMDD` pattern anywhere in filename (e.g. `report_20260427.csv`, `매출현황_20260427.xlsx`)
- Previously only 6-digit `YYMMDD` at filename start or hyphenated `YYYY-MM-DD` anywhere were matched
- Adjacent-digit boundary check prevents false positives on arbitrary numeric strings (e.g. `2026042712345.csv` → no match)
- Match priority: `YYYY-MM-DD` (ISO) > `YYYYMMDD` (8-digit, anywhere) > `YYMMDD` (6-digit, filename start)

## [1.4.0] - 2026-04-07

### Added
- Right-click context menu **Delete File** option on file list
- Confirmation dialog before deletion (modal warning with file path)
- Files are moved to OS trash (recoverable), not permanently deleted
- Toast notification on successful deletion

## [1.3.1] - 2026-03-31

### Fixed
- Date extraction regex: files with underscore separator (e.g. `260330_report.csv`) are now correctly indexed

## [1.2.0] - 2026-03-24

### Changed
- Renamed to DateWise Calendar

## [1.1.0] - 2026-03-24

### Added
- Status bar calendar icon for quick sidebar toggle
- Published to Open VSX Registry

## [1.0.0] - 2026-03-22

### Added
- Monthly calendar UI with 6-week grid, today highlight, weekend colors
- Date-based file indexing (YYMMDD / YYYY-MM-DD filename patterns)
- Color dots for 5 file groups (Notes / Data / Images / Others / Event)
- File list grouped by type with Obsidian integration (md/canvas)
- Google Calendar integration via gogcli (4-calendar filter, monthly fetch)
- Command bar with `/memo`, `/todo`, `/ask`, `/idea`, `/find`, `/grep`
- Slash command autocomplete (Tab / Arrow / Enter)
- Command history (Arrow Up/Down, max 50)
- Date jump (MMDD / YYMMDD / YYYYMMDD)
- Multi-date selection (Ctrl+Click)
- Daily note auto-creation with section-based content insertion
- Keyboard shortcut Ctrl+Alt+B / Cmd+Alt+B for sidebar toggle
- Title bar refresh button for file index + calendar event reload
- Google auth expiry detection with in-sidebar login button
- Cross-platform support (Windows / macOS / Linux)
- VSIX package for manual installation
