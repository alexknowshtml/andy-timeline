# Week 9: Memory Intelligence (Days 76-82)

**December 16-22, 2025** | [← Previous: Week 8](./week-08-days-69-75.md) | [Next: Week 10 →](./week-10-days-83-89.md)

> **Previously:** Security hardening brought Laravel Sanctum, credential scanning, and push notifications. Light mode finally became production-ready. The task UX revolution shipped click-to-edit, due date pickers, and drag-and-drop phases in a single day.

---

## Overview: Memory Lane and Infrastructure Maturation

Days 76-82 marked a major shift toward **memory intelligence** - giving Andy the ability to remember, recall, and learn from past sessions. The week also laid the foundation for multi-user support with team-scoped credentials, and completed the migration from Infisical to Andy Core's native credential system. A full iMessage inbox triage system emerged, creating parity with email workflows.

**Key themes:** Memory Lane semantic search, host-bridge service extraction, credential system migration, iMessage inbox triage, token usage analytics, multi-user foundation, remote browser automation.

---

## Day 76: Credential Migration Begins (December 16, 2025)

**Commits: 74**

**Google OAuth Migration:**
- `3d7b28cf9`: Migrate Google Calendar OAuth to credential system
- `52b8a4c2b`: Migrate Gmail OAuth to credential system - Phase 2 COMPLETE
- `687450d51`: Add google-docs MCP with auth wrapper
- Full OAuth token management now through Andy Core's encrypted credentials

**Infisical Deprecation:**
- `3d7d8a238`: Remove Infisical references, use Andy Core credential system
- `1f4a5d1a8`: Update documentation for encrypted credentials system
- Consolidated from two secret management systems to one

**Documentation Cleanup:**
- `02996e6bc`: Add frontmatter protection warning to newsletter SOP
- `40b26f398`: Consolidate to single person template in .claude/includes

---

## Day 77: Remote Browser Automation (December 17, 2025)

**Commits: 70**

**dev-browser MCP Integration:**
- `fef0117a0`: Add dev-browser remote automation SOP and update skill docs
- `d5bc09292`: Remove Playwright MCP references, dev-browser is the primary browser automation
- Unified browser automation through Tailscale-connected Mac machines

**Switch-Browser Script:**
- `9aeeaac40`: Add switch-browser script for remote browser host management
- `6249938c8`: switch-browser test auto-tries both Macs on failure
- Automatic failover between Mac Mini and Mac Studio for remote browser

**Remote Browser Skill:**
- `1ae70c894`: Update remote-browser skill with auto-switch and screenshot upload
- Production-ready browser automation for headless Claude Code sessions

---

## Day 78: Quiet Day (December 18, 2025)

**Commits: 17**

Maintenance day with minor fixes and relationship updates. System running smoothly with minimal intervention required.

---

## Day 79: Memory System Foundation (December 19, 2025)

**Commits: 35**

**Surprise-Triggered Memory Extraction:**
- `22c0a64c4`: Add surprise-triggered memory extraction
- `0a8753c4e`: Add surprise-triggered memory extraction to memory catcher
- When Claude expresses surprise ("I didn't know that!"), the system automatically captures the learning

**Meeting Processing:**
- `553ef6403`: Process action items from Jigar Mehta impromptu meeting (Dec 19)
- Continued refinement of meeting workflow

**Knowledge Base:**
- `1eb2755fe`: Add pg_textsearch to knowledge base for future reference
- `5059e3793`: Add Trimmy clipboard formatter to knowledge base

**Link Healing:**
- `692ab2d56`: Fix 6 broken links to browser-automation-with-playwright.md
- Automated maintenance continuing

---

## Day 80: Memory Lane Launch (December 20, 2025)

**Commits: 91** 🔥 (Busiest day of the week)

**Memory Lane Core Features:**
- `08090a4a7`: Implement hybrid entity retrieval: filter by entity, rank by query
- `7b8e436c2`: Add comprehensive memory system architecture documentation
- `94f096aa1`: Rename memory system to Memory Lane in documentation
- `47e171ecc`: Add "surfaced because" context to Memory Lane cards
- `ab4581bcb`: Improve semantic memory reason display based on similarity
- `e1dc71db3`: Persist searchQuery to database for Memory Lane context
- `014374615`: Add recall count tracking and display for memories
- `935b48048`: Add recall_count tracking to memories database

**Lesson Learned:** Memory without context is just data. Explaining why a memory surfaced makes it actionable.

**Memory Injection Enhancement:**
- `24d54fea5`: Always include minimal conversation context in semantic memory search
- `159b650ca`: Add PostToolUse hook for assistant-triggered memory recall
- `813c0c109`: Add graduated negative penalty to memory feedback
- Memories now surface during Claude Code sessions based on semantic relevance

