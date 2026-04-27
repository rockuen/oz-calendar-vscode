# Changelog

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
