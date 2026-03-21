# LaneWay — Product Roadmap

> One file. No server. No subscription. Just open and plan.
>
> Every feature on this roadmap respects the core constraint: **LaneWay is a single HTML file that runs locally in a browser.** No hosting, no backend, no accounts.

---

## Current State (v9.0)

LaneWay is a fully-featured Gantt chart and project timeline planner. What's already built:

- Multi-plan tabs with independent settings
- Three-level hierarchy: Projects, Phases (7 types), Segments
- Milestones with 9 shapes, 8 types, draggable labels, connector lines, segment snapping
- Zoom presets (Month/Week/Day) with progressive header bands
- Business days mode (hide weekends, count working days)
- Phase progress roll-up (duration-weighted average)
- Export: JSON (lossless), PNG (1x/2x/3x), SVG, clipboard copy, print/PDF
- Undo/redo (40 states), keyboard shortcuts
- Dark/light theme toggle
- Auto-save to localStorage with backup nudge
- Live stats bar, column resizing, row height adjustment
- Demo plans seeded on first load
- QR code and compressed text sharing (share plans via code or QR image)
- Import from shared code or QR image upload

---

## Tier 1: Game-Changers

*These transform LaneWay from a timeline viewer into a real planning tool.*

### 1.1 Dependency Arrows & Auto-Scheduling
**Priority: Highest | Effort: 3-7 days**

The single most impactful remaining feature. Without dependencies, LaneWay is a drawing tool. With them, it becomes a planning engine.

- Finish-to-start (FS), start-to-start (SS), finish-to-finish (FF), start-to-finish (SF) connectors
- Auto-cascade: when a segment slips, downstream dependencies shift automatically
- Lag/lead time on connections (e.g. "starts 3 days after X finishes")
- Visual: curved SVG arrows on the milestone overlay layer, with hover highlighting
- Data model: new `deps[]` array on segments storing `{fromSegId, type, lag}`
- Drag to create: click a segment handle, drag to another segment to connect

### ~~1.2 Export as Standalone HTML~~ ✅ COMPLETE (v9.0)

Shipped in v9.0. ☰ → Share as File downloads a standalone HTML copy with the plan data pre-loaded. Recipient double-clicks and sees the plan immediately. Uses `window.__LANEWAY_PRELOAD__` injection.

### ~~1.3 QR Code & Compressed Text Sharing~~ ✅ COMPLETE (v9.0)

Shipped in v9.0. Share plans via compressed text code or QR code image. Import via pasting code or uploading QR image. LZ-String compression with Base64 fallback, dynamic QR sizing, adaptive error correction, and default-value stripping for minimal code size.

### ~~1.4 Command Palette (Ctrl+K / Cmd+K)~~ ✅ COMPLETE (v9.0)

Shipped in v9.0. Ctrl+K / Cmd+K opens spotlight-style search. 17 static actions + all projects, phases, and milestones searchable. Arrow keys to navigate, Enter to select, Escape to close.

### 1.5 AI Plan Generator (Optional)
**Priority: High | Effort: 3-5 days**

Natural language plan creation. Entirely optional — works without it.

- User provides an API key (OpenAI/Anthropic) — stored in localStorage, never sent elsewhere
- "Create a 6-month mobile app launch plan with discovery, dev, QA, UAT, and launch phases"
- "Add a QA phase after each dev phase in Project X"
- "Shift all milestones forward by 2 weeks"
- AI generates plan JSON that LaneWay imports directly
- Prompt templates for common scenarios
- No API key required for core functionality — this is a power-user enhancement

---

## Tier 2: Make It Indispensable

*These keep users coming back. LaneWay becomes the tool they can't work without.*

### 2.1 What-If Scenarios
**Priority: High | Effort: 2-3 days**

Every PM gets asked "what if we slip 2 weeks?" — this lets you answer in 30 seconds.

