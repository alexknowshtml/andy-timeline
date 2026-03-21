# Week 12: Discord Conversations & Personal Archives (Days 97-103)

**January 6-12, 2026** | [← Previous: Week 11](./week-11-days-90-96.md) | [Next: Week 13 →](./week-13-days-104-110.md)

> **Previously:** WebSocket consolidation unified real-time communication. The UniFi Network Tracker launched for physical presence detection. Skills architecture matured with @skill autocomplete in chat. The PM Agent introduced Discord-based human-in-the-loop approvals with button-click-to-spawn workflow.

---

## Overview: @Andy Discord Conversations, Langfuse Observability, and Memory Preservation

Week 12 brought a major interaction paradigm shift: **@Andy Discord mentions** created a new way to interact with Claude through threaded Discord conversations. The **Langfuse integration** added production observability for Claude Code sessions. Personal memory preservation arrived with the **Flickr archive browser**, making 15+ years of photos searchable. The week also saw the **milestone Day 100**, continued UDM health monitoring refinements, and newsletter workflow improvements.

**Key themes:** @Andy Discord mentions with thread conversations, Langfuse tracing for observability, Flickr archive preservation, UDM health monitoring, agreement automation, skill extractions from real work (mac-app-dev, andy-h-domain-setup).

---

## Day 97: Newsletter Ship & Meeting Prep (January 6, 2026)

**Commits: 40**

### Newsletter Final Push

You finalized the weekly newsletter with `broadcast_id 22429983`, marking another consistent edition shipped. The process included moving action items up in meeting summaries and preparing the Adam 1:1 agenda for the following week.

### Session State Fixes

**Commits `d53f6e77a`, `48e24753c`**

Early tool_start detection improved UI feedback timing. Preview page safe area fixes addressed PWA mode display issues. Small polish items that compound into a smoother experience.

**Lesson Learned:** Newsletter consistency builds subscriber trust. The rhythm of weekly shipping matters more than any single edition's content.

---

## Day 98: Network Tracker Containerization & Dual Memory Search (January 7, 2026)

**Commits: 28**

### Network Tracker Goes to Docker

**Commit `e7661cb0d`**

The Network Tracker service moved into a container, making deployment consistent with other services. The backfill job also got scheduled for regular presence data updates.

### Dual Search for Memory Retrieval

**Commits `7fd8f4789`, `94a5e5af1`**

Memory retrieval gained a dual search mode with `searchSource` tracking - combining keyword and semantic search approaches. A UI toggle in the debug panel lets you switch between modes, making it easier to understand how memories are being surfaced.

### BIRT Coalition Coordination

Partnership work continued with BIRT coalition contacts export for ConvertKit integration, plus meeting notes from the working session.

### Healing Home Care Project Agreement

**Commit `d5483ccee`**

A new event agreement generated for February 7, 2026, with detailed event resources matching the December template.

**Lesson Learned:** Memory retrieval is a multi-strategy problem. Neither keyword nor semantic search alone is sufficient - the combination catches what each misses.

---

## Day 99: Agreement Automation & Track Meet Complete (January 8, 2026)

**Commits: 15**

### /renew-agreement Command

**Commit `73e080446`**

Agreement renewal got its own command, cross-referenced with `/create-agreement`. Philly.rb Q1 2026 agreement (Jan/Feb/Mar) generated with proper page breaks and formatting.

### /website Skill

**Commit `6f90fe5f4`**

A new skill for managing client websites, consolidating common web maintenance tasks into a single reference.

### Track Meet Phase 7 Complete

**Commit `c4d498eee`**

The Track Meet project reached its Polish phase milestone. What started as an experimental feature is now production-ready.

### Mobile UI Improvements

- Horizontal scrolling for tables on mobile
- Disabled swipe-to-change-sessions gesture (was causing accidental navigation)
- Improved error display for API errors including content filtering

**Lesson Learned:** Knowing when a project phase is "done" matters. Track Meet Phase 7 completion freed mental space for other priorities.

---

## Day 100: Mac App Dev & UDM Health Monitor (January 9, 2026)

**Commits: 16**

### 🎯 Day 100 Milestone

100 days of building Andy. From a blank repo to 44+ agents, 112+ skills, and a system that genuinely assists daily work.

### mac-app-dev Skill Extraction

**Commit `aafe3d7a6`**

The Pearsnap screenshot tool development taught enough about native macOS development that it warranted capturing in a skill. Building Mac apps with Swift Package Manager, ScreenCaptureKit, code signing, and deployment - all the gotchas documented for future reference.

