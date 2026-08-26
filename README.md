[English](README.md) · [繁體中文](README.zh-TW.md) · [日本語](README.ja.md) · [한국어](README.ko.md)

# Open Agent Usage

Open Agent Usage is a macOS menu bar app that shows how much of your AI coding agent quota you have used. It reads usage from four sources: **Claude Code**, **Codex**, **Gemini**, and **Antigravity**.

All data is read from files that already exist on your Mac. Nothing is uploaded anywhere. The only outbound network connection this app makes is to Gumroad, and only when you activate a Pro license key.

The menu bar shows how many percent of each limit you have used and when it resets, color-coded so you can tell your status at a glance: green at 30% or below, blue at 60% or below, orange at 80% or below, and red above 80%. Click the menu bar icon to open a panel with the account, plan, and usage for each time window, per service.

This repository does not contain the app's source code. Open Agent Usage is proprietary software distributed as a compiled binary; see [License](#license).

## Features

| | Free | Pro |
|---|:---:|:---:|
| Menu bar quota display for all 4 agents | Yes | Yes |
| Light / dark appearance, 11 accent colors | Yes | Yes |
| 4 languages (English, Traditional Chinese, Japanese, Korean) | Yes | Yes |
| Expandable panel with account, plan, and per-window usage | Yes | Yes |
| Session list (see what each Claude Code session is doing, click to jump to it) | No | Yes |
| `open-agent-usage` command-line interface for AI agents | No | Yes |
| Price | Free | US$4.99, one-time |

Every new install gets a 30-day trial with all Pro features unlocked, no account required. After the trial ends, the app keeps working with the Free feature set unless you purchase a Pro license.

## Installation

1. Download the latest `.dmg` (or `.zip`) from [Releases](../../releases/latest).
2. Open the disk image and drag **Open Agent Usage** into your **Applications** folder.
3. This build is **not notarized by Apple**, so macOS Gatekeeper will block the first launch. See below for how to open it.

This is a preview build. A notarized build is planned for a future release; until then, opening the app requires one of the steps below.

### Opening an unnotarized app (main method)

In Finder, **Control-click** the app in your Applications folder, choose **Open**, then click **Open** again in the dialog that appears. You only need to do this once — after that, the app opens normally.

### Alternative: Terminal

```bash
xattr -dr com.apple.quarantine /Applications/OpenAgentUsage.app
```

## Additional Setup

### Claude Code usage needs a bridge script

Claude Code only writes your quota data to the status line's standard input; it does not save that data to a file anywhere. To read it, Open Agent Usage needs a small bridge script installed:

```bash
/Applications/OpenAgentUsage.app/Contents/Resources/scripts/install-claude-bridge.sh
```

The script backs up `~/.claude/settings.json` before making any change. Your existing status line keeps working exactly as before, with no visible change in appearance.

- Check installation status: add `--status`
- Remove the bridge and restore your original settings: add `--uninstall`

### Gemini usage needs Accessibility permission

Open **System Settings → Privacy & Security → Accessibility**, and enable **Open Agent Usage**.

If the Gemini app is not running, the Gemini row in the menu bar panel hides itself automatically.

## Buy Pro

Purchase a Pro license here: **https://playmaker12.gumroad.com/l/openagentusage**

After purchase, Gumroad emails you a license key. Open the app's **Settings → Purchase**, paste the key, and activate. Activation needs an internet connection once to verify the key; after that, Pro features keep working offline.

## System Requirements

- macOS 15 or later
- Apple silicon and Intel Macs (universal binary)

## Report Issues

- Email: aione314159@gmail.com
- Or open a GitHub Issue in this repository

## License

Open Agent Usage is proprietary software. No source code is distributed in this repository.

Copyright (c) 2026 aione. All rights reserved.