- Clone a plan as a "scenario" tab with a visual indicator (coloured tab border)
- Side-by-side comparison view: Scenario A vs Scenario B
- Diff highlighting: segments that moved show delta arrows, changed dates in red/green
- "Apply scenario" to make it the new baseline

### 2.2 Baseline / Snapshot Comparison
**Priority: High | Effort: 2-3 days**

Track planned vs actual delivery with visual drift indicators.

- "Lock baseline" button saves a snapshot of all dates and progress
- Ghost bars appear behind current bars showing original baseline dates
- Drift indicators: arrows/labels showing how many days each segment slipped or pulled in
- Baseline stored in plan JSON — exports and imports with the plan
- Multiple baselines supported (e.g. "Original plan", "Re-plan after Q2")

### 2.3 Critical Path Highlight
**Priority: High | Effort: 1-3 days**
*Requires: Tier 1.1 (Dependency Arrows)*

Auto-compute and visualise the longest dependency chain.

- Toggle to highlight critical path segments in red/orange
- Show total float/slack time on non-critical segments
- "What happens if this slips?" — hover a critical segment to see downstream impact
- Critical path recalculates automatically as dates change

### 2.4 One-Click Status Report Generator
**Priority: Medium | Effort: 2-3 days**

Solves the "can you share the project timeline?" problem permanently.

- Generate a clean status report from current plan state:
  - Overall progress percentage and trend
  - Milestones hit this period / upcoming in next 7/14/30 days
  - Segments at risk (0% progress but should have started)
  - Segments completed since last report
  - Critical path status (if dependencies exist)
- Output formats: copy to clipboard as markdown, download as HTML, or include in exported PNG
- Customisable: choose which sections to include

### 2.5 Progress History Sparkline
**Priority: Medium | Effort: 1-2 days**

Turn a static snapshot into a living story of project health.

- Auto-record overall progress % daily in localStorage
- Tiny sparkline chart in the stats bar showing trend over time
- Stall detection: "Progress hasn't moved in 5 days" subtle warning
- Per-project sparklines in the task list (optional toggle)

---

## Tier 3: Delight & Differentiate

*These make people love LaneWay and tell others about it.*

### 3.1 Alternative Views

Same underlying data, different visualisation. Toggle between views without losing any information.

**a) Kanban Board View**
- Segments displayed as cards in columns: Not Started / In Progress / Done
- Drag cards between columns to update progress
- Group by project or by phase type

**b) Calendar View**
- Monthly calendar grid showing milestones and segment start/end dates
- Click a date to see all activity for that day
- Compact month-at-a-glance with colour-coded dots

**c) Resource / Person View**
- Optional assignee field on segments
- Toggle to group rows by person instead of by phase
- Workload heatmap: colour-code weeks by capacity (green/amber/red)
- Identify over-allocated people at a glance

**d) Burndown / Burnup Chart**
- Toggle a line chart overlay on the Gantt
- Shows planned completion rate vs actual progress velocity
- Projected completion date based on current velocity

### 3.2 Templates Library
**Priority: Medium | Effort: 2-3 days**

Reduce blank-page anxiety. Get people to value in 10 seconds.

- Built-in plan templates:
  - Software Development (Agile sprints)
  - Software Development (Waterfall)
  - Product Launch
  - Marketing Campaign
  - Construction / Fit-out
  - Event Planning
  - Startup MVP Build
  - Cloud Migration / Cutover
  - Hiring Pipeline
- "Start from template" option when creating a new tab
- "Save as template" — save any plan as a reusable template in localStorage
- Template preview before applying

### 3.3 Import From Anything
**Priority: Medium | Effort: 3-5 days**

Remove the biggest adoption barrier: "I already have my plan elsewhere."

- **CSV/TSV paste**: paste spreadsheet data → auto-map columns → generate phases/segments
- **Markdown table import**: paste a markdown table with task names and dates
- **MS Project XML import**: parse `.xml` export format
- **Jira CSV export import**: map Jira fields (Summary, Start, Due, Status, Assignee) to LaneWay segments
- Smart column detection: auto-identify date columns, name columns, status columns
- Preview before import with field mapping UI