### andy-h-domain-setup Skill

**Commit `d40b1ca7e`**

Setting up trackmeet.indyhall.org generated learnings about adding HTTPS domains to the andy-h Fedora server. Another "learn while doing, extract to skill" pattern.

### UDM Health Monitor

**Commits `fdba994bf`, `a27779b44`**

The UniFi Dream Machine health monitor launched as a scheduled job. Initial version checked connectivity, memory, and QUIC errors. Multiple fixes followed for timestamp parsing on busybox and state tracking for transition-only alerts.

### Small Talk Newsletter

Created and published the weekly newsletter draft with memory jogger feature.

**Lesson Learned:** Skills should emerge from real work, not speculative planning. The mac-app-dev skill exists because Pearsnap required learning those things, not because someone thought "we should document Mac development."

---

## Day 101: Discord Rename & YouTube Comments (January 10, 2026)

**Commits: 34**

### Discord Channel Reorganization

**Commit `3aebdd181`**

The `andy-v2` channel renamed to `system-notifications` for clarity. New dedicated channels emerged:
- `#memory-lane` for Memory Catcher notifications
- `#network` for UDM health monitor alerts

Custom avatars added for each service - yellow lightning bolt for Andy, purple brain for Memory Catcher.

### UDM Health Monitor Refinements

**Commits `a645bf912`, `cf21c1f22`, `84f30a789`**

State tracking evolved to only alert on state transitions (not every poll). QUIC error detection fixed for shell escaping. The monitor became quieter - alerting when things change, not when they stay the same.

### YouTube Comments Skill

**Commit `94a2e8b33`**

A new skill for fetching video comments, supporting livestream Q&A planning for upcoming sessions.

### Front CLI

**Commit `1652b6e8f`**

Access to Front (frontapp.com) inboxes for Indy Hall and STB added, enabling programmatic inbox access.

### Overdue Reminder Notifications

**Commits `a98cc4a73`, `7c3b0ad4e`**

Overdue reminder digest notifications now run 3x daily. Batch notifications for 3+ simultaneous reminders prevent notification spam.

**Lesson Learned:** Monitoring systems should alert on transitions, not states. "The system is unhealthy" once is useful; every minute is noise.

---

## Day 102: @Andy Discord Mentions (January 11, 2026)

**Commits: 75** 🔥 (Busiest day of the week)

### @Andy Discord Conversations Launch

**Commits `a8dd9401d`, `40b07e933`, `a571c989f`**

The week's flagship feature: mention @Andy in Discord and get a threaded Claude conversation.

**How it works:**
1. User mentions @Andy in a Discord channel
2. Bot creates a thread, posts "Working..." status
3. Laravel job spawns Claude Code via host-bridge HTTP
4. Claude processes with full agent context
5. Response streams back to thread
6. Further messages in thread continue the conversation

**Key infrastructure:**
- `ProcessDiscordMention` job handles initial mentions
- `ProcessDiscordThreadMessage` handles follow-ups
- `DiscordThread` model tracks conversation state
- Host-bridge server exposes spawn-claude endpoint

### Conversational Awareness System

**Commits `864a3dda2`**

The Discord bridge gained sophisticated conversation management:

- **Busy state tracking:** 👀 react when new message arrives while Claude is processing
- **Pause/resume:** "stop", "wait", "hold on" pauses thread (⏸️ react), kills running Claude process
- **Resume flow:** "go", "continue", "ok" resumes with pending messages
- **Override:** Any other message replaces pending work with new instruction

This isn't just message handling - it's interrupt-driven conversation management.

### Langfuse Observability Integration

**Commits `bfb399668`, `f34f92739`**

Claude Code sessions now trace to Langfuse for production observability:

- `session_start.sh` / `session_end.sh` hooks bracket sessions
- `user_prompt.sh` captures prompts
- `trace.sh` handles the actual tracing logic

The SOP at `sops/integrations/langfuse-observability.md` documents the integration.

### Status Message Evolution

The Discord status messages went through rapid iteration:

1. Started with detailed "Working on: X" messages
2. Added typing indicator while processing
3. Replaced Working message with typing indicator only
4. Added tool activity detection via stream-json
5. Settled on minimal status with real-time tool activity display

**Lesson Learned:** Discord threads are a surprisingly good interface for AI conversations. The platform handles threading, notifications, mobile access, and history - all infrastructure you'd otherwise build yourself.

