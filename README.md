[English](README.md) · [繁體中文](README.zh-TW.md) · [日本語](README.ja.md) · [한국어](README.ko.md)

# Open Agent Usage

A macOS menu bar app that shows how much of your AI coding agent quota you have used, for **Claude Code**, **Codex**, **Gemini**, and **Antigravity**.

![Menu bar, collapsed](docs/menubar-strip.png)

This is what it looks like most of the time: a small strip in the menu bar with an icon and a percentage per agent.

## Key features

- **All four agents in one strip** — Claude Code, Codex, Gemini, and Antigravity quotas side by side, so you don't have to open four different apps to check what's left.
- **Click a session to jump to it** — the panel lists your recent Claude Code sessions with project, branch, model, and what each one is doing; click one to switch straight to that window. (Pro)
- **Everything stays on your Mac** — usage is read from files that already exist locally, nothing is uploaded. The only exception is a one-time check with Gumroad when you activate a Pro license.
- **Light and dark, either automatic or pinned** — the strip and panel follow macOS appearance by default, or you can force Light or Dark from Settings.
- **Four languages** — English, Traditional Chinese, Japanese, and Korean, switchable instantly with no restart.

## The expanded panel

Click the menu bar icon to open the full panel.

![Expanded panel with numbered callouts](docs/panel-annotated.png)

Project names, terminal commands, and account emails in these screenshots are blurred on purpose, for privacy — it's not a rendering issue.

1. **Quota strip** — all limits side by side: Claude Code's 5-hour and 7-day windows, Codex's usage, each with its own percentage and time to reset. The same row has a light/dark toggle and a settings button on the right.
2. **Session list** — recent Claude Code sessions, showing project, branch, model, how long each has been idle, and what it's currently doing. Click one to switch to that window. A green dot means the session is currently running.
3. **Per-service cards** — the signed-in account, plan, and model for each agent.
4. **One row per limit** — a ring, a percentage, a bar, and the reset time. Color always follows usage: green at 30% or below, blue at 60% or below, orange at 80% or below, red above 80%.

![Panel in dark and light appearance](docs/panel-light-dark.png)

The same panel in dark (left) and light (right) appearance.

## Free vs Pro

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
3. Double-click it. It opens like any other app — the build is signed with a Developer ID certificate and notarized by Apple, so Gatekeeper lets it through with no warning and no workaround.

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

## Settings, page by page

### General

![Settings — General](docs/settings-general.png)

**Launch at login** registers the app as a login item, so the strip is there after a restart. **Refresh interval** is fixed at 60 seconds — the strip only redraws when you actually look at it, so reading more often would not gain you anything. **Updates** shows the installed version, checked against the GitHub releases page with a **Check now** button; the app never installs anything on its own.

### Appearance

![Settings — Appearance](docs/settings-appearance.png)

**Language** takes effect immediately, no restart needed. **Theme** follows macOS by default, or you can pin **Light** or **Dark**. **Text size** (Small / Medium / Large) scales the strip and this settings window together.

![Settings — Appearance, accent colors](docs/settings-appearance-accents.png)

Scrolling down the same page shows **11 accent colors** — from Ocean Blue and Findmo Green to Cherry Blossom, Lavender, Coral, Mint, Amber, Burgundy, Graphite, and Warm Brown. The accent is used for selection, buttons, and the settings icons.

### Dynamic Island

![Settings — Dynamic Island](docs/settings-island.png)

**Show quota on the notch** draws a quota strip that joins the notch of the built-in display, so the notch appears to widen; click it to see the detail. **Expand on hover** opens the detail on hover as well as on click — it's off by default, since a sheet that appears whenever the pointer passes the notch is easy to trigger by accident. **Show time until reset** appends the remaining time after each percentage, for example `51% 1h59m`.

![Settings — Dynamic Island, expanded options](docs/settings-island-expanded.png)

Scrolling down, the **When expanded** section controls what the full panel shows: **List sessions** (recent Claude Code sessions and what each is doing, click one to switch to its window), **Show per-service detail** (a card per service with every limit's own ring, bar, and reset time), and **Show account and model** (the signed-in email and model in use on each service card — worth turning off while recording or presenting).

### Shortcut

![Settings — Shortcut](docs/settings-shortcut.png)

**Enable shortcut** turns on a global key combination that opens and closes the expanded strip from anywhere, without moving the pointer to the notch. Click the key-combination button, then press the keys you want; Escape cancels, and **Reset** restores the default. It's registered through Carbon, which needs no Accessibility permission — it works as soon as the app is installed.

### Permissions

![Settings — Permissions](docs/settings-permissions.png)

**Accessibility** is needed to raise the window a session runs in, and to read Gemini's usage page; click the row to open System Settings. **Input monitoring** is needed for Escape to close the expanded strip — a separate grant from Accessibility, about watching the keyboard rather than driving windows. **Claude statusline bridge** shows whether the bridge script is installed; click to copy the install command. Accessibility is tied to the app's code signature, so an unsigned build loses it every time it is rebuilt — if a session row stops responding, check this page first.

### Purchase

![Settings — Purchase](docs/settings-purchase.png)

The top of the page shows your current license status and, during the trial, how many days are left. Below that, a **Free and Pro** table lists exactly which features are Free (the quota strip) and which are Pro (the session list, and the `open-agent-usage` command-line interface) — when the trial ends, only the Pro-marked items stop working.

![Settings — Purchase, buy and activate](docs/settings-purchase-buy.png)

Scrolling down shows the price (**US$4.99**) and a **Buy on Gumroad** button, plus a field to paste and activate a license key once you have one.

### About

![Settings — About](docs/settings-about.png)

The version number, license (**Proprietary**), system requirement (**macOS 15.0+**), and a data statement (**Read locally only**), plus the developer name and a feedback email with a copy button.

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
