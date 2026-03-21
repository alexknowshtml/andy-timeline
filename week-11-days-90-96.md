# Week 11: Real-Time Infrastructure (Days 90-96)

**December 30, 2025 - January 5, 2026** | [← Previous: Week 10](./week-10-days-83-89.md)

> **Previously:** Auto-suggest buttons launched, making the assistant feel anticipatory. The /overview command migrated to agent-based architecture (3 agents extracted). Twitter API and sessions-api skills enabled new capabilities. Christmas Eve saw 193 commits with chat-first PWA loading and Streamdown markdown renderer.

---

## Overview: WebSocket Consolidation, Network Tracker, and Human-in-the-Loop Automation

Week 11 marked a significant infrastructure evolution. The **WebSocket consolidation** project unified all real-time communication into a single connection, eliminating polling overhead. The **UniFi Network Tracker** emerged as a new service tracking physical presence at Indy Hall. **Skills architecture** matured with proper directory structure and @skill autocomplete in chat. The **PM Agent** introduced Discord-based human-in-the-loop approval for proactive AI operations.

**Key themes:** WebSocket unification, Network Tracker service, skills consolidation, beads issue tracking, dangerous command protection, wine cellar automation, iMessage attachment display, PM Agent with Discord approvals.

---

## Day 90: Skills Consolidation & Sentry Integration (December 30, 2025)

**Commits: 74**

### Skills Architecture Cleanup

You consolidated scattered scripts into proper skills with a consistent directory structure. Key additions:

- `91f73b5cc`: Add podman skill for container management
- `657b08547`: Add git-workflow skill for knowledge-rich commits
- `5d797fe23`: Add pm2 skill for managing long-running services
- `01f2cbc68`: Add scheduled-jobs skill for background automation
- `89994f589`: Add mcp-servers skill and fix suggest-options hook
- `058752e9e`: Add Google Drive/Docs/Sheets skill for gogcli

**Lesson Learned:** Skills that wrap multiple tools (podman, pm2) save context by documenting common operations in one place. The skill becomes the single source of truth.

### Sentry Error Tracking

- `7c79c3461`: Add Sentry error tracking to Andy Core
- `4140bb29d`: Fix Sentry source map uploads by loading env vars in Vite config

Error tracking finally landed in the chat interface. Crashes now surface immediately instead of hiding in logs.

### User Impersonation

- `923856953`: Add user impersonation with Mirror package
- `6d4b9c1ca`: Add safe area insets to impersonation banner
- `0b26e67d4`: Increase impersonation banner offset to 3.5rem

Multi-user foundation work continued with the ability to switch between user contexts for debugging.

### PWA Background Streaming Fixes

- `e9cbbe8d9`: Fix PWA background streaming with polling-based catch-up
- `2cbccae85`: Fix PWA background catch-up with polling and full rebuild
- `63e7bd35f`: Fix catch-up duplicate content by clearing streaming state first

Multiple attempts to fix PWA session restoration when the app resumes from background.

**Lesson Learned:** PWA session recovery is a multi-layered problem. Fixing one layer often reveals issues in the next.

---

## Day 91: Beads Issue Tracker & Dangerous Command Protection (December 31, 2025)

**Commits: 57**

### Beads Issue Tracker Initialization

**Commit `0b03ed20d`**

You initialized the beads issue tracker for the andy repo, bringing persistent issue tracking across Claude Code sessions. Key commits:

- `e0b3b0621`: Move beads instructions from AGENTS.md to CLAUDE.md
- `81d4288e4`: Consolidate Landing the Plane protocol into shared include
- `df1b930f6`: Update pause command to integrate with beads workflow
- `d53f6e12c`: Add /close-epic skill for beads+plan workflow

Beads enables multi-session work continuity - issues persist even when sessions end.

**Lesson Learned:** Session boundaries shouldn't mean lost context. Persistent issue tracking bridges the gap between Claude Code sessions.

### Dangerous Command Modal

**Commits `f3dc74096`, `63a9a75e6`, `78abb458a`**

A safety system emerged for dangerous shell commands:

- PreToolUse hook blocks dangerous commands before execution
- 15-second countdown with auto-proceed for informed decisions
- Integration with the approval flow for user consent

Commands like `rm -rf` now require explicit acknowledgment, reducing accidental damage.

**Lesson Learned:** Friction in the right places prevents disasters. A 15-second countdown is annoying until it saves you from a catastrophic rm -rf.

### Chat Drafts Feature

- `12b8683b8`: Add server-side storage for chat drafts
- `a9be1ce36`: Add save to drafts feature for chat input
- `e63bb4d7e`: Auto-expand drafts section when opening drawer from Load drafts button

