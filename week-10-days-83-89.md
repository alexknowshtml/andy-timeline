# Week 10: Agent Refactoring (Days 83-89)

**December 23-29, 2025** | [← Previous: Week 9](./week-09-days-76-82.md)

> **Previously:** Memory Lane launched with semantic search and "surfaced because" context. The host-bridge service extraction split 1 monolith into 6 focused services. iMessage inbox triage brought text message workflows to parity with email. Two consecutive days hit 91 commits each.

---

## Overview: UI Polish, Agent Architecture, and Proactive Systems

Days 83-89 brought two major themes: **auto-suggest buttons** that reduce friction in the chat UI, and a significant **agent refactoring** of the /overview command. The week also introduced Twitter API integration, sessions-api for historical context, date cadence tracking, and the /interview command for plan deep-dives. Infrastructure work continued with MCP watchdog jobs, iMessage sync refinements, and Streamdown for streaming markdown.

**Key themes:** Auto-suggest buttons, /overview agent migration, Twitter API skill, sessions-api, date night planning system, PWA polish, Streamdown renderer, open source preparation.

---

## Day 83: System Maintenance & MCP Watchdog (December 23, 2025)

**Commits: 187** 🔥

**MCP Watchdog System:**
- `2e481ec3e`: Add MCP watchdog job to Bree scheduler
- `d0d674fb3`: Update job scheduler docs with MCP watchdog (26 total jobs)
- `d57855d60`: Add CPU watchdog to Google Docs MCP wrapper
- `688e80ace`: Revert CPU watchdog from MCP wrapper - broke stdio communication
- Lesson learned: MCP stdio communication is fragile

**Newsletter Send:**
- `329008de0`: Send Indy Hall newsletter for week of Dec 23, 2025
- Full newsletter automation workflow executing reliably

**Podman Cleanup:**
- `a60e27a9b`: Add weekly podman cleanup job (27 total jobs)
- Automated container maintenance

**UI Fixes:**
- `cea1a8697`: Fix inbox indicator to exclude snoozed threads
- `7bf999ce3`: Fix memory usage display to use MemAvailable instead of MemFree
- `a42790351`: Make file paths clickable in reminder detail sheet

**Relationship Simplification:**
- `4325cfc88`: Simplify relationship nudges - remove unused morning/evening options
- Streamlined daily automation

---

## Day 84: Chat-First PWA & iMessage Polish (December 24, 2025)

**Commits: 193** 🔥 (Busiest day of the week)

**Chat-First Loading:**
- `2b45525c4`: Add chat-first PWA loading for faster mobile cold start
- `d029aca21`: Improve chat-first loading: prefetch routes, show sidebar on desktop
- `5fe71ca0f`: Add /new route for starting fresh chat sessions
- `c71c4442f`: Add 'Continue last session' button to /new route empty state
- Mobile app now opens directly to chat, not dashboard

**Synology NAS Documentation:**
- `1c16dde93`: Add Synology NAS documentation and management skill
- `1c0884bff`: Add cert sync script for Synology NAS
- `69f736bbf`: Enable Caddy DNS-01 cert management for Synology NAS
- Complete infrastructure documentation for NAS management

**iMessage Snooze Animations:**
- `5acdcdee9`: Add flip animation to snooze/unsnooze toggle
- `2cd6f95b7`: Polish snooze toggle with Emil Kowalski animation principles
- `1a327eec5`: Add smooth crossfade transition to snooze toggle
- Premium micro-interactions inspired by mobile-first design

**Matrix iMessage Sync:**
- `d439f7d34`: Matrix iMessage sync: date filtering, empty thread fix, scheduler integration
- `630ad0966`: Add --debug-senders flag to Matrix iMessage sync
- More reliable sync with better debugging

**Streamdown Integration:**
- `7f5993074`: Add Streamdown for streaming markdown rendering
- `f00c1e0c0`: Add copy button with haptic feedback to Streamdown code blocks
- Improved chat bubble rendering for streamed content

---

## Day 85: Mobile Polish & Server Restart Detection (December 25, 2025)

**Commits: 141**

**Server Restart Detection:**
- `0eb6bd7c4`: Fix false server restart prompts on session restore
- `c106476a9`: Fix glow corners and false server restart prompts
- `91a98ad92`: Fix false 'server restart' prompts on session restore
- Eliminated annoying false positives in session management

**Session Title UX:**
- `9a92ece15`: Make session title click-to-edit, remove pencil icon
- `8f8e91b46`: Make session title save optimistic
- `07399b357`: Add onBlur auto-save for session title
- `1e0c8479e`: Consolidate session title + timestamp in Memory Lane bar
- Streamlined session management interface

