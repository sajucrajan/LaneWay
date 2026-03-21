# I Got Tired of "Can You Share the Project Timeline?" — So I Built My Own Tool

## The origin story of LaneWay: office politics, no Monday.com, and one very satisfying exported PNG

---

Let me paint you a picture.

It's Thursday. You've been heads-down in delivery mode for three weeks. Suddenly, a Slack message appears:

> *"Hey, can you share the project timeline? Just a quick update for the stakeholders 😊"*

The emoji. THE EMOJI. Nothing says "this is not actually quick" like a 😊 at the end of that sentence.

You open MS Project. It takes 45 seconds to load. You remember you don't have a licence for the version that exports nicely. You open a shared spreadsheet someone made in 2019. You open Monday.com — wait, your organisation doesn't have Monday.com. You think about Jira. You close that thought immediately.

Twenty minutes later you've screenshotted a portion of a Gantt chart, cropped it in Paint, and sent it in an email with the subject line "Timeline (latest)" — which is the sixth email with that subject this month.

**There had to be a better way.**

---

## The Plan: Keep It Simple. Stupidly Simple.

No servers. No subscriptions. No IT ticket to request access. No "your trial has expired."

Just a file. Open it. Plan. Done.

That was the brief I gave myself. And the result is **LaneWay** — a full-featured Gantt chart and project timeline planner that runs entirely in a single HTML file.

Not a "simple" Gantt. A *proper* one.

Multi-plan tabs. Nine milestone shapes. Drag-and-drop everything. PNG export good enough to drop straight into a PowerPoint. Business days mode. Progress roll-up. Undo/redo. The works.

And it fits in one file you can email to yourself.

---

## How It Started (And How It Kept Growing)

It started small. A basic timeline with a few coloured bars. "Yeah, that's probably enough."

It was not enough.

First it was *"the bars need labels."* Then *"can there be multiple bars in the same row?"* Then *"what about milestones?"* Then *"the milestone label is too close to the diamond, can it be dragged?"* Then *"can it snap to 15-degree increments?"*

Reader, it snaps to 15-degree increments.

Each feature was born from a real frustration. Business days mode came from explaining to a stakeholder why a 30-calendar-day delivery was actually 21 working days. The multi-tab feature came from having four projects with completely different timeline widths fighting each other in the same view. The PNG export came from that first meeting where LaneWay was actually used — and someone asked "wait, what tool is this?" with genuine surprise.

That question felt good. That question is why LaneWay is now open source.

**A note on how it was built:** LaneWay was built entirely using Claude (Anthropic's AI) — every line of code, every feature, every design decision was a collaboration between a PM with a frustration and an AI with a text editor. No traditional coding background required. That's also part of the story.

---

## The Meeting That Made It Real

A few weeks ago I walked into a project review — the kind where stakeholders ask questions that have no good answers, the kind where someone will definitely say "can we align this with the strategic priorities" without specifying what those are.

I had a plan. I opened LaneWay, hit Export, chose 2× resolution, white background, full timeline. Downloaded a crisp PNG. Dropped it into the slide deck.

The question *"can you share the project timeline?"* came, as predicted.

I sent the PNG. 

No MS Project file that requires a licence to open. No "let me get you access to the Jira board." No spreadsheet with seventeen merged cells. Just a clean, readable image of the entire plan — phases, milestones, progress bars, the lot.

One person asked if it was from a paid tool.

It was not from a paid tool. It was from a 200KB HTML file — built with Claude, iterated over dozens of sessions, shaped entirely by real workflow needs.

---

## What LaneWay Actually Does

Here's what you get:

**The three-level model** — Plans contain Projects. Projects contain Phases (rows). Phases contain Segments (the coloured bars). Multiple segments can stack in the same row for sprint planning or parallel workstreams.

**Milestones** — nine shapes, eight types (Go-live, Kickoff, Freeze, Sign-off and more), draggable labels with connector lines you can customise: thickness, colour, solid/dashed/dotted.

**Multi-plan tabs** — each tab is a completely independent plan. Your 3-month sprint and your 18-month product roadmap don't have to fight over column widths anymore.

**Export that actually works** — full-width PNG (even if the timeline is wider than your screen), SVG, clipboard copy, and a print stylesheet for PDF. Resolution options: 1× draft, 2× recommended, 3× high-res. White or dark background.

**Everything else** — undo/redo (40 states), business days mode, phase progress roll-up, keyboard shortcuts, live stats bar, dark/light theme.

Zero installation. Zero subscription. Zero IT tickets.

---

## The Technical Bit (For the Curious)

Built on React 18 — but via the CDN UMD build, no JSX, no build step. The entire application is written as `React.createElement` calls (aliased as `h()`). The dev loop is: edit the file, reload the browser. That's it.

Everything saves to browser `localStorage` automatically. Export to JSON for backups. Import on another machine. Fully offline after first load.

The single-file constraint was intentional. It means you can commit it to git, email it, put it on a USB drive, or open it from a network share. No infrastructure required. No "wait for IT to provision the server."

The source is on GitHub, GNU GPL v3 licensed, and the contributing guide is literally "edit the HTML file and open a PR."

---

## Try It

**GitHub:** [github.com/sajucrajan/LaneWay](https://github.com/sajucrajan/LaneWay)

Download the file. Open it. Two demo plans are pre-loaded so you can see what it looks like in action. Delete them and build your own.

Next time someone sends you the 😊 message, you'll be ready.

---

*LaneWay — one file, no server, no subscription, no IT ticket. Just open and plan.*

---

**Tags:** `#ProjectManagement` `#OpenSource` `#BuildInPublic` `#WebDev` `#Productivity` `#GanttChart` `#SideProject`