Messages can now be saved as drafts and loaded later, useful for composing complex prompts.

### Test Coverage Expansion

- `675081555`: Add Phase 7 console command tests (59 tests, 161 assertions)
- `1bed1c18c`: Add Phase 8 frontend tests with Vitest (169 tests)
- `54b40e635`: Add Phase 8b frontend tests (169 → 420 tests)

Test coverage nearly tripled in one day, from 169 to 420 frontend tests.

**Lesson Learned:** Test coverage compounds. Once the infrastructure exists (Vitest + testing patterns), adding more tests becomes fast.

---

## Day 92: @Skill Autocomplete & Unified Suggestions (January 1, 2026)

**Commits: 66**

### @Skill Mention Autocomplete

**Commits `9b7c2dc9e`, `00d666df8`, `482029122`**

A major UX improvement: typing @ in the chat input now shows skill autocomplete with fuzzy matching:

- `9b7c2dc9e`: Add @skill mention autocomplete to chat UI
- `00d666df8`: Add unified suggestion mode combining commands and skills
- `282387e27`: Add scroll-to-load-more for @skill autocomplete

Skills are now as discoverable as slash commands. The unified suggestion mode makes both patterns feel native.

**Lesson Learned:** Autocomplete isn't just convenience - it's education. Users discover capabilities they didn't know existed.

### /summarize Skill with OpenRouter Free Tier

- `97ede4c5e`: Add /summarize skill with OpenRouter free tier
- `7492f6238`: Add git hook to auto-regenerate skills.json
- `be6697b30`: Add auto-summarization to file-this skill (Phase 3)

Free summarization arrived via OpenRouter, enabling PDF/article extraction without API costs.

### Skills Structure Fixes

- `5392f602b`: Fix 8 skills with wrong structure - move to directories with SKILL.md
- `d3f7ebaa9`: Fix 4 more skills with structure issues
- `228fe5cda`: Fix credentials skill structure - move to directory with SKILL.md

Skills standardized to directory-with-SKILL.md pattern for consistency.

### Home Assistant on Synology NAS

- `dbef11d0a`: Replace Homebridge with Home Assistant on NAS
- `1fd40f146`: Document Home Assistant setup on Synology NAS
- `fa18bec23`: Fix Home Assistant reverse proxy config - HTTP on 9081

Smart home infrastructure migrated from Homebridge to Home Assistant, with full documentation.

### Chat Input History

- `c2b63f7f4`: Add up/down arrow key history recall in chat input

Arrow keys now cycle through previous messages, like a proper terminal.

**Lesson Learned:** Terminal conventions translate well to chat interfaces. Up-arrow for history feels natural.

---

## Day 93: UniFi Network Tracker MVP (January 2, 2026)

**Commits: 50**

### Network Tracker Service Launch

**Commits `ac3490bc9`, `707682b7b`, `f6938ccc0`, `71d03033f`**

A new service emerged tracking who's physically present at Indy Hall via UniFi network data:

- **Phase 1:** UniFi API integration, client listing, device tracking
- **Phase 2:** Discord check-in collector for human-reported presence
- **Phase 3:** Correlation engine matching devices to known owners
- **Phase 4:** Extended API endpoints and network-tracker skill

The service runs on the Mac Mini, polls UniFi every minute, and exposes an API for querying "who's here now."

**Lesson Learned:** Physical presence detection requires multiple data sources. Network devices + Discord check-ins + manual identification creates a complete picture.

### SSH Skill Consolidation

- `9ead2b8d7`: Rename /udm to /ssh-udm and /synology to /ssh-synology
- `f4671ca14`: Rename /mac-mini to /ssh-mini for consistency
- `80ba04486`: Add UniFi API support to /ssh-udm skill

SSH-related skills unified under consistent naming: /ssh-mini, /ssh-udm, /ssh-synology.

### WebSocket Event Migration (Phase 3)

- `6300fa262`: Add event migration to unified WebSocket (Phase 3)
- `7f76eb1a1`: Fix WebSocket auth to accept jfdi-session cookie
- `f668cfd19`: Phase 4: Add WebSocket broadcast for chat streaming events

WebSocket consolidation continued, migrating events from multiple connections to a unified transport.

**Lesson Learned:** WebSocket auth is tricky. Cookie-based auth works better than token headers for browser clients.

---

## Day 94: Network Tracker UI & WebSocket Consolidation (January 3, 2026)

**Commits: 105** 🔥 (Busiest day of the week)

### Network Tracker UI Polish

**Commits `f2512f77f`, `730a972a4`, `c226f92aa`**

The Network Tracker got a full web UI:

- `f2512f77f`: Redesign Network Tracker dashboard with shadcn/Tailwind styling
- `730a972a4`: Add web UI dashboard for Network Tracker
- `c226f92aa`: Enhanced presence dashboard with rich data and interactive controls
- `8af729f6a`: Add People table as primary entity linking devices and check-ins
- `b36d694f6`: Add duplicate person detection and merge functionality
- `a68764413`: Add manual person selection for merging

The dashboard shows who's present, their devices, check-in history, and allows editing device ownership.

**Lesson Learned:** MVP to polished UI in one day is possible when the data model is right. The People table as primary entity unlocked rapid UI iteration.

### Duplicate Person Merge

- `b36d694f6`: Add duplicate person detection and merge functionality
- `6807b58bc`: Improve duplicate merge UX with smart defaults and user choice
- `faf4bd686`: Add person aliases for merged name tracking

People get duplicated when the same person uses different devices or check-in methods. The merge feature consolidates them with alias tracking.

### WebSocket Consolidation (Phases 1-4)

- `d0d6f0090`: Phase 1: Extend WS snapshot with chat state for PWA catch-up
- `540d861d1`: Phase 2: Client-side WS chat state catch-up
- `d57c423d4`: Phase 4c+4d: Add WebSocket transport and chat.send handler
- `25824878b`: Phase 5: Wire WebSocket chat into ChatPanel

Chat now uses WebSocket exclusively instead of SSE + polling. One connection for everything.

**Lesson Learned:** WebSocket consolidation is high-effort but worth it. Single connection = simpler debugging, better mobile battery life, faster reconnection.

### Wine Cellar Catalog

**Commit `279dec1d6`**

A fun side project: 52 bottles cataloged with the /wine skill:

- `279dec1d6`: Add wine cellar catalog with 52 bottles and /wine skill
- `a57f9ee17`: Add rack organization to wine cellar skill and place all 52 bottles

Every bottle photographed, cataloged, and assigned to a rack position.

**Lesson Learned:** Personal data management isn't just for work. A wine database with AI assistance makes finding the right bottle trivial.

---

## Day 95: iMessage Attachments & Reactions (January 4, 2026)

**Commits: 83**

### iMessage Attachment Display

**Commits `aec5ca766`, `8f83ab541`, `ff249862d`**

iMessage inbox gained media support:

- `aec5ca766`: Add iMessage attachment and reaction display in inbox
- `8f83ab541`: Resolve message sender names and add attachment serving
- `ff249862d`: Add HEIC→JPEG conversion support to iMessage attachment upload
- `67df583b0`: Show sender name on tapback reactions
- `2b6d4fab9`: Add Italian tapback patterns and hex identifier group chat detection

Photos, videos, and tapback reactions now display inline. HEIC images auto-convert for web display.

**Lesson Learned:** Messaging display requires locale awareness. Italian tapbacks ("Amato", "Mi piace") needed explicit pattern matching.

### imsg-server Migration

**Commits `2cfb043d0`, `5965ecd62`, `ae53828ce`**

iMessage sync migrated from MCP to a dedicated HTTP server:

- `2cfb043d0`: Switch iMessage sync from MCP to imsg HTTP server
- `ae53828ce`: Add imsg-server source code to andy repo
- `411226213`: Fix split thread bug: consolidate phone-keyed duplicates into name-keyed threads

The imsg-server provides faster, more reliable message sync than the previous MCP-based approach.

### Relationship Freshness Automation

- `b9aafef85`: Speed up freshness updater with parallel TypeScript processing
- `c38da2a3f`: Add fast incremental last_contact updater
- `5b43e016a`: Switch verify-last-contact.py to use gogcli instead of Python Gmail API

Relationship last_contact dates now update automatically with parallel processing.

### PR Review Skill

- `064992d9b`: Add pull-requests-review skill for GitHub PR workflow
- `bf2f3646e`: Add review-pr skill for GitHub PR workflow

GitHub PR workflow now has a dedicated skill for reviewing, cherry-picking, and merging contributions.

**Lesson Learned:** Open source contribution handling needs structure. The PR review skill documents the workflow for messy PRs that need cleanup before merging.

---

## Day 96: PM Agent & Discord Approval Flow (January 5, 2026)

**Commits: 27** (in progress)

### PM Agent with Discord Approvals

**Commits `28c94b85f`, `184cf2711`, `82c0aacb8`**

The PM Agent introduced human-in-the-loop automation:

- `28c94b85f`: Add PM Agent with /pm command and scheduled runs
- `184cf2711`: Add discord-agent-bridge and PM approval webhook infrastructure
- `82c0aacb8`: Complete Discord approval flow: button → webhook → Claude spawn
- `44aa22ab2`: Complete Discord approval system design with all four resolved decisions

