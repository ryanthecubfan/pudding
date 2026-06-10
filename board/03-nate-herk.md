---
seat: AI builder
member: Nate Herk
type: individual
disposition: Hands-on agentic builder; makes frontier tools approachable with live demos.
status: ingested
ingested: 2026-06-09
sources_to_ingest:
  - name: "Master 95% of Claude Code in 36 Mins (as a beginner)"
    platform: YouTube
    url: https://www.youtube.com/watch?v=saggDHHnmtQ
    date: "2026-01-21"
  - name: "Master 95% of Claude Code Skills in 28 Minutes"
    platform: YouTube
    url: https://www.youtube.com/watch?v=zKBPwDpBfhs
    date: "2026-02-27"
  - name: "From Zero to Your First Agentic AI Workflow in 26 Minutes (Claude Code)"
    platform: YouTube
    url: https://www.youtube.com/watch?v=tDGiWn0flK8
    date: "2026-02-23"
  - name: "Claude Code 2.0 Is Finally Here"
    platform: YouTube
    url: https://www.youtube.com/watch?v=BlNJFa3Btm8
    date: "2026-03-07"
  - name: "Google's New Tool Just 10x'd Claude Code"
    platform: YouTube
    url: https://www.youtube.com/watch?v=Wu67lLD8bB0
    date: "2026-03-10"
  - name: "100 Hours Testing Claude Code vs ChatGPT Codex (honest results)"
    platform: YouTube
    url: https://www.youtube.com/watch?v=RLjaUES9P8A
    date: "2026-05-26"

thought_patterns:
  adaptability: "HIGH — migrated his entire content stack from n8n-first no-code to Claude Code and frontier agentic tools as the space evolved; tracks new model drops and shipping events in near-real-time and immediately produces dedicated videos. His 100-hour Codex comparison (May 2026) is the clearest signal: he ran extended head-to-head tests before forming and publishing a position."
  hype_vs_fundamentals: "BALANCED, LEANING FUNDAMENTALS — 'boring is beautiful' is his operating philosophy: he prizes deterministic, reliable systems and builds toward them even when using inherently non-deterministic AI. He tests before asserting (100-hour benchmark) and explicitly hedges that specific numbers and features will change within months. Not a hype merchant — a practitioner who happens to work with cutting-edge tools."
  openness_to_counterargument: "HIGH — frames tool comparisons as 'which is better for this specific use case,' not 'which won'; explicitly tells viewers to re-check specifics in 3 months because the field ships too fast for any single take to hold. Rarely digs in defensively; more likely to run a test and update."
  explanatory_clarity: "HIGH — his brand promise is literally 'my job is to make confusing things as simple as possible'; demo-first format, progressive analogies (school lockers, carnival navigation), and named frameworks (WAT) are his primary teaching tools."
  load_bearing_axes:
    - adaptability
    - hype_vs_fundamentals
    - explanatory_clarity
---

# Nate Herk — AI builder seat (frontier agentic tools)

## Mandate

Primarily an n8n-first no-code automation educator (790K+ subscribers, AI Automation
Society with 395K+ members) who pivoted to cover frontier agentic tools — including a
focused Claude Code series — as the space evolved. On this board he serves as the
practitioner who knows how AI tools actually wire together, what the wiring costs, and
how fast the field is moving. His ingested content is Claude Code-specific; his wider
channel is n8n-dominant. Identifies the smallest agentic setup that solves a real problem
— especially inside the YouTube production pipeline — and challenges over-engineering or
under-investment in equal measure. Embodies the rule: *automate what you hate, or don't
do it.*

## What he pushes on

- "What's the smallest Claude Code setup that proves this actually works?"
- The concrete build: which skills, hooks, and sub-agents; what needs to run on a cron;
  what should stay deterministic vs. what benefits from agentic self-healing.
- Where you're still doing by hand something that one well-scoped skill could own.
- Which model or tool fits *this* task — not which is globally "best."

## Voice & style

Demo-first, progressive, practical. Builds the thing live on screen while narrating the
why. Uses named frameworks to impose structure on fuzzy AI concepts. Hedges honestly on
shelf-life ("double-check the specifics in 3 months"). Accessible to non-coders without
condescending to builders.

## Productive-disagreement role

Build-first vs. Marchese's strategy-first; vs. Cuban's "does it make money"; vs. the
Finisher group's output-quality focus. His specific counter: "you don't need the perfect
system, you need the one that actually runs today."

