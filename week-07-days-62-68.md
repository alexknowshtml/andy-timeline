# Week 7: API-First Architecture (Days 62-68)

**December 2-8, 2025** | [← Previous: Week 6](./week-06-days-55-61.md) | [Next: Week 8 →](./week-08-days-69-75.md)

> **Previously:** The chat UI feature explosion shipped Sparkfile, image uploads, and slash command intelligence in a single day. Synthesis Intelligence agents came online, and the orbit/tag system was finally separated after 55 days of technical debt.

---

## Overview: Everything Becomes an API

Days 62-68 marked a fundamental architectural shift: everything moved to APIs. Projects, events, tasks, workstreams - all became database-backed services accessible through skills. Voice input arrived, making Andy genuinely useful on mobile. Claude Memory integration brought external memory systems into the fold. Token usage observability emerged for cost tracking.

**Key themes:** API skills explosion, voice input, Claude Memory integration, disaster recovery, event system migration, token optimization, daily reflection prompts.

---

## Day 62: Project Import & API Foundation (December 2, 2025)

**The API Skills Emerge (136 commits)**

The day began with a major architectural shift: instead of file-based project management, everything would go through Andy Core's API.

**New Slash Commands:**
- `/import-project` - Guided project migration from markdown to database
- Task ordering by count (easiest-first import strategy)
- Polymorphic notes for projects/tasks/phases

**Database Evolution:**
- `ed0c4a7a0`: Add personables table for linking people to any model
- `bdb67431e`: Add file_path to people table for source tracking
- `9e6b52d3e`: Add description and completed_at fields to tasks

**Decision-Review Skill:**
A new skill emerged for walking through unresolved decisions:
- Detect decision signals in documents
- Propose → React → Document flow
- Refinement signal detection for improvement opportunities

**Project Detail UI:**
- Altitude views (/projects/life, /projects/ground)
- Clean URLs for project navigation
- What's Next header with altitude tabs
- Progress bar with source path below

**Email Scanning Subagent:**
- `6e2823315`: Add sent-email-scanner subagent to prevent context bloat
- Haiku scanner replaced with direct Gmail API script
- Faster relationship-refresh cycles

---

## Day 63: Voice Input & API Skills Explosion (December 3, 2025)

**Voice Input Feature (102 commits)**

The biggest feature of the day: voice input for the chat UI.

**Voice Implementation:**
- `25e649330`: Add voice input feature to chat interface
- Two modes: tap for manual, long-press for auto-stop
- Safari compatibility fixes for audio format detection
- Default voice mode setting in preferences

**Lesson Learned:** Input modality diversity (text, voice, image) makes systems more accessible. Voice unlocks mobile use cases.

**API Skills Created:**

This was the skills explosion day - four comprehensive API skills created:

**Events API Skill:**
- `496c4db98`: Add comprehensive Events API for Andy Core calendar
- Full CRUD operations for events
- Timezone handling for naive datetimes

**Tasks API Skill:**
- `a59966522`: Add full Tasks API with CRUD operations
- PostgreSQL boolean type gotcha documented

**Phases API Skill:**
- `e05b9192c`: Add Phases API with full CRUD

**Streams API Skill:**
- `91c793224`: Add Streams API with full CRUD and streams-api skill

**The Pattern:** Each API skill follows identical structure:
- Production URL configuration
- Full CRUD operation docs
- Related skills sections
- Trigger phrases for invocation

**Lesson Learned:** When you have 4+ similar things, create a template. API skills are the template for service integration.

**Caching Infrastructure:**
- `7f18d5381`: Add caching + cache invalidation for projects and events pages
- Event-project linking via polymorphic tables

**Link Healing:**
- `904a67cd0`: Fix broken links in historical documents (24 files)
- Continued link repair across the week

---

## Day 64: Disaster Recovery & Transcription (December 4, 2025)

**Server Infrastructure Hardening (93 commits)**

After the API skills, focus shifted to resilience.

**Disaster Recovery Documentation:**
- `70971bdd5`: Consolidate disaster recovery docs into single file
- `6864ef40c`: Switch backup to 1Password CLI
- `f02729666`: Add setup-server.sh for automated server provisioning
- Infrastructure configs captured for recovery

**Transcription Skill:**
- `05080408f`: Add transcribe-media skill
- `921199e5a`: Add speaker diarization to transcription workflow
- `cda3d4789`: Increase file upload limit to 200MB for large audio files
- `05080408f`: Add upload progress indicator

**Chat UI Improvements:**
- Rebuild button added to chat header
- Stale detection for when source files change
- Audio file upload support
- Compact dialog positioning fixes

**Email Auto-Linking:**
- `76691957f`: Fix email auto-linking showing raw HTML attributes
- `ab4860460`: Fix email auto-linking in chat markdown renderer

**Meeting Notes Evolution:**
- `ed3cf7df6`: Add recording/transcript intake to /process-meeting-notes
- Coworking advice snippets added

---

## Day 65: Workstreams & Session Archival (December 5, 2025)