### 3.4 ICS Calendar Export
**Priority: Medium | Effort: 1 day**

Milestones belong in calendars. Bridge the gap.

- Export milestones as `.ics` calendar file
- Import into Google Calendar, Outlook, Apple Calendar
- Each milestone becomes a calendar event with plan name, project name, and milestone type
- Option to export segment start/end dates as calendar events too
- "Subscribe" link for recurring export (manual — re-export when plan changes)

### 3.5 Presentation / Slideshow Mode
**Priority: Medium | Effort: 3-5 days**

Replace PowerPoint for timeline presentations entirely.

- Full-screen mode with clean, distraction-free rendering
- Auto-scroll through the timeline at configurable speed
- Pause on each project with highlighted milestones
- Animated zoom transitions (month → week → day)
- Laser pointer cursor for live presentations
- "Present this project" — focus on a single project's timeline
- Press Escape to exit, spacebar to pause/resume

### 3.6 Annotations & Callouts
**Priority: Low | Effort: 2-3 days**

Capture context that lives alongside the visual plan.

- Click anywhere on the timeline to add a floating note
- Callout types: Info (blue), Warning (amber), Decision (green), Blocker (red)
- Connector lines from callouts to relevant segments
- Toggle all annotations visible/hidden
- Export includes annotations in PNG/SVG output

---

## Tier 4: Polish & Professional

*These make LaneWay feel like a premium tool.*

### 4.1 Minimap
- Thumbnail overview of the entire plan in a corner overlay
- Viewport indicator — shows what portion of the plan is currently visible
- Drag the viewport rectangle to navigate
- Essential for plans with 20+ projects and wide date ranges
- Toggle on/off

### 4.2 Custom Phase Types
- Replace the hardcoded 7 types (Arch/Dev/QA/UAT/Pilot/Prod/Hold) with user-defined types
- Custom label, colour, and icon per type
- Per-plan type definitions — each plan can have its own vocabulary
- Default set provided, fully editable
- Makes LaneWay useful beyond software: construction, marketing, events, hiring

### 4.3 Custom Fields on Segments
- Add arbitrary key-value fields: Owner, Priority, Cost, Story Points, Risk, Department
- Choose which fields appear as columns in the task list
- Filter and sort by custom fields
- Fields included in JSON export/import
- Field definitions stored per-plan

### 4.4 Filter, Search & Highlight
- Filter rows by: project, phase type, progress range, assignee, date range, keyword
- Dim non-matching rows instead of hiding them (preserves timeline context)
- Search highlights matching segments with a glow/pulse effect
- Active filters shown as removable chips above the task list
- "Show only critical path" filter (requires Tier 2.3)

### 4.5 Bulk Actions
- Multi-select rows: Shift+click (range), Ctrl/Cmd+click (toggle)
- Batch operations: shift all dates by N days, set progress, change colour/type, delete
- "Select all in this project" context menu option
- Visual selection indicator (highlighted rows)

### 4.6 PWA / Install as Desktop App
- Service worker for complete offline support from first load (no CDN dependency)
- Web app manifest with icon and app name
- "Install LaneWay" prompt — runs as standalone window, no browser chrome
- App icon on desktop, dock, or Start menu
- Note: requires the HTML file to be served from localhost or HTTPS (can bundle a tiny local server script)

### 4.7 Embed / iframe Mode
- `?embed=1` URL parameter triggers read-only rendering
- Hides toolbar, drawer, footer — shows only the Gantt chart
- Auto-resize to container width
- Interaction: hover to see tooltips, scroll to navigate, but no editing
- For Confluence, Notion, internal dashboards, or any iframe host

---

## Tier 5: Future Vision

*These make LaneWay a category-defining tool.*