The PM Agent reviews projects and tasks, identifies what needs attention, and can spawn follow-up actions. Discord buttons provide the approval interface - click to approve an action, and Claude spawns to execute it.

**Lesson Learned:** Proactive AI needs oversight mechanisms. Discord buttons bridge the gap between "AI suggests" and "human approves."

### WebSocket PWA Fixes

- `f4dc66e35`: Revert chat/WebSocket files to pre-consolidation state
- `7964df554`: Prevent duplicate WebSocket connections by checking CONNECTING state
- `94a7de000`: Fix PWA session state loss when minimizing chat
- `1de8fe6d5`: Fix /new route restoring previous session instead of starting blank

WebSocket consolidation revealed edge cases in PWA session handling. Some changes were reverted to stabilize the experience.

**Lesson Learned:** Aggressive refactoring sometimes needs tactical retreats. Reverting broken changes is faster than debugging under pressure.

---

## Reflection: Week 11

---

### The Mistakes We Made

#### 1. WebSocket Consolidation Complexity

**Cost:** Multiple revert commits (`f4dc66e35`) after WebSocket changes broke PWA session handling\
**Fix:** Tactical revert to pre-consolidation state while debugging continues\
**Lesson Learned:** WebSocket + PWA + session state = complex interaction matrix. Test PWA scenarios specifically, not just desktop browser.

#### 2. Skills Directory Structure Inconsistency

**Cost:** Day 92 required fixing 12 skills with wrong directory structure\
**Fix:** Batch migration to directory-with-SKILL.md pattern\
**Lesson Learned:** Establish conventions before scaling. Early skills used mixed patterns that required cleanup.

#### 3. Network Tracker Duplicate People

**Cost:** Same person appearing multiple times from different devices/check-in sources\
**Fix:** Built duplicate detection and merge functionality\
**Lesson Learned:** Entity resolution is hard. Any system tracking people from multiple sources needs merge capability from day one.

---

### The Surprising Things

#### 1. 420 Frontend Tests in One Day

**Expected:** Gradual test coverage growth\
**Actual:** Day 91 went from 169 to 420 tests in a single session

Once Vitest and testing patterns were established, adding tests became mechanical. The bottleneck was setup, not execution.

#### 2. Wine Cellar Became Useful Fast

**Expected:** Fun side project, rarely used\
**Actual:** Immediate utility for selecting bottles for dinner

Cataloging 52 bottles took an afternoon. Now "what wine pairs with lamb?" returns an actual answer.

#### 3. Network Tracker UI in One Day

**Expected:** MVP API only, UI later\
**Actual:** Full shadcn dashboard with People table, device editing, and filters in Day 94

When the data model is right, UI falls out quickly. The People table as primary entity made everything click.

#### 4. Discord Buttons Work for AI Approval

**Expected:** Complex approval UI needed\
**Actual:** Discord's native button reactions provide perfect approval interface

The PM Agent posts to Discord with action buttons. Click "Approve" and Claude spawns to execute. Simple, mobile-friendly, already-installed.

---

### System Statistics

**Development Activity:**
- Total commits: 462
- Busiest day: Day 94 (Jan 3) - 105 commits 🔥
- Second busiest: Day 95 (Jan 4) - 83 commits
- Average commits/day: 66

**New Skills (12):**
- `podman` - Container management (consolidated from multiple scripts)
- `git-workflow` - Knowledge-rich commit patterns
- `pm2` - Long-running service management
- `scheduled-jobs` - Background automation overview
- `mcp-servers` - MCP server troubleshooting
- `google-drive` - Google Drive/Docs/Sheets via gogcli
- `/summarize` - Free summarization via OpenRouter
- `network-tracker` - UniFi presence tracking
- `/close-epic` - Beads workflow integration
- `nas-domain-setup` - Synology NAS domain configuration
- `pull-requests-review` - GitHub PR workflow
- `imsg` - iMessage server integration

**New Commands (2):**
- `/pm` - Project management with Discord approval flow
- `/research-links` - Newsletter link curation

**New Services (1):**
- **UniFi Network Tracker** - Physical presence detection via network devices + Discord check-ins

**Infrastructure:**
- Beads issue tracker initialized
- Sentry error tracking integrated
- WebSocket consolidation (Phases 1-5)
- imsg-server replaced MCP-based iMessage sync
- Wine cellar database with 52 bottles
- User impersonation for multi-user debugging

**Test Coverage:**
- Frontend tests: 169 → 420 (148% increase)
- Console command tests: 59 new tests

---

**Next:** @Andy Discord mentions bring conversational AI to Discord threads → [Week 12: Discord Conversations & Personal Archives](./week-12-days-97-103.md)