**PWA Refinements:**
- `8f99c777b`: Fix iOS PWA keyboard focus issue on chat open
- `fa2bddacb`: Add micro-interactions for premium UI feel
- `6c5e0bcca`: Improve scroll-to-bottom button positioning and style
- `067dfb441`: Add instant visual feedback when navigating from chat to dashboard
- Continued mobile polish

**iMessage Sync via MCP:**
- `97c1e1a0a`: Update iMessage sync to use MCP server instead of Matrix bridge
- Direct MCP integration for text message sync

---

## Day 86: Auto-Suggest Buttons Launch (December 26, 2025)

**Commits: 130**

**Auto-Suggest Buttons System:**
- `3bcf25561`: Add auto-suggest v1: clickable response buttons for yes/no questions
- `5b4356116`: Add auto-suggest reminder hook and strengthen CLAUDE.md instruction
- `f82977eea`: Switch auto-suggest reminder from Stop to UserPromptSubmit hook
- `29c4047fa`: Persist suggestion buttons across session rebuild and make them purple
- `ca558c245`: Add purple loading indicator for suggestion buttons
- Clickable response buttons reduce friction and make the interface feel responsive

**Lesson Learned:** Small friction multiplies across interactions. Buttons make the assistant feel like it anticipates your needs.

**Slash Commands Updates:**
- `cd430ebb1`: Auto-update andy-core slash-commands.json on new command creation
- `f6eda777a`: Copy full command content instead of just name
- `4660ef3d4`: Add PWA safe areas and click-to-copy for slash commands page
- Dynamic command loading without frontend rebuild

**MobileNav Stability:**
- Multiple fixes for MobileNav position snap during Chat→Dashboard transition
- `be26d397e`: Add aggressive dashboard caching with 24h refresh cycle
- Smooth navigation between views

**Knowledge Keeper Consolidation:**
- `fb9c44c33`: Consolidate knowledge-keeper agent into file-this skill
- Agent archived, functionality preserved in skill

---

## Day 87: Twitter API & Sessions Skill (December 27, 2025)

**Commits: 116**

**Twitter API Integration:**
- `5f5232d98`: Add Twitter API skill using twitter-api-v2
- `4f04a60ef`: Add Twitter MCP server integration
- `fc989386f`: Add rate limit warnings to Twitter skill (100 reads/month)
- `4444ee4bd`: Default timeline/mentions to 1 tweet to conserve rate limits
- Full Twitter integration with rate limit awareness

**Lesson Learned:** When resources are scarce, make costs visible. Rate limit warnings help users appreciate tradeoffs.

**Sessions-API Skill:**
- `e1cc865aa`: Add sessions-api skill for searching Claude session transcripts
- `b67f527db`: Add session_resume intent for auto-invoking sessions-api skill
- `51cc428f1`: Add detailed discussion retrieval workflow to sessions-api skill
- `dc988ba32`: Add session-context-retriever agent for historical context lookup
- Query past conversations by keyword, date range, or files touched

**Lesson Learned:** Session transcripts are a goldmine of context. Making them searchable unlocks institutional memory.

**Date Night Planning System:**
- `4ac2c2cd2`: Add date night tracker from Google Maps takeout
- `e38b78a36`: Convert date night planning from SOP to slash command
- `0094b35ea`: Add date cadence tracking system with proactive nudges
- `9c930bc68`: Track in_progress dates to avoid nagging during active planning
- Proactive date planning with restaurant tracking

**Lesson Learned:** Proactive systems must know when to stay quiet. Don't nag during active planning.

**Memory Quality Improvements:**
- `b50dcf583`: Improve memory recall quality: raise floor to 0.70, boost facts
- `5b1eb54c3`: Add 'fact' memory type for stable personal information
- Better memory relevance filtering

**Datetime Context:**
- `f30fea0db`: Add travel-aware timezone context for Andy Core chat UI
- `ba5827a19`: Inject datetime context only on first message of each session
- Timezone-aware context injection

---

## Day 88: /Overview Agent Migration (December 28, 2025)

**Commits: 89**

**/Overview Command Refactoring:**
- `913a2d213`: Refactor: Extract Knowledge Scanner from overview.md inline prompt
- `bcb7d7f91`: Refactor: Migrate Inbox Coordinator to agent-based overview mode
- `778202716`: Migrate Calendar Coordinator to agent-based overview mode
- `e85b6d578`: Complete Phase 1 agent migration for /overview command
- `62ecf0b33`: Add quality validation results for all migrated agents
- Major architectural shift: inline prompts → registered agents

**Lesson Learned:** Inline prompts are expedient but agents are sustainable. Each agent has its own file, tests, and can be reused across commands.

**Open Source Preparation:**
- `800946b89`: Add open source preparation plan
- `d49fac2bc`: Add /interview slash command for plan deep-dives
- Foundation for sharing Andy's development approach