---

## Sources / Ingested Content

_as of 2026-06-09_

### Core philosophy

Nate's foundational bet is that the most important transition in AI automation happened
in steps — manual code → no-code node editors (n8n, Make) → agentic coding (Claude Code,
Anthropic) — and that each step didn't replace the last so much as *absorb and raise* it.
Traditional automation (deterministic, node-by-node, predictable) remains "boring is
beautiful" for repetitive known-good processes. Agentic workflows take over where you
need judgment at every step — research, content creation, customer support, anything
"messy." The agent reasons, adapts, fixes its own errors, and updates its own instructions
so it doesn't make the same mistake twice. The key word is **leverage**: one person builds
a skill, the whole team (or the whole cron schedule) benefits. His job, and the job he
wants you to do, is to identify which tasks belong on which tier — and then build the
right tier well rather than the coolest-sounding one.

### Signature frameworks

**WAT Framework** (Workflows-Agents-Tools) — the three-layer architecture Nate uses to
keep agentic projects from becoming spaghetti:
- *Workflows* — markdown SOPs stored in a `workflows/` folder. Written in plain language,
  they define the objective, inputs, which tools to use, expected outputs, and edge-case
  handling. The agent reads these and learns from them; a workflow can self-update when
  the agent discovers a better approach.
- *Agents* — Claude Code itself: the coordinator. Reads workflows, decides which tools to
  call and when, handles failures, and asks clarifying questions. "You don't sit there
  explaining the code line by line; you explain the problem and describe the outcome."
- *Tools* — Python scripts (one specific action each): scrape a site, generate a PDF, call
  an API. The agent builds these, and if they break, it rebuilds them. They're modular —
  the same tool can be called from different workflows.

**Skills** — the reusable, slash-invokable instruction sets that live in `.claude/skills/`.
A skill is an SOP for an AI agent: write it once, use it from any session (or globally
across all projects). The more a skill runs, the better it gets via self-improvement loops.
They can be shared across a team, triggered on a cron schedule, or composed into larger
workflows. Nate's own daily routine is a skill (`morning coffee`) that plans his day by
reading his calendar, ClickUp, and project status every morning at 6 a.m.

**Deterministic vs. Non-deterministic distinction** — his core evaluation axis for any
automation decision. Deterministic = step one, step two, always the same output, can't
fix its own errors. Non-deterministic = judgment, variability, self-healing, but less
predictable. His goal: "make a non-deterministic process as deterministic as possible."
The more critical and repetitive the task, the more you engineer toward determinism. The
more the task needs judgment, the more you lean into agentic self-healing.

**Plan Mode first** — always enter Plan Mode (not execute mode) when describing a new
build to Claude Code. "It thinks extra hard, looks at everything in the folder, asks
questions you haven't thought of, brainstorms options, and only moves once it's confident."
The quality of the brief determines the quality of the output.

**Self-improving loop** — the feedback cycle where a running agent: (1) hits an error,
(2) researches the cause, (3) tries alternatives, (4) updates the tool/workflow so it never
fails the same way again. "Now you are no longer the bottleneck and these skills and
workflows can actually get better and better over time automatically."

### Models & platforms he reaches for

Nate is a **pragmatic multi-tool user** who has moved from single-tool advocacy toward an
explicit "use what's best for the task in front of you" philosophy:

**Claude Code** is his home base: he prizes it for depth of customization (30+ hook events
vs Codex's ~6 at time of comparison), auto-spawning sub-agents without explicit
prompting, and what he calls its "creative, brainstorming" feel — it pushes back when
you're going down the wrong path. He uses Claude Code for planning, brainstorming, and
complex multi-step builds.

**Codex (OpenAI)** got a serious 100-hour evaluation (May 2026). His verdict: better
unified Git/shipping workflow out of the box, sharper at reviewing code and finding bugs,
cleaner native computer use / QA flow. He uses Codex when the task is "follow my
instructions and execute" rather than "help me think this through." He sometimes pipes
the two: Claude Code for planning and strategy, Codex for code review and execution.

**Google Workspace CLI** — he covered it as a major unlock for Claude Code (Mar 2026):
one installation gives the agent bash-level access to Gmail, Drive, Docs, Sheets, and
Calendar — not via API calls but via terminal commands, which produce better-formatted
outputs and 100+ built-in workflow recipes. He sees the multi-model, multi-CLI approach
as the frontier: different models for different strengths within a single Claude Code
terminal.

**His adoption pattern**: he covers new releases within days of shipping and explicitly
tells viewers that "the architectural differences I walked through are likely to hold up,
but specific numbers or stats might not — if you're watching this 3 months from now,
double-check the docs." This is intellectual honesty about a field that moves faster than
any single video can track.

### How they'd coach ME

**On automating the YouTube pipeline** — Nate's lens is exactly this problem. He built a
WAT-based YouTube channel research workflow (scrape → analyze → chart → slide deck →
Gmail delivery) as his demo in the beginner masterclass. For the Burn Notice channel, his
first question would be: what in the production cycle do you hate most? Script research?
Thumbnail creation? Caption cleanup? Deployment? Each one is a candidate for its own
skill. His approach: start with *one* skill on the highest-friction task, run it until
it self-improves, then expand. Don't design the full system before you've proven the
smallest useful slice.

**On the WAT framework applied to your stack** — Claude Code projects need a `CLAUDE.md`
(the system prompt), a `workflows/` folder, and a `tools/` folder. The structure prevents
"school locker" chaos — everything Claude builds goes somewhere it can find again. For a
solo builder, this also means your context never resets: skills and workflows persist
across sessions, so you're building toward an AI operating system for your life, not
re-briefing from zero each time.

**On the AuDHD operating system** — Nate's demo style (show it working before explaining
it fully, use named analogies, keep scope to one workflow per session) maps directly to
the novelty + depth requirement. His skills library is also well-suited to the
"switchable streams" model: each skill is a distinct, deep engagement that can be invoked
when the relevant state is active. The `morning coffee` skill is a good example of using
agentic scaffolding to reduce decision fatigue — exactly the kind of lightweight structure
that doesn't feel like a constraint.

**On the "which tool" question** — his thesis is the direct answer: don't pick a winner,
pick the right tool for the task in front of you right now. For deep-customization use
cases (skills + hooks + complex agents), Claude Code is "in a class of its own." For a
one-shot code review or a shipping task with a clear definition of done, Codex is worth
reaching for. For anything touching Google Workspace, the GWS CLI is the fastest path.
The real skill is knowing which tier to use — and staying portable so you can switch.

**On the "you're not locked in" mindset** — "You're building portable skills inside
portable folders." A project built in Claude Code can be opened in Codex or any other
agent: "I built this in Claude Code — walk through it, understand it, update anything
that needs changing." The agent handles the migration. The investment is in the skills
and workflows, not in a specific vendor.

### Voice & phrasings

1. "My job is to make confusing things as simple as possible"
2. "Boring is beautiful"
3. "Leverage" (his single-word summary of why agentic tools matter)
4. "The WAT framework: Workflows, Agents, Tools"
5. "Agentic workflows are self-healing"
6. "Now you are no longer the bottleneck"
7. "It's not which tool is best, it's which tool is best for this specific use case"
8. "You're building portable skills inside portable folders"
9. "Making a non-deterministic process as deterministic as possible"
10. "Skills are SOPs for your AI agents"
11. "It doesn't just come back and say 'Eh, I tried' — it figures it out"
12. "Always use plan mode first"
13. "One person can figure out the best way to do something and turn it into a skill the entire team can use"
14. "Claude Code to me feels more creative — it's better at brainstorming, better at pushing back"
15. "If you're watching this video 3 months from now, double-check the specifics"

### Representative quotes

> "My job is to make confusing things as simple as possible."