**Host-Bridge Service Extraction:**
- `8c458cf3f`: Create host-bridge-server with service delegation
- `7137cf2f4`: Extract health-service from host-bridge
- `1693da9e2`: Extract job-service from host-bridge
- `4abd55dc4`: Extract claude-service from host-bridge
- `3d1253440`: Extract entity-service from host-bridge
- `e86dfe28e`: Extract memory-service from host-bridge (highest risk)
- `aaadaca7d`: Add embedding cache to memory-service
- Major architectural improvement: 1 monolith → 6 focused services

**Lesson Learned:** Order extractions by risk. Build confidence with easy wins before tackling the hardest piece.

**Memory Lane UI Polish:**
- `0a37a10b0`: Sort Memory Lane by most recently recalled first
- `473494db7`: Load persisted feedback on Memory Lane mount
- `465ea7429`: Fix recallCount to be session-scoped, not global
- `b2c84f514`: Add enhanced memory info display to Memory Lane panel
- Time Machine visualization, orbit heat maps, constellation animations

**Multi-User Foundation:**
- `1bbdba209`: Add Teams support for credential sharing
- `e6e2db213`: Add ANDY_USER_ID support to MCP wrapper scripts
- `32d9d1dbe`: Add user credentials page with global/per-user separation
- `bdc6e946a`: Add per-user proxy authentication to multi-user plan

**Admin Dashboard:**
- `423744406`: Add system health indicator dots to left nav sidebar
- `8b8dc3e31`: Add system stats to admin dashboard
- `5554da0c9`: Add MCP server metadata (first added, last modified dates)
- `aea77b1ea`: Add MCP server toggle and restart functionality
- `2e1e325e0`: Add Credentials admin UI for managing API keys

**New Skills:**
- `64028fdcf`: Add Cloudflare tunnel skill for public dev server access
- `6dff66d01`: Add Tally MCP wrapper script and clean up config

---

## Day 81: Token Analytics & Team Credentials (December 21, 2025)

**Commits: 91** 🔥 (Tied with Day 80)

**Token Usage Analytics:**
- `c57252d4b`: Add per-model token tracking for accurate session costs
- `9963cffdc`: Add model_tokens JSON cast to ClaudeSession model
- `19ea6f9c0`: Add API billing data for model breakdown chart
- `d04260d04`: Clarify data sources in token usage stats
- `5c60a5dfa`: Simplify token usage: show API billing inline with session stats
- `3122ac1bb`: Fix token counting to avoid double-counting streaming chunks
- Accurate cost tracking per model (Opus vs Sonnet vs Haiku)

**Lesson Learned:** You can't optimize what you don't measure. Model-level tracking reveals where money actually goes.

**Team Credential System:**
- `6bdaf99bb`: Add team-specific encryption keys for credential isolation
- `125a16f26`: Add team-id support to get-credential.ts and create Indy Hall team
- `1d6daea9c`: Add is_system flag to credentials for app-only secrets
- `bab2bdb7b`: Update credentials pages for team and app-only scopes
- Foundation for multi-tenant credential management

**Lesson Learned:** Multi-tenant architecture requires thinking ahead. Foundation work now enables features later.

**Infisical Migration Complete:**
- `58600ab03`: Complete Infisical to Andy Core credential migration
- `eceb27208`: Migrate file-upload.ts and restore-database.ts to database credentials
- `a61e8d91d`: Update archive-claude-sessions to use database credentials
- All scripts now use Andy Core's native credential system

**Plan Cleanup:**
- `3b5d67ddb`: Migrate 6 orphaned plans from ~/.claude/plans to project folder
- `aa4d08a06`: Archive 4 completed plans, create backlog for deferred ideas
- `5123a53d9`: Archive 4 completed plans, update backlog with deferred items
- `8210e0253`: Archive 7 completed/deferred plans, merge overview plans

**New Skills:**
- `4c75cc8b9`: Add gradient-peek skill for expandable content previews
- TaskRow redesign with gradient peek and improved expand UX

**Relationship Manager:**
- `125a16f26`: Enhance heat map with size, connections, and cluster interactions
- `393f2ea0b`: Replace Memory Lane orbit viz with heat map visualization

---

## Day 82: iMessage Inbox Triage (December 22, 2025)

**Commits: 51 (and counting)**

**iMessage Sync System:**
- `4a4d1c165`: Add iMessage sync scheduled job
- `879780f10`: Add iMessage unreplied text checker
- `1823c8377`: Register /check-texts slash command in frontend
- `a9878a222`: Add Haiku assessment to iMessage sync job
- Full sync of unreplied text messages with AI triage assessment

**Inbox Triage UI:**
- `6d7f1751e`: Implement Inbox text message triage UI
- `034bd2da5`: Polish Inbox UI with design improvements
- `69390cc40`: Improve Inbox action buttons and add dismiss confirmation
- `c1a45041f`: Fix phone number parsing to match MCP response format
- `9e339cbeb`: Add phone number lookup to iMessage sync for Reply button
- Complete text message triage interface with Done/Snooze/Reply actions

