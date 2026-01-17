# Scheduled Send for Claude - Prototype Handover Document

**Date:** January 15, 2026
**Prototype Version:** 1.0
**Status:** Interactive prototype complete, design discussions ongoing

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [What We Built](#what-we-built)
3. [Design Journey & Iterations](#design-journey--iterations)
4. [Key Design Decisions](#key-design-decisions)
5. [Current Implementation](#current-implementation)
6. [Open Design Questions](#open-design-questions)
7. [Technical Specifications](#technical-specifications)
8. [Next Steps](#next-steps)

---

## Project Overview

### Problem Statement
When users hit their usage limit in Claude, they face a binary choice: pay now or abandon their thought. There's no option for users who are willing to wait but don't want to lose their train of thought or switch to competitor platforms.

### Solution
Add a third option: **"Schedule for later"** - allows users to queue their message to send automatically when their limit resets, with notification when Claude responds.

### Business Rationale
- **Retention over acquisition**: Keep engaged free users who would otherwise switch to ChatGPT/Gemini
- **Future conversion potential**: Users who stay build habits and may convert later
- **Global expansion**: Serves price-sensitive users in markets where $100-200/month is prohibitive
- **Brand alignment**: Supports Claude's "Keep thinking" promise

---

## What We Built

### Deliverables
1. **Interactive HTML Prototype** (`index.html`)
   - Fully functional click-through prototype
   - Matches Claude's production design system
   - No dependencies, pure HTML/CSS/JavaScript

2. **Product Brief** (provided by user)
   - Complete problem statement and business case
   - Success metrics and technical considerations
   - Edge case handling

3. **Complete User Flow**
   - Normal message sending
   - Usage limit modal with 3 options
   - Scheduled message state
   - Edit mode with save/cancel
   - All state transitions

---

## Design Journey & Iterations

### Phase 1: Initial Concept (Heavy Card Design)
**What we tried:**
- Separate large card component replacing the input area
- Prominent scheduled message display with icon, header, and info box
- Edit/Cancel buttons as primary actions within the card

**Issues identified:**
- Too heavy, didn't match Claude's minimalist philosophy
- Added visual complexity instead of reducing it
- Created a "separate component" feel rather than integrated state

**Reference files:** `01-limit-modal.html`, `02-scheduled-message-card.html`, `03-edit-state.html`

### Phase 2: Minimal Integration
**Evolution:**
- Moved away from separate card to input box transformation
- Explored toolbar placement (above vs. below)
- Discussed where actions should live (inside input vs. status bar)

**Key realizations:**
1. Claude's design philosophy: minimal, contextual, non-intrusive
2. Input box should handle input controls only
3. Status bar naturally describes state AND offers actions
4. Avoid hover-revealed UI (not discoverable)

### Phase 3: Input Box Layout Refinement
**Challenge:** Matching Claude's exact production design

**Iterations:**
1. **Toolbar position**: Initially placed model selector and send button at top-right
   - **Issue**: Screenshot showed all toolbar items at bottom in one horizontal line
   - **Fix**: Moved all controls to bottom of input box

2. **Text box height**: Started with 60px single-line
   - **Issue**: Too short for comfortable multi-line input
   - **Fix**: Increased to 100px with 50px bottom padding for toolbar

3. **Toolbar layout**: Separate bottom toolbar below input
   - **Issue**: Toolbar should be inside the text box
   - **Fix**: Made all toolbar items absolutely positioned within input box
   - **Result**: `[+] [🕐]` on bottom-left, `[Opus 4.5 ▼] [↑]` on bottom-right

### Phase 4: Design System Matching
**Refined details to match Claude production:**
- Border color: `#D4D1CC` (not `#E0DDD8`)
- Border radius: `16px` (not `12px`)
- Font: Inter (Claude's actual font, not ABC Whyte)
- Focus state: `#C0BCB7` (subtle, not orange)
- Padding: `16px` with `50px` bottom for toolbar
- Min height: `100px` for comfortable typing

---

## Key Design Decisions

### 1. Edit/Cancel Action Placement
**Current discussion: Where should Edit/Cancel actions live?**

#### Option A: Status Bar Only (Recommended)
```
┌──────────────────────────────────────────┐
│ Can you help me create...                │ (grayed)
│                                           │
│ [+] [🕐]              [Opus 4.5 ▼] [⏰]  │
└──────────────────────────────────────────┘
⏰ Scheduled for 9:00 PM (in 2h 15m) · Edit · Cancel
```

**Pros:**
- Cleanest, most minimal
- Status bar naturally describes state and offers actions
- Input box stays focused on input controls
- Follows Claude's "always visible" over "hover magic" principle

**Cons:**
- Actions below the fold (user must look down)

#### Option B: Inside Text Box (Alternative)
```
┌──────────────────────────────────────────┐
│ Can you help me create...                │
│                                           │
│ [+] [🕐] Edit Cancel  [Opus 4.5 ▼] [⏰] │
└──────────────────────────────────────────┘
⏰ Scheduled for 9:00 PM (in 2h 15m)
```

**Pros:**
- Actions immediately visible with the message
- Everything in one place

**Cons:**
- Clutters input box
- Mixes input controls with state actions
- Less minimal

#### Option C: Hover-Revealed Edit Button
Edit button appears on hover in bottom-right corner

**Pros:**
- Ultra-clean when not hovering
- Familiar pattern from messaging apps

**Cons:**
- Not discoverable (users might not find it)
- Doesn't follow Claude's "always visible" principle
- Mobile doesn't support hover

**Recommendation:** Option A (Status bar) - most aligned with Claude's design philosophy

### 2. Button State Transitions
**Decision: Use contextual button icons**

States:
- **Normal**: Arrow `↑` (send message)
- **Scheduled**: Clock `⏰` (disabled, visual indicator)
- **Editing**: Checkmark `✓` (save changes)

**Rationale:**
- Minimal - no separate Save button needed
- Clear - icon communicates state and action
- Consistent - follows established pattern

### 3. Status Message Format
**Decision: Show both absolute and relative time**

Format: `⏰ Scheduled for 9:00 PM (in 2h 15m)`

**Rationale:**
- Absolute time (9:00 PM) = concrete, lets users plan
- Relative time (2h 15m) = immediate context
- Both serve different mental models

### 4. Visual State Indication
**Decision: Gray out text when scheduled**

- Read-only state: `color: #999` + `cursor: default` + `background: #FAFAF9`
- Edit state: Normal color + active cursor + border highlight

**Rationale:**
- Familiar pattern (like disabled inputs)
- Clearly signals "queued, not active"
- Content remains readable

### 5. Toolbar Preservation
**Decision: Keep all toolbar items intact in all states**

- `[+]` attachment
- `[🕐]` history
- `[Opus 4.5 ▼]` model selector
- `[↑/⏰/✓]` contextual action button

**Rationale:**
- User might want to add attachments while editing
- Model selection still relevant
- Don't hide functionality based on state

---

## Current Implementation

### File Structure
```
scheduled_send_claude/
├── index.html              # Main interactive prototype
├── 01-limit-modal.html     # Original modal design (legacy)
├── 02-scheduled-message-card.html  # Card design (legacy)
├── 03-edit-state.html      # Edit state design (legacy)
├── 04-notification.html    # Push notification mockups
└── 05-complete-flow.html   # Overview page (legacy)
```

**Note:** Files 01-05 are from the initial heavy card design. `index.html` is the current minimal implementation.

### User Flow (Current)

1. **Welcome State**
   - "Wen returns!" greeting
   - Empty input box with "Type / for commands" placeholder

2. **Normal Conversation**
   - User types and sends message
   - Chat interface shows user/assistant messages
   - Usage banner visible: "Usage limit reached • Resets 9:00 PM • limits shared with Claude Code"

3. **Hit Limit Modal**
   - Triggered by clicking "Keep working" button
   - Three options presented:
     - Pay per message
     - Upgrade to higher plan
     - **Schedule for later** (highlighted)

4. **Scheduled State**
   - Input box shows queued message (grayed text, read-only)
   - Send button changes to clock icon `⏰` (disabled)
   - Status bar shows: `⏰ Scheduled for 9:00 PM (in 2h 15m) · Edit · Cancel`
   - All toolbar items remain visible and functional

5. **Edit State**
   - Click "Edit" in status bar
   - Input becomes editable with highlighted border
   - Clock icon changes to checkmark `✓`
   - Status bar shows: `✏️ Editing · Cancel`

6. **Save Changes**
   - Click checkmark or press Enter
   - Returns to scheduled state with updated message

7. **Cancel Schedule**
   - Click "Cancel" (confirmation dialog appears)
   - Returns to normal empty input state
   - All scheduled data cleared

### Technical Implementation

**State Management:**
```javascript
let currentMessage = '';
let scheduledMessage = '';
let isScheduled = false;
let isEditingSchedule = false;
```

**Key Functions:**
- `handleSendClick()` - Routes to send or save based on state
- `showScheduledState()` - Transitions to scheduled read-only
- `saveScheduledEdit()` - Saves edits and returns to scheduled
- `cancelScheduleBtn` - Clears schedule and resets

**CSS Classes:**
- `.input-box` - Base input styling
- `.input-box.scheduled-readonly` - Grayed, disabled state
- `.input-box.scheduled-editing` - Orange border, active
- `.schedule-status` - Status bar below input
- `.bottom-toolbar` - Left-side toolbar (+ clock)
- `.input-actions` - Right-side toolbar (model, send)

---

## Open Design Questions

### 1. Auto-send Behavior
**Question:** What happens when the limit actually resets?

**Options:**
- A) Message sends immediately, Claude responds, user gets notification
- B) User gets notification that message is about to send (last chance to cancel)
- C) Message sends but user must return to see response (no notification)

**Recommendation:** Option A - matches "automatic" promise in feature description

### 2. Multiple Scheduled Messages
**Question:** Can users schedule messages in multiple conversations?

**Current:** One message per conversation (product brief constraint)

**Consideration:** Should we show an indicator if other conversations have scheduled messages?

### 3. Incognito Mode
**Question:** How to handle when user is in incognito mode?

**Decision from brief:** Feature not available in incognito (requires server persistence)

**UX question:** Should we:
- Hide the "Schedule for later" option entirely?
- Show it but disable with explanation tooltip?
- Show modal explaining why it's not available?

### 4. Notification Design
**Question:** What should the notification look like?

**Current:** Multiple mockups in `04-notification.html`
- macOS style (full notification with actions)
- Windows style
- Compact banner

**Decision needed:** Which style for different platforms?

### 5. Message Edit During Queue
**Question:** What happens if user is editing when limit resets?

**From brief:** "Send last saved version if user editing when limit resets"

**UX question:** Should we:
- Silently send last saved version?
- Show a toast notification: "Your message was sent while you were editing"?
- Interrupt edit with modal asking to send or continue editing?

### 6. Failed Send Handling
**Question:** What if auto-send fails (network error, server error)?

**Options:**
- A) Retry with exponential backoff, notify user if persistent failure
- B) Keep in queue, show error state, let user manually retry
- C) Save as draft, let user choose to resend or discard

**Consideration:** Should failed messages stay visible in the input box?

### 7. Timezone Handling
**Question:** How to display scheduled time for users in different timezones?

**Current:** Shows "9:00 PM" but doesn't specify timezone

**Options:**
- Show user's local time always
- Show time with timezone abbreviation "9:00 PM GMT+8"
- Show countdown only, hide absolute time

---

## Technical Specifications

### Design System Values

**Colors:**
```css
/* Backgrounds */
--bg-primary: #FAF9F6;
--bg-white: #FFFFFF;
--bg-hover: #F5F5F5;
--bg-scheduled: #FAFAF9;

/* Text */
--text-primary: #1F1F1F;
--text-secondary: #666;
--text-disabled: #999;

/* Borders */
--border-default: #D4D1CC;
--border-focus: #C0BCB7;
--border-scheduled: #E8CFBB;

/* Brand */
--accent-orange: #D97757;
--accent-orange-hover: #C66846;

/* Usage Banner */
--banner-bg: #F5EDE4;
--banner-text: #5C4A3A;
--banner-dot: #D97757;
```

**Typography:**
```css
font-family: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
font-size: 15px (body text)
font-size: 13px (secondary/meta text)
line-height: 1.5
```

**Spacing:**
```css
/* Input box */
padding: 16px 16px 50px 16px;
min-height: 100px;
border-radius: 16px;

/* Toolbar */
bottom: 12px;
left: 12px (left toolbar)
right: 12px (right toolbar)
gap: 8px (between buttons)

/* Button sizes */
width: 32px; height: 32px; (send button)
padding: 6px 10px (model selector)
border-radius: 6px (buttons)
```

**Transitions:**
```css
transition: border-color 0.15s;
transition: background 0.2s;
transition: opacity 0.2s;
```

### Browser Compatibility
- Modern browsers (Chrome, Firefox, Safari, Edge)
- Uses CSS Grid, Flexbox, absolute positioning
- SVG icons (inline)
- No external dependencies

### Performance
- Single HTML file: ~30KB
- No network requests (except Google Fonts)
- Minimal JavaScript: ~100 lines
- No build process required

---

## Design Principles Applied

### 1. Minimalism
- No unnecessary UI elements
- Input box transforms state instead of adding components
- Actions live in status bar, not cluttering main area

### 2. Contextual Clarity
- Button icon changes based on state (arrow → clock → checkmark)
- Gray text clearly indicates "queued" state
- Status bar provides context: what's happening, when, and what you can do

### 3. Familiar Patterns
- Grayed read-only text = standard disabled pattern
- Status bar = familiar from messaging apps (WhatsApp, Telegram)
- Edit/Cancel actions = standard editing pattern

### 4. Non-intrusive
- Scheduled message stays in input box (where user expects it)
- No modals after scheduling (except initial choice)
- Notification only when response is ready (not when sending)

### 5. Keep Thinking
- Message is preserved, not lost
- User can refine while waiting
- Auto-send removes friction (don't need to remember to return)

---

## Success Metrics (from Product Brief)

### P0 - Critical
- **Completion rate**: >95% of scheduled messages successfully send and receive response

### P1 - Important
- **Schedule adoption**: 15-25% of limit-hit users choose "Schedule for later"
- **Return rate**: >70% of users return to view response

### P2 - Monitoring
- **Conversion impact**: No significant decrease in Max/Pay-per-use conversion
- **Abuse patterns**: Flag queue farming or rapid schedule/cancel cycling

---

## Edge Cases Considered

### From Product Brief
1. **Conversation deleted while queued** → Cancel send, discard message
2. **User upgrades while queued** → Send immediately (no need to wait)
3. **Network failure on send** → Retry with backoff, notify if persistent failure
4. **Limit resets early** → Send immediately
5. **User editing when limit resets** → Send last saved version

### Additional Considerations
6. **User logs out while message queued** → Message persists (server-side storage)
7. **Browser closed while queued** → Message persists (server-side storage)
8. **Multiple devices** → Scheduled message visible across all devices
9. **Message contains attachments** → Not supported in v1 (text only per brief)
10. **Very long messages** → Text area auto-expands, toolbar stays at bottom

---

## Next Steps

### Before Implementation
1. **Finalize Edit/Cancel placement** - Decide on status bar vs. in-box approach
2. **Design notification experience** - Platform-specific or unified?
3. **Define error states** - What happens when things go wrong?
4. **Test on mobile** - Current design is desktop-focused

### Implementation Phase
1. **Backend API design**
   - POST /schedule-message (queue message)
   - PUT /schedule-message/:id (edit queued message)
   - DELETE /schedule-message/:id (cancel schedule)
   - GET /schedule-messages (fetch user's queued messages)

2. **Database schema**
   ```
   scheduled_messages:
     - id
     - user_id
     - conversation_id
     - message_content
     - scheduled_for (timestamp)
     - created_at
     - updated_at
     - status (queued, sent, failed, cancelled)
   ```

3. **Cron job / scheduler**
   - Check for messages where scheduled_for <= now
   - Send messages automatically
   - Handle failures with retry logic

4. **Notification system**
   - Integrate with existing notification infrastructure
   - Send when Claude response is complete (not when message sends)

5. **Frontend integration**
   - Adapt prototype to production React/Vue components
   - Add loading states, error states
   - Implement real API calls
   - Add analytics tracking

### Post-Launch
1. **Monitor metrics** - Track adoption, completion, return rates
2. **Gather feedback** - User surveys, support tickets
3. **Iterate on UX** - Based on real usage patterns
4. **Consider v2 features**:
   - Multiple queued messages per conversation
   - Attachment support
   - Proactive scheduling (before hitting limit)
   - Scheduled message management page

---

## Files Reference

### Current Implementation
- **index.html** - Main interactive prototype (use this)

### Legacy Designs (Initial exploration)
- **01-limit-modal.html** - Modal with 3 options
- **02-scheduled-message-card.html** - Heavy card design
- **03-edit-state.html** - Card edit state
- **04-notification.html** - Notification mockups
- **05-complete-flow.html** - Overview page with timeline

### Documentation
- **Product brief** (provided separately) - Full business case and requirements
- **HANDOVER.md** (this document) - Design journey and decisions

---

## Questions for Product/Engineering

1. **Server-side persistence**: Which storage system? Redis queue vs database?
2. **Notification delivery**: Push notifications, email, or in-app only?
3. **Rate limiting**: Can users abuse by repeatedly scheduling/canceling?
4. **Analytics**: Which events should we track?
5. **A/B testing**: Test different copy/positioning for "Schedule for later" option?
6. **International markets**: Which countries to launch first?
7. **Model selection**: Does scheduled message lock model, or use current default when sent?
8. **Context preservation**: How much conversation context to include when auto-sending?

---

## Contact & Context

This prototype was developed through iterative design discussions focused on:
- Matching Claude's exact production design system
- Following Claude's minimalist design philosophy
- Balancing feature discoverability with visual simplicity
- Exploring multiple approaches before converging on final design

For questions about design decisions, rationale, or alternative approaches explored, refer to the conversation history where each iteration was discussed in detail.

---

**Last Updated:** January 15, 2026
**Status:** Prototype complete, awaiting final design decisions on action placement
**Next Review:** Product team sync on edit/cancel UX and notification design