**Terminology Refinement (71 commits)**

**Streams → Workstreams Rename:**
- `471ba3849`: Rename "streams" to "workstreams" throughout project system
- `d333c3e28`: Fix migration for PostgreSQL compatibility
- Cross-cutting themes (Marketing, Agents, Performance) now called workstreams

**Session Archival System:**
- `856c77575`: Add weekly Claude session archive job to DO Spaces
- `43d5bd0a0`: Fix extract-commands job for cron compatibility
- `438a8b4cb`: Document archive-claude-sessions and extract-commands jobs

**Newsletter Workflow:**
- `07c9c6645`: Fix newsletter workflow - correct script path and flags
- `9115a4001`: Add frontmatter to 15 slash commands for autocomplete extraction
- `/newsletter` added to chat autocomplete

**Chat Title Persistence:**
- `9458bf85f`: Add chat title persistence and slash command sync features
- `c1cc5ef1e`: Add sync button to /commands page for on-demand command extraction

---

## Day 66: Token Optimization & Event System (December 6, 2025)

**Major Token Reduction (87 commits)**

**Token Optimization Project:**

A systematic effort to reduce context consumption:

**Phase 1: Include Consolidation**
- `9ce04ef97`: Consolidate 3 email cache includes into 1
- `7d3d19c7a`: Merge 2 email filter config files
- `a3b3c5291`: Deduplicate communication rules to style-guide.md
- `c2e0e6680`: Merge documentation-map and sop-index

**Phase 2: Protocol Trimming**
- `9070e4569`: Trim protocol examples to 1 per file
- `6d7f417ad`: Reorganize CLAUDE.md context list

**Phase 3: Cleanup**
- `6469e7a0d`: Update stale references to consolidated files
- `6ca38bed5`: Remove 3 orphaned include files

**Lesson Learned:** Context cleanup isn't one-time. Schedule periodic optimization reviews.

**Event System Migration (Phases 1-3):**

The event system evolved from files to database:

**Phase 1:** People linking and outcomes tracking
**Phase 2:** Project people endpoints and Cursor data linking
**Phase 2.5:** Event planning data display in calendar UI
**Phase 3:** Event project templates and slash commands

**New Slash Commands:**
- `/plan-event` - Create event planning projects from templates
- `/document-outcomes` - Capture post-event outcomes

**Token Usage Observability:**
- `b502fb052`: Add token usage dashboard and slash command
- `f52fff8f8`: Add token usage tracking to claude_sessions table
- `2ca33cf00`: Add session analyzer for token usage observability
- `/token-usage` slash command for usage reporting

**Include Usage Reporting:**
- `f41788732`: Add include usage reporting command
- `326bc8c10`: Schedule weekly include usage reports

---

## Day 67: Event System Completion & Health Dashboard (December 7, 2025)

**UI Polish & Phase 4-5 Completion (88 commits)**

**Event System Phases 4-5:**
- `bb933d2cf`: Move agreement field from events to projects table
- `9ef5d2421`: Phase 5 cleanup - remove outdated event template
- Event system migration completed across all 5 phases

**Admin Health Dashboard Evolution:**
- `dc1897797`: Add collapsible health dashboard panels with auto-refresh
- `d070e3a65`: Sort health panels by status - problems first
- `19a86266a`: Add expand/collapse all toggle
- `ee8c02598`: Add info icon with tooltip for sync job descriptions

**Project Page Event Integration:**
- `91e097dff`: Add inline event detail sheet on project page
- Event tooltips explaining status dot meanings
- Persist event drawer state in URL

**Chat UI Enhancements:**
- `771d822e6`: Add 👍 emoji to page title when agent responds
- `4cac8d5aa`: Add optional response ready sound notification
- `2029e4ed3`: Persist chat open state across refresh
- Drop zone overlay fix for file dragging

**Auto Theme Feature:**
- `b184ee0e3`: Add auto theme with sunrise/sunset and dark override
- Sun-based automatic switching

**People Page:**
- `c4a105c2f`: Add People page with FileBrowser + sorting
- Remove markdown index in favor of database-driven view

**Performance:**
- `ece111b85`: Lazy load MDXEditor and optimize bundle chunking
- Shared FileBrowser component for Knowledge and Meetings pages

**New Slash Command:**
- `/bug` - Create GitHub issues from conversation context

---

## Day 68: Claude Memory Integration (December 8, 2025)

**Memory System Arrives (40+ commits as of afternoon)**

**Claude Memory Viewer:**
- `c875ac736`: Add Claude Memory viewer page
- `75d1b8bf4`: Use proxy for Claude Memory iframe
- `75c53b223`: Add Overview and Memory links to admin sidebar

**Caddy Proxy Configuration:**

Getting claude-mem to work through the reverse proxy required multiple iterations:
- `03fb85cbc`: Path-based proxy route for asset loading
- `5de9d30b0`: Use host.containers.internal for container-to-host proxying
- `ec354eb1d`: Proxy routes for SVG icons and logo
- `80b6e45c3`: Direct proxy routes for claude-mem API
- `47a980ac6`: Proxy route for preview API
- `a49172b88`: All claude-mem API routes for complete functionality