**Thread Management:**
- `97dd2577e`: Add AI summary to collapsed thread card with snooze styling
- `3d2b85f4f`: Rename Pending to Snoozed and show snooze-until date
- `1146d8133`: Clear snooze when marking thread as replied/dismissed
- `81eb3ccc2`: Fix sync job overwriting manual status changes in inbox
- Status tracking: needs_reply → replied/snoozed/dismissed

**Lesson Learned:** Proven patterns transfer across modalities. Text triage is email triage with different plumbing.

**UI Polish:**
- `fa5b0895f`: Simplify celebration card to stats-only with subtle pulse animation
- `715e0d55b`: Replace memory quotes with relationship nudge and subtle pulse animation
- `0ae988653`: Add yellow glow effect to latest message in thread cards
- `c37d66dcb`: Add smooth slide animation for snooze options
- `1076a58c7`: Fix sticky header on mobile by using h-screen scroll container

**Multi-User Environment:**
- `828818ae0`: Add ANDY_USER_ID env var to MCP servers for per-user credentials
- Continued foundation for multi-user support

**Lesson Learned:** Memory systems need to work at multiple timescales. Session-level recall ("what did we just discuss?"), cross-session memory ("you mentioned this last week"), and semantic search ("find related concepts") each serve different needs. The host-bridge service extraction (1 monolith → 6 services) showed that even rapidly-built systems benefit from architectural cleanup once they stabilize.

---

## Reflection: Week 9

---

### The Mistakes We Made

#### 1. Memory Service Was Highest Risk

**Cost:** Saved memory-service extraction for last in host-bridge refactor
**Fix:** Ordered extractions by risk - health-service first, memory-service last
**Lesson Learned:** Order extractions by risk. Build confidence with easy wins before tackling the hardest piece.

#### 2. Sync Job Overwrote Manual Changes

**Cost:** iMessage sync job was overwriting manual status changes (replied/dismissed)
**Fix:** Add logic to preserve manual changes during sync
**Lesson Learned:** Background jobs must respect manual overrides. Users are the source of truth.

#### 3. Token Double-Counting During Streaming

**Cost:** Cost tracking was inaccurate until Day 81
**Fix:** Detect and exclude streaming chunks from token counts
**Lesson Learned:** Streaming data has different shapes than batch data. Don't assume uniformity.

---

### The Surprising Things

#### 1. Memory Lane Surfacing Context Worked

**Expected:** Semantic search would be noisy
**Actual:** "Surfaced because..." explanations made memories actionable

Memory without context is just data. Explaining why a memory appeared made it useful.

#### 2. 91 Commits on Two Consecutive Days

**Expected:** Holiday week would be slow
**Actual:** Days 80 and 81 both hit 91 commits each

Memory Lane launch + token analytics + team credentials all shipped in the busiest 48-hour stretch.

#### 3. Host-Bridge Extraction Was Clean

**Expected:** Monolith → microservices would be painful
**Actual:** 1 monolith → 6 focused services with minimal issues

When you understand the boundaries, extraction is mechanical rather than creative.

#### 4. iMessage Triage Mirrored Email Exactly

**Expected:** Text messages would need different workflows
**Actual:** Sync → Assess → Triage → Act pattern worked unchanged

Proven patterns transfer across modalities. The plumbing differs, but the workflow is the same.

---

### System Statistics

**Development Activity:**
- Total commits: 359
- Busiest days: Dec 20 & Dec 21 - 91 commits each 🔥
- Third busiest: Dec 16 - 74 commits
- Average commits/day: 51

**New Slash Commands (1):**
- `/check-texts` - iMessage unreplied text checker

**New Skills (4):**
- `gradient-peek` - Expandable content previews
- `public-tunnel` - Cloudflare tunnel for dev server access
- `remote-browser` - Remote browser automation with switch-browser
- `transcribe-media` - Media transcription from URLs

**New SOPs (2):**
- `dev-browser-remote-automation.md` - Remote browser automation guide
- `credential-system-migration.md` - Infisical to Andy Core migration

**System Counts (Updated):**
- Agents: 44 total (stable)
- Slash Commands: 59 total (+1)
- Skills: 51 total (+4)
- SOPs: 106 total (+2)

**Major Features:**
- Memory Lane semantic memory system
- Host-bridge service extraction (6 services)
- iMessage inbox triage UI
- Token usage analytics with model breakdown
- Team credential system
- Infisical migration complete
- Remote browser automation

**UI/UX Improvements:**
- Inbox triage with Done/Snooze/Reply
- Thread card AI summaries
- Celebration card with relationship nudges
- Heat map visualization for relationships
- Gradient peek for expandable content
- Smooth snooze animations

---

**Next:** Auto-suggest buttons, /overview agent migration, Twitter API integration, and open source preparation → [Week 10: Agent Refactoring](./week-10-days-83-89.md)
