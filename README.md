# Claude Scheduled Send - Interactive Prototype

An interactive UI prototype exploring a "scheduled send" feature for Claude. When users hit their usage limits, they could queue messages to send automatically when limits reset.

**[Live Demo](https://whoats.github.io/claude-scheduled-send/)** *(update with your actual URL)*

## The Concept

When users reach their Claude usage limit, they currently have two options: wait or pay more. This prototype explores a third option — **schedule for later**.

Instead of losing their train of thought, users could:
- Queue their message to send when limits reset
- Edit or cancel scheduled messages
- Get notified when Claude responds

For the full product rationale, see the **[Product Brief](PRODUCT_BRIEF.md)**.

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

## Disclaimer

This is an independent project, not affiliated with or endorsed by Anthropic. The prototype and product brief were created as a design exploration—an exercise in imagining how a "scheduled send" feature might work and what product considerations would shape its design. No insider knowledge, just curiosity about a problem worth solving.

## License

MIT
