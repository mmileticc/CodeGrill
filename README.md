# CodeGrill (pluginIntelliJ1st)

IntelliJ IDEA plugin that roasts your selected code with AI, turns actionable hints into trackable tasks, and gives you a lightweight productivity side panel.

<!-- Plugin description -->
CodeGrill is an IntelliJ Platform plugin for Kotlin/Java projects that combines AI-powered code roasting with an in-editor TODO workflow.

It can generate short ROAST/HELP/NICE comments for selected code, convert HELP comments into TODO tasks, track TODO vs DONE progress in a dedicated tool window, and provide quick actions from gutter icons.
<!-- Plugin description end -->

## Features

- AI roast for selected code with the `Roast my code` action.
- Adjustable roast intensity: `Low`, `Medium`, `High`.
- Response language switch: `English` or `Serbian (Latin)`.
- Generated comment formats:
	- `// ROAST: ...`
	- `// HELP: ...`
	- `// NICE: ...`
- Comment cleanup actions:
	- Delete all generated comments
	- Delete only NICE comments
	- Delete only ROAST/HELP comments
- TODO workflow integrations:
	- `// HELP` comment can be converted to `// TODO` from gutter icon.
	- `// TODO` comment can be marked as `// DONE` from gutter icon.
	- `Code Tasks` tool window scans project files and shows progress (`DONE / total`).
- Extra tool window: `FocusKeeper9000` with embedded browser controls.

## Compatibility

- IntelliJ Platform: `2024.2+` (`since-build = 242`)
- JVM toolchain: `21`
- Language support wired in plugin config:
	- Java
	- Kotlin (optional dependency)

## Requirements

- JDK `21`
- IntelliJ IDEA `2024.2` or compatible IDE based on IntelliJ Platform
- OpenAI API key available in environment variable:
	- `OPENAI_API_KEY`

## Quick Start (Run Locally)

1. Set OpenAI key (PowerShell):

```powershell
$env:OPENAI_API_KEY="your_key_here"
```

2. Run sandbox IDE:

```powershell
.\gradlew runIde
```

3. In sandbox IDE, open a Kotlin/Java file, select code, then run:
	 - Right click -> `Roast my code`
	 - or shortcut `Ctrl+Alt+Q`

## How To Use

### 1) Roast selected code

- Select a code block.
- Trigger `Roast my code`.
- Plugin sends the prompt to OpenAI and inserts generated comments above the selection.

### 2) Configure roast behavior

From `Tools -> Roast Tools`:

- `Roast level` -> Low / Medium / High
- `Roast language` -> English / Serbian

### 3) Manage generated comments

From `Tools -> Roast Tools -> Delete comments`:

- Delete all generated comments (`Ctrl+Alt+D`)
- Delete only NICE comments
- Delete only ROAST comments

### 4) Turn help into tasks

- Click gutter icon on a `// HELP` line to create `// TODO`.
- Click gutter icon on a `// TODO` line to mark it as `// DONE`.

### 5) Track progress in Code Tasks tool window

- Open `Code Tasks` tool window.
- View completion percentage and task list.
- Filter by:
	- `In progress` (TODO)
	- `Completed` (DONE)
- Double-click task to jump to exact location.

## Toolbar / Tool Windows

- `FocusKeeper9000` action is available in toolbar (`MainToolbarRight`) and `View` menu.
- `FocusKeeper9000` tool window opens embedded browser panel with simple navigation controls.

## Project Structure

```text
src/main/kotlin/com/github/mmileticc/pluginintellij1st/
	OpenAIAPI.kt                 # OpenAI HTTP integration
	roasting/                    # Roast actions, settings, comment cleanup
	comments/                    # Annotator + gutter markers (HELP/TODO/DONE)
	services/TodoScannerService.kt
	toolWindow/                  # Code Tasks + FocusKeeper9000 tool windows
	actions/                     # Toolbar/menu actions
src/main/resources/META-INF/plugin.xml
```

## Development Commands

```powershell
# Run tests
.\gradlew test

# Build plugin artifact
.\gradlew buildPlugin

# Verify plugin against recommended IDEs
.\gradlew verifyPlugin

# Run sandbox IDE
.\gradlew runIde
```

## Notes on OpenAI Integration

- Requests are made to `https://api.openai.com/v1/chat/completions`.
- Current code uses model string: `gpt-5.2`.
- If API call fails, plugin inserts a fallback ROAST/HELP message with error details.

## Security & Privacy

- API key is read from `OPENAI_API_KEY` environment variable.
- Selected code is sent to OpenAI endpoint when roast action is triggered.
- Do not use on sensitive code unless your policy allows external API processing.

## Changelog

See `CHANGELOG.md`.

## License

Add your license file and update this section (for example: MIT, Apache-2.0, etc.).

