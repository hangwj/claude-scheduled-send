# Claude Scheduled Send - Interactive Prototype

An interactive HTML prototype exploring a "Schedule for Later" feature for Claude when users hit their usage limits.

## Overview

When users reach their plan's message limit, instead of only offering "pay now or wait", this feature adds a third option: **queue the message to send automatically when the limit resets**.

## Quick Start

Open `index.html` in your browser to interact with the prototype.

## What's in this repo

| File | Description |
|------|-------------|
| `index.html` | Main interactive prototype - click through the full user flow |
| `HANDOVER.md` | Detailed design documentation, decisions, and specifications |
| `screens_claude/` | Reference screenshots of Claude's current limit states |

## User Flow

1. User sends a message → hits usage limit
2. Modal appears with 3 options: Pay per message, Upgrade, or **Schedule for later**
3. Choosing "Schedule" queues the message with visual feedback
4. User can **Edit** or **Cancel** the scheduled message
5. Message auto-sends when limit resets, user gets notified when Claude responds

## Design Highlights

- Minimal UI - input box transforms state instead of adding components
- Status bar shows schedule info with Edit/Cancel actions
- Button icon changes contextually: `↑` send → `⏰` scheduled → `✓` save edit

## License

MIT