**Lesson Learned:** Reverse proxy setups for external services rarely work on first try. Budget for iteration.

**Knowledge Search MCP:**
- `f9f20142e`: Add knowledge-search MCP server, replace osgrep
- `b0653de81`: Remove osgrep files after switching

**Infisical Machine Identity:**

Server authentication improvements:
- `9dae6baeb`: Add Machine Identity setup for persistent server auth
- `a135752a5`: Add infisical auth setup script for servers
- `140b5618e`: Add machine identity auth for scheduled backups
- `dc8d4be18`: Add infisical-run.sh wrapper for machine identity auth

**Theme Fix:**
- `d1251db98`: Apply theme on initial page load
- Theme preferences now work immediately without navigation

**Event Planning:**
- `70e2122dc`: Auto-link event to project and improve workflow
- `f2a63ecc6`: Complete BSR 20th Anniversary project setup

**Dashboard Improvements:**
- `1a9b84b20`: UI/design improvements for Status Brief cards
- `e90ddfdb2`: Add expandable task details with description, people, waiting fors

**Daily Reflection Prompt:**
- New scheduled job for 4pm ET daily prompts to Discord
- Rotating question variations: "Who helped you today? Who did you support?"
- MCP-first architecture using Claude Code headless execution

**Lesson Learned:** API-first architecture pays compound dividends. Moving from file-based to database-backed systems (projects, events, tasks) enabled features that would have been impossible otherwise: live filtering, instant updates, cross-referencing. Voice input and Claude Memory integration showed that production systems need continuous enhancement, not "done" states.

---

## Reflection: Week 7

---

### The Mistakes We Made

#### 1. Claude Memory Proxy Iteration

**Cost:** 6+ commits to get claude-mem working through Caddy reverse proxy
**Fix:** Systematic path-based routing for assets, APIs, and icons
**Lesson Learned:** Reverse proxy setups for external services rarely work on first try. Budget for iteration.

#### 2. Event System Migration Complexity

**Cost:** 5 phases to migrate from file-based to database-driven events
**Fix:** Phased migration with data integrity checks at each step
**Lesson Learned:** Major system migrations need explicit phases with validation between each.

#### 3. Token Usage Double-Counting

**Cost:** Inaccurate cost tracking during streaming
**Fix:** Later fixed in Days 76-82 with proper streaming chunk detection
**Lesson Learned:** Streaming data requires different counting logic than batch data.

---

### The Surprising Things

#### 1. 136 Commits in a Single Day

**Expected:** Big feature days might hit 50-70 commits
**Actual:** Day 62 hit 136 commits - the API skills explosion

When a pattern is clear (API skills template), replication is fast.

#### 2. Voice Input Unlocked Mobile Use Cases

**Expected:** Voice would be a nice-to-have
**Actual:** Voice made Andy genuinely useful on mobile

The mode switch (tap vs long-press) matched natural interaction patterns.

#### 3. Token Optimization Found Low-Hanging Fruit

**Expected:** Context was already tight
**Actual:** 3 include consolidations, 2 file merges, orphaned files removed

Scheduled optimization reviews pay dividends. Context bloat is invisible until you look.

#### 4. Daily Reflection Prompts Changed Behavior

**Expected:** 4pm Discord prompts would be ignored
**Actual:** Regular prompts created accountability without friction

Low-effort nudges have outsized impact on habit formation.

---

### System Statistics

**Development Activity:**
- Total commits: 711 (Dec 2-8)
- Busiest day: Dec 2 - 136 commits
- Second busiest: Dec 3 - 102 commits

**New Slash Commands (8):**
- `/import-project` - Guided project migration
- `/plan-event` - Event planning from templates
- `/document-outcomes` - Post-event outcome capture
- `/token-usage` - Token usage reporting
- `/bug` - Create GitHub issues from context
- `/rebuild-andy-frontend` - Frontend rebuild automation
- `/create-skill` - Skill creation workflow

**New Skills (14):**
- events-api, projects-api, streams-api (workstreams)
- decision-review, directory-cleanup, email-triage
- place-capture, transcribe-media, podman-redirect
- email-modify-protocol, frontend-conventions
- reminder-tools (SKILL.md versions)

**New Agent:**
- sent-email-scanner - Subagent for context-efficient email scanning

**System Counts:**
- Agents: 41 total
- Slash Commands: 58 total
- Skills: 16 total
- SOPs: 102 total

**Event System Migration:**
- 5 phases completed
- File-based → Database-driven
- Agreement field moved to projects
- Event-project linking operational

**Token Optimization:**
- 3 include consolidations
- 2 file merges
- Examples trimmed across protocols
- Orphaned files removed

---

**Next:** Security hardening with Laravel Sanctum, push notifications, credential scanning, and knowledge library reorganization → [Week 8: Security Hardening](./week-08-days-69-75.md)