**Slash Commands Dynamic Loading:**
- `7e2d4a0a5`: Make slash commands load dynamically without frontend rebuild
- `76558d2a2`: Fix copy button to include frontmatter in slash commands
- Hot-reloadable command system

**Model Selection:**
- `848321d14`: Use opus model for audit-quality-review job
- `e1dc93243`: Switch link-healer agent from sonnet to haiku
- Targeted model selection based on task complexity

**TodoPanel Improvements:**
- `a402da28d`: TodoPanel: default to collapsed, show task preview
- `4ce579154`: TodoPanel: show task preview when collapsed, counts always visible
- Better task visibility in UI

---

## Day 89: Draft Queue & Protocol Memory (December 29, 2025)

**Commits: 59** (continuing)

**Draft Queue System:**
- `431fd495c`: Add draft queue system for proactive outbound messages
- `7bda9b0d5`: Add communication patterns for draft templating
- `a7c439cd2`: Remove auto-drafting until we have real examples
- Foundation for proactive message drafting

**Protocol Memory Type:**
- `f2abbcb1f`: Add protocol memory type for always-loaded operational rules
- New memory category for system-critical information

**/Overview Phase 2:**
- `2701f382c`: Phase 2: Add overview-preflight.ts consolidating pre-flight checks
- `dad42806f`: Add Andy Core API proxy rule to agent startup checklist
- Continued agent architecture improvements

---

## Reflection: Week 10

---

### The Mistakes We Made

#### 1. MCP CPU Watchdog Broke Communication

**Cost:** Day 83 commit `d57855d60` added CPU watchdog to MCP wrapper, immediately reverted in `688e80ace`
**Fix:** Reverted within same session after stdio communication failures
**Lesson Learned:** MCP stdio communication is fragile. Don't add middleware that might buffer or delay output.

#### 2. False Server Restart Prompts

**Cost:** Day 85 required 3 commits to fix false "server restart" prompts annoying users
**Fix:** Fixed session restore logic to not trigger restart detection
**Lesson Learned:** Session management edge cases compound into bad UX. Test session restore thoroughly.

#### 3. Twitter API Rate Limits Hit Hard

**Cost:** Day 87 discovered only 100 reads/month on Twitter API free tier
**Fix:** Added rate limit warnings, defaulted to 1 tweet per query, made costs visible
**Lesson Learned:** Always check API pricing/limits before integrating. Free tiers can be surprisingly restrictive.

---

### The Surprising Things

#### 1. Auto-Suggest Buttons Transformed UX

**Expected:** Nice-to-have feature for yes/no questions
**Actual:** Buttons make the assistant feel anticipatory and responsive

The friction reduction multiplied across every interaction. What seemed like a small polish became a defining UX characteristic.

#### 2. 193 Commits on Christmas Eve

**Expected:** Light development day
**Actual:** Day 84 was the busiest day of the week (193 commits)

Chat-first PWA loading, Synology documentation, iMessage animations, and Streamdown all shipped on Dec 24.

#### 3. Session Transcripts As Institutional Memory

**Expected:** Sessions-api would be occasionally useful
**Actual:** Querying past conversations unlocked massive context

Being able to ask "what did we discuss about X last week" changed how context accumulates across sessions.

#### 4. Agent Migration Went Smoothly

**Expected:** /overview refactoring would take multiple days
**Actual:** Phase 1 completed in one day (Day 88), all agents validated

The pattern was clear: extract inline prompt → create agent file → add to registry → validate quality.

---

### System Statistics

**Development Activity:**
- Total commits: 915
- Busiest day: Day 84 (Dec 24) - 193 commits 🔥
- Second busiest: Day 83 (Dec 23) - 187 commits 🔥
- Third busiest: Day 85 (Dec 25) - 141 commits
- Average commits/day: 131

**Auto-Suggest System:**
- Core implementation: 5 commits
- Hook integration: 2 refinements
- Session persistence: 1 commit
- Total: complete system in one day

**Agent Architecture:**
- Agents extracted from /overview: 3 (Knowledge Scanner, Inbox Coordinator, Calendar Coordinator)
- Agents consolidated: 1 (knowledge-keeper → file-this skill)
- Agent quality validations: all passing

**New Skills (3):**
- `twitter-api` - Twitter timeline/mentions with rate limit awareness
- `sessions-api` - Claude session transcript search
- `synology` - NAS management documentation

**New Commands (3):**
- `/new` - Fresh chat session route
- `/date-night` - Date planning with venue tracking
- `/interview` - Plan deep-dive conversations

**PWA Improvements:**
- Chat-first loading for mobile cold start
- Session title click-to-edit
- Scroll-to-bottom button polish
- iOS keyboard focus fix
- Micro-interactions throughout

**Infrastructure:**
- MCP watchdog job added
- Podman weekly cleanup job added
- Streamdown markdown renderer integrated
- Protocol memory type added

---

**Next:** To be continued as development progresses...