---

## Day 103: Flickr Archive & Discord Polish (January 12, 2026)

**Commits: 31**

### Flickr Archive Browser

**Commits `3c96e2992`, `8ce8612a2`**

A personal memory preservation project: 15+ years of Flickr photos became searchable:

- `flickr-archive-to-sqlite.py` imports photo metadata into SQLite
- `flickr-upload-to-spaces.py` uploads photos to DigitalOcean Spaces
- `flickr-browser-server.py` serves a web UI for browsing
- `index.html` provides a 667-line browser interface

Photos can now be browsed by date, searched by title/description, and viewed in their original resolution.

### Discord Image Support

**Commits `2aff022be`, `bf3536d8f`**

Discord messages can now include images:

- Images download to temp files for Claude viewing
- Image-only messages (no text) handled gracefully
- Circuit breaker added to prevent crash loops from malformed messages

### Credential Rotation

**Commit `1eac75834`**

The credentials skill gained rotate/update functionality for managing API keys.

### Queue Worker Scaling

**Commits `4e3cb8e56`, `f137f0d87`**

Running 3 queue workers prevents thread blocking when multiple Discord conversations happen simultaneously. Redundant scheduler polling removed.

**Lesson Learned:** Personal archives deserve the same engineering attention as work systems. Searchable access to 15 years of photos has immediate value - finding that photo from a specific trip or event.

---

## Reflection: Week 12

---

### The Mistakes We Made

#### 1. Discord Status Message Churn

**Cost:** Day 102 had multiple commits iterating on status message format: Working → typing indicator → tool activity → minimal format\
**Fix:** Eventually settled on minimal status with tool activity detection\
**Lesson Learned:** Ship something, learn from usage, iterate. The "perfect" status format wasn't obvious until users interacted with it.

#### 2. QUIC Error Detection Shell Issues

**Cost:** UDM health monitor failed to detect errors due to shell escaping\
**Fix:** Fixed regex patterns for busybox compatibility\
**Lesson Learned:** Test monitoring scripts in the actual environment. Dev machine bash != production busybox.

#### 3. Queue Worker Blocking

**Cost:** Single queue worker meant Discord conversations blocked each other\
**Fix:** Scaled to 3 workers\
**Lesson Learned:** Async operations need capacity planning. One worker is fine until two things happen at once.

---

### The Surprising Things

#### 1. Discord as AI Interface Works

**Expected:** Clunky, limited compared to custom chat UI\
**Actual:** Threading, notifications, mobile app, history - all "free" from platform

Discord's existing infrastructure handles problems that would take weeks to build from scratch.

#### 2. Langfuse Integration Was Straightforward

**Expected:** Complex tracing setup\
**Actual:** Four hook scripts and it works

The hook architecture in Claude Code made observability integration almost trivial.

#### 3. Flickr Archive Had Immediate Value

**Expected:** Nice-to-have nostalgia project\
**Actual:** Immediately useful for finding specific photos

"When did we visit that restaurant?" is answered by searchable photo archives.

#### 4. Day 100 Felt Normal

**Expected:** Major milestone celebration\
**Actual:** Another productive day

100 days of building didn't feel like a milestone because the work just... continues. The system keeps growing.

---

### System Statistics

**Development Activity:**
- Total commits: 239 (excluding auto-updates)
- Busiest day: Day 102 (Jan 11) - 75 commits 🔥
- Average commits/day: 34

**New Skills (6):**
- `mac-app-dev` - Native macOS development with Swift
- `andy-h-domain-setup` - HTTPS domain setup on Fedora server
- `youtube-comments` - Fetch video comments for Q&A prep
- `/clip-video` - Transcribe and cut video clips
- `/website` - Client website management
- `/renew-agreement` - Agreement renewal workflow

**New Infrastructure:**
- **@Andy Discord mentions** - Thread-based Claude conversations
- **Langfuse tracing** - Production observability for Claude Code
- **Flickr archive browser** - 15+ years of photos searchable
- **Front CLI** - Programmatic inbox access

**Discord Channels:**
- `#system-notifications` (renamed from andy-v2)
- `#memory-lane` (Memory Catcher)
- `#network` (UDM health)

**Agreements Generated:**
- Philly.rb Q1 2026 (Jan/Feb/Mar)
- Healing Home Care Project (Feb 7)

---

**Next:** Voice interface launch and daily planning workflows → [Week 13: Voice Interface & Daily Planning](./week-13-days-104-110.md)
