# Claude Scheduled Send - Interactive Prototype

An interactive UI prototype exploring a "scheduled send" feature for Claude. When users hit their usage limits, they could queue messages to send automatically when limits reset.

**[Live Demo](https://whoats.github.io/claude-scheduled-send/)** *(update with your actual URL)*

> **Disclaimer:** This is an unofficial prototype for demonstration purposes only. Not affiliated with Anthropic.

## The Concept

When users reach their Claude usage limit, they currently have two options: wait or pay more. This prototype explores a third option — **schedule for later**.

Instead of losing their train of thought, users could:
- Queue their message to send when limits reset
- Edit or cancel scheduled messages
- Get notified when Claude responds

## Try It Out

1. Open `index.html` in your browser
2. Type a message and hit send
3. The "usage limit" modal appears with options:
   - Pay per message
   - Upgrade plan
   - **Schedule for later** ← the new concept
4. Click "Schedule for later" to see the queued message
5. Hover over the scheduled message to edit, copy, or cancel

## Features Demonstrated

- Scheduled message badge and styling
- Edit scheduled messages inline
- Cancel with confirmation dialog
- Copy message to clipboard

## License

MIT