### 5.1 Peer-to-Peer Collaboration (WebRTC)
- No server needed — direct browser-to-browser sync
- Share a session code; others join and see live cursors
- Conflict resolution: operational transforms or last-write-wins with undo
- Session state stored locally — collaboration is ephemeral, plan data stays in localStorage
- Still one HTML file, still no server
- Fallback: manual sync via export/import for async collaboration

### 5.2 Plan Health Dashboard
- Auto-calculated RAG status (Red/Amber/Green):
  - % complete vs % elapsed time
  - Milestones on track vs overdue
  - Critical path slack remaining
  - Progress velocity trend
- Health trend chart over time
- Exportable as a status badge image (PNG)
- Per-project and overall plan health

### 5.3 Monte Carlo Schedule Simulation
- Input optimistic / expected / pessimistic duration per segment
- Run 1,000 simulations in the browser (Web Worker for performance)
- Output: probability distribution of project completion dates
- "80% confidence of finishing by March 15th"
- Visual: confidence cone overlay on the Gantt chart
- Turns gut-feel estimates into statistical forecasts

### 5.4 Version History & Auto-Recovery
- Auto-save numbered versions in localStorage (last 10-20)
- "History" panel showing timestamped snapshots with change summaries
- Click to preview any version, restore, or diff against current
- "Oops" recovery: accidental deletes are always reversible
- Storage-aware: auto-prune oldest versions when localStorage is near capacity

### 5.5 Multi-Language (i18n)
- Language selector in settings
- Initial languages: English, Spanish, French, German, Japanese, Chinese, Hindi, Arabic (RTL)
- All UI strings in a language map object
- Community contributions welcome — add a language by editing one JSON block
- Date formatting respects locale

### 5.6 Accessibility (a11y)
- ARIA labels on all interactive elements
- Full keyboard navigation: Tab through rows, Enter to edit, arrow keys to navigate
- Screen reader announcements for drag-and-drop operations
- High-contrast mode toggle
- Focus indicators that meet WCAG 2.1 AA
- Opens up government and enterprise adoption

---

## Features Deliberately NOT on the Roadmap

These conflict with LaneWay's core philosophy:

| Feature | Why Not |
|---|---|
| User accounts / login | No server, no accounts — privacy by design |
| Cloud sync / database | Requires infrastructure — contradicts single-file approach |
| SaaS pricing / premium tier | LaneWay is free and open source, forever |
| Mobile-native app | The HTML file works in mobile browsers already |
| Plugin/extension system | Adds complexity; keep it one file |
| Real-time notifications | No server to push from |

---

## Priority Matrix

```
                        HIGH IMPACT
                            |
         Dependency Arrows  |  Export as Standalone HTML
         Critical Path      |  Compressed Plan Sharing
         What-If Scenarios  |  Command Palette
         Baselines          |  Status Report Generator
                            |
  HIGH EFFORT ──────────────┼────────────────── LOW EFFORT
                            |
         WebRTC Collab      |  Today Line Extension
         Monte Carlo        |  Progress Sparkline
         Import From All    |  ICS Calendar Export
         Alt Views          |  Custom Phase Types
                            |
                        LOW IMPACT
```

---

## Suggested Release Plan

| Release | Tier | Headline |
|---|---|---|
| **v9.0** | Tier 1 | "The Planning Release" — dependency arrows, standalone HTML export, compressed sharing, command palette |
| **v10.0** | Tier 2 | "The Intelligence Release" — what-if scenarios, baselines, critical path, status reports |
| **v11.0** | Tier 3 | "The Platform Release" — alternative views, templates, import from anything, presentation mode |
| **v12.0** | Tier 4 | "The Professional Release" — minimap, custom fields, filters, bulk actions, PWA |
| **v13.0** | Tier 5 | "The Collaboration Release" — WebRTC, health dashboard, Monte Carlo, i18n, a11y |

---

*Every feature respects the rule: one file, no server, no subscription. If it can't work locally in a browser, it doesn't belong in LaneWay.*
