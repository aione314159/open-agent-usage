[English](README.md) · [繁體中文](README.zh-TW.md) · [日本語](README.ja.md) · [한국어](README.ko.md)

# Open Agent Usage

Open Agent Usage 是一款 macOS 選單列常駐 App，把你的 AI coding agent 用量配額直接顯示在選單列上。讀取 **Claude Code**、**Codex**、**Gemini**、**Antigravity** 四個來源的用量資料。

所有資料都從你 Mac 上既有的檔案讀取，**不會上傳任何東西**。這個 App 唯一對外的連線是連到 Gumroad，而且只有在你要啟用 Pro 授權碼時才會發生。

選單列會顯示每個限制用掉幾 % 以及何時重置，並用顏色標示：≤30% 綠色、≤60% 藍色、≤80% 橘色、>80% 紅色，一眼就能看出狀態。點選單列圖示可以展開面板，看到每個服務的帳號、方案，以及各個時間窗的用量。

本 repo **不含原始碼**。Open Agent Usage 是專有軟體，以編譯好的執行檔發布；詳見〈[授權](#授權)〉。

## 功能

| | 免費 | Pro |
|---|:---:|:---:|
| 四個 agent 的選單列配額顯示 | 有 | 有 |
| 淺色／深色外觀、11 種強調色 | 有 | 有 |
| 4 種語言（英／繁中／日／韓） | 有 | 有 |
| 展開面板看帳號、方案、各時間窗用量 | 有 | 有 |
| Session 清單（看每個 Claude Code session 在做什麼，點一下切過去） | 無 | 有 |
| `open-agent-usage` 命令列介面，給 AI agent 呼叫 | 無 | 有 |
| 價格 | 免費 | US$4.99，一次買斷 |

每次全新安裝都會啟動 **30 天全功能試用**，不需要註冊帳號。試用期結束後，App 仍可正常使用免費功能，除非你購買 Pro 授權。

## 安裝

1. 從 [Releases](../../releases/latest) 下載最新的 `.dmg`（或 `.zip`）。
2. 打開磁碟映像檔，把 **Open Agent Usage** 拖進 **Applications** 資料夾。
3. 這個版本**尚未經過 Apple 公證**，所以 macOS 的 Gatekeeper 第一次開啟時會擋下來。請看下面的開啟方式。

這是一個預覽版本，之後會推出經過公證的正式版；在那之前，開啟這個 App 需要以下其中一種方式。

### 開啟未公證的 App（主要做法）

在 Finder 裡對 Applications 資料夾中的 App **按住 Control 點一下**，選擇**「打開」**，跳出的對話框再點一次**「打開」**。只需要做一次，之後就可以正常開啟。

### 替代做法：終端機

```bash
xattr -dr com.apple.quarantine /Applications/OpenAgentUsage.app
```

## 額外設定

### Claude Code 的用量需要多裝一個橋接腳本

Claude Code 只會把配額資料寫進 status line 的標準輸入（stdin），不會把它存成任何檔案。Open Agent Usage 要讀到這份資料，需要先安裝一個小型橋接腳本：

```bash
/Applications/OpenAgentUsage.app/Contents/Resources/scripts/install-claude-bridge.sh
```

腳本執行前會先備份 `~/.claude/settings.json`。你原本的 status line 完全照常運作，外觀不會有任何變化。

- 檢查安裝狀態：加上 `--status`
- 移除橋接並還原原本設定：加上 `--uninstall`

### Gemini 的用量需要輔助使用權限

打開**系統設定 → 隱私權與安全性 → 輔助使用**，勾選 **Open Agent Usage**。

Gemini App 沒有在執行時，選單列面板裡的 Gemini 那一列會自動隱藏。

## 購買 Pro

在這裡購買 Pro 授權：**https://playmaker12.gumroad.com/l/openagentusage**

購買後 Gumroad 會用 email 寄給你一組授權碼。打開 App 的**設定 → Purchase**，貼上授權碼並啟用。啟用時需要連網驗證一次，之後 Pro 功能離線也能正常使用。

## 系統需求

- macOS 15 或以上
- 支援 Apple silicon 與 Intel（universal binary）

## 問題回報

- Email：aione314159@gmail.com
- 或在本 repo 開 GitHub Issue

## 授權

Open Agent Usage 是專有軟體，本 repo 不含原始碼。

Copyright (c) 2026 aione. All rights reserved.