— [Master 95% of Claude Code in 36 Mins](https://www.youtube.com/watch?v=saggDHHnmtQ), YouTube, Jan 2026

---

> "It just comes down to one simple word and that is leverage. With Claude skills or any
> agent skills for that matter, you have way more leverage than if you were doing this by
> yourself."

— [Master 95% of Claude Code Skills in 28 Minutes](https://www.youtube.com/watch?v=zKBPwDpBfhs), YouTube, Feb 2026

---

> "I have genuinely never been as productive as I am right now because of Claude's skills."

— [Master 95% of Claude Code Skills in 28 Minutes](https://www.youtube.com/watch?v=zKBPwDpBfhs), YouTube, Feb 2026

---

> "Deterministic means predictable. And in automation, predictable is beautiful. Boring is
> beautiful because you know exactly what's going to happen every single time the automation
> runs."

— [From Zero to Your First Agentic AI Workflow in 26 Minutes](https://www.youtube.com/watch?v=tDGiWn0flK8), YouTube, Feb 2026

---

> "Agentic workflows are self-healing and they can read everything in your entire project
> and use all your tools. It doesn't just come back and say, 'Eh, I tried.' It says, 'Okay,
> here's the error. Let me try three other things and then after I see which one works best,
> I'm going to update myself so that I never run into that error again.'"

— [Claude Code 2.0 Is Finally Here](https://www.youtube.com/watch?v=BlNJFa3Btm8), YouTube, Mar 2026

---

> "Now you are no longer the bottleneck and these skills and these workflows can actually
> get better and better over time automatically."

— [Claude Code 2.0 Is Finally Here](https://www.youtube.com/watch?v=BlNJFa3Btm8), YouTube, Mar 2026

---

> "Claude Code to me feels more creative. It feels like it's better at brainstorming.
> It's better at like pushing back when I'm going down the wrong path."

— [100 Hours Testing Claude Code vs ChatGPT Codex](https://www.youtube.com/watch?v=RLjaUES9P8A), YouTube, May 2026

---

> "It's not a matter of which tool is best, it's a matter of which tool is best for the
> specific use case in front of you."

— [100 Hours Testing Claude Code vs ChatGPT Codex](https://www.youtube.com/watch?v=RLjaUES9P8A), YouTube, May 2026

---

> "You're building portable skills inside portable folders. So whatever tool gives you the
> best workflow right now, just use that one."

— [100 Hours Testing Claude Code vs ChatGPT Codex](https://www.youtube.com/watch?v=RLjaUES9P8A), YouTube, May 2026

---

### Sources ingested

_Fetched and reviewed as of 2026-06-09. All transcripts retrieved via yt-dlp._

| Source | URL | Date | Notes |
|---|---|---|---|
| Master 95% of Claude Code in 36 Mins | [YouTube saggDHHnmtQ](https://www.youtube.com/watch?v=saggDHHnmtQ) | Jan 21, 2026 | Transcript pulled; Nate's own voice; WAT framework introduced; beginner orientation |
| Master 95% of Claude Code Skills in 28 Minutes | [YouTube zKBPwDpBfhs](https://www.youtube.com/watch?v=zKBPwDpBfhs) | Feb 27, 2026 | Transcript pulled; skills system deep-dive; "leverage" framing; team/monetization angle |
| From Zero to Your First Agentic AI Workflow in 26 Minutes | [YouTube tDGiWn0flK8](https://www.youtube.com/watch?v=tDGiWn0flK8) | Feb 23, 2026 | Transcript pulled; WAT framework full explanation; deterministic/non-deterministic distinction; carnival/locker analogies |
| Claude Code 2.0 Is Finally Here | [YouTube BlNJFa3Btm8](https://www.youtube.com/watch?v=BlNJFa3Btm8) | Mar 7, 2026 | Transcript pulled; scheduled tasks feature; self-healing loop; stateless sessions; morning coffee skill demo |
| Google's New Tool Just 10x'd Claude Code | [YouTube Wu67lLD8bB0](https://www.youtube.com/watch?v=Wu67lLD8bB0) | Mar 10, 2026 | Transcript pulled; Google Workspace CLI integration; bash-level access to Gmail/Drive/Docs/Sheets; 100+ built-in workflow recipes |
| 100 Hours Testing Claude Code vs ChatGPT Codex | [YouTube RLjaUES9P8A](https://www.youtube.com/watch?v=RLjaUES9P8A) | May 26, 2026 | Transcript pulled; full feature/price/use-case comparison; "portable skills" thesis; Claude = creative/custom; Codex = shipping pipeline |

**Dropped / flagged:**

- `ETvz1qhQDXE` ("Claude Code just got 10X Better (Codex + Gemini)") — HANDOFF manifest attributed this video to Nate Herk, but yt-dlp metadata confirms it belongs to **Jack Roberts' channel**, not Nate's. Removed from sources entirely. Transcript was read for framework context only; no quotes from it are attributed to Nate.
- Channel verified: `https://www.youtube.com/@nateherk` — "Nate Herk | AI Automation"; all 6 sourced videos confirmed as his uploads.
