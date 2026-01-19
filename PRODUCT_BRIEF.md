# Scheduled Send for Claude
## Product Brief: Never Stop Thinking

---

## Problem Statement

When users hit their usage limit, they face a binary choice: pay now or abandon their thought. The current experience offers Subscribe to Max ($100-200/month) or Pay-per-usage.

**The gap**: Users who are willing to wait but don't want to lose their train of thought or switch platforms to continue their work.

**Current state**: Claude shows a limit banner with reset time. If users try to send, a modal prompts upgrade options. There's no way to preserve their message for later.

---

## Why This Matters

### The Monetization Concern

This feature gives users a free alternative to paying. Doesn't that undercut revenue?

**Not necessarily—because this segment is unlikely to convert in the moment.**

| User Type | Current Behavior | With Scheduled Send |
|-----------|------------------|---------------------|
| Will pay | Hits limit → upgrades | No change—they still pay |
| Won't pay, high intent | Hits limit → switches to ChatGPT/Gemini | Retained, potential future conversion |
| Won't pay, low intent | Hits limit → switches or abandons | No change—not engaged anyway |

The middle segment is the opportunity. These users are price-sensitive—Max at $100-200/month is prohibitive, especially outside US markets. They want to keep using Claude but hit a wall.

**The business case:**

1. **Retention > acquisition**: Keeping engaged free users costs less than acquiring new ones
2. **Lifetime value**: Users who stay 12 months and eventually convert beat those who churn at month 1
3. **Global expansion**: Pricing reasonable in San Francisco is prohibitive in Malaysia, Brazil, or Poland

**The risk of NOT doing this:**

Users who hit the limit switch to ChatGPT or Gemini to continue their work. This is particularly damaging because:

- **Context loss**: Users re-establish context on competitor platforms—frustrating, but they do it to finish their task
- **Memory advantage erodes**: Claude's conversation history is a retention moat. Forcing users elsewhere undermines it
- **Habit formation**: Users build workflows across multiple platforms; Claude becomes "one of several"

### Brand Alignment

Claude's tagline is **"Keep thinking"**—a thinking partner for problem solvers who can't let go of an idea.

> "Claude is for those who see AI not as a shortcut, but as a thinking partner to take on their most meaningful challenges."

Hitting a limit forces thinking to stop. Scheduled Send turns a hard stop into a pause—aligning product behavior with brand promise.

---

## Target Segment

Free and Pro users who hit limits regularly but don't convert to Max.

**Characteristics:**
- Price-sensitive (Max is a significant commitment, especially outside US)
- High-intent (want to continue, can't afford to right now)
- Global users where USD pricing is prohibitive

**Behavioral signal**: Users who dismiss the upgrade modal and switch to competitor platforms to finish their task.

---

## Solution Overview

Add a third option to the usage limit modal: **"Schedule for later"**

When selected:
- Message is queued and saved
- Scheduled message appears in chat with a "Scheduled" badge
- Message auto-sends immediately when limit resets
- User receives notification when Claude's response is ready

### Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Entry point | Add to existing limit modal | Peer to existing options |
| Queue limit | One message per conversation | Prevents complexity and abuse |
| Queue visibility | Appears as message in chat with badge | Contextual, clear, matches existing message pattern |
| Send trigger | Auto-send on limit reset | Preserves intent without requiring return |
| Notification | On response complete | Value is the response |
| Edit/Cancel | Inline editing | Native to chat context |

### User Flow

1. User hits limit → modal with "Schedule for later" option
2. User selects → scheduled message appears in chat with badge
3. User can edit or cancel while waiting
4. Limit resets → message auto-sends
5. Claude responds → push notification sent
6. User returns to completed conversation

---

## Edge Cases

| Scenario | Handling |
|----------|----------|
| Conversation deleted while queued | Cancel send, discard message |
| User upgrades while queued | Send immediately |
| Network failure on send | Retry with backoff; notify if persistent |
| Limit resets early | Send immediately |
| User logs out while queued | Message persists (server-side) |
| Multiple devices | Scheduled message visible across all |

---

## Success Metrics

| Priority | Metric | Description | Target |
|----------|--------|-------------|--------|
| **P0** | Completion rate | % of scheduled messages that send and receive response | >95% |
| **P1** | Schedule adoption | % of limit-hit users who choose "Schedule" | 15-25% of non-converters |
| **P2** | Return rate | % of users who return to view response | >70% |
| **Monitoring** | Conversion impact | Change in Max/Pay-per-use conversion rate | No significant decrease |
| **Guardrail** | Abuse patterns | Queue farming, rapid schedule/cancel cycling | Flag if detected |

---

## Questions & Answers

**Q: Why not just let users queue unlimited messages?**
A: One message per conversation prevents abuse and keeps the feature simple. *Note: The current prototype supports unlimited scheduled messages for demo purposes. V1 implementation should enforce one message per conversation.*

**Q: Does this work for incognito chats?**
A: No. Requires server-side persistence. Incognito chats are not stored.

**Q: What happens to scheduled messages if a user upgrades mid-wait?**
A: The message sends immediately.

**Q: Could this replace Pay-per-usage for some users?**
A: Possibly for low-volume users. But Pay-per-usage serves immediate needs; Scheduled Send requires waiting.

**Q: How do we know this won't cannibalize Max subscriptions?**
A: Monitor conversion rates post-launch. Hypothesis: users choosing "Schedule" are those who would have switched to competitors.

**Q: What about timezone handling?**
A: Show user's local time. Format: "9:00 PM" or with timezone "9:00 PM GMT+8".

**Q: Does scheduled message lock the model selection?**
A: TBD - either lock at schedule time or use current default when sent.

## Disclaimer

This is an independent project, not affiliated with or endorsed by Anthropic. The prototype and product brief were created as a design exploration—an exercise in imagining how a "scheduled send" feature might work and what product considerations would shape its design. No insider knowledge, just curiosity about a problem worth solving.

---

*v1.0 | January 2025*

---


