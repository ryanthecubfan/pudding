---
name: research-prospective-board-member
description: Ingest one board member for the pudding virtual board of advisors. Fetches real source material (YouTube transcripts via yt-dlp, web pages), synthesizes a full persona card matching the 08-ali-abdaal.md schema, and lands the work as a squash-merged PR. Use when the user invokes /research-prospective-board-member, mentions "ingest [name]", or says "do the next board member".
argument-hint: <member-number-or-name>
allowed-tools: Read, Bash, Edit, Write, WebFetch, WebSearch, Agent
---

# Research Prospective Board Member

Ingest one board member: fetch real sources, synthesize persona card, commit and ship as a PR.

## Overview

This skill runs the full Step 3 ingestion for a single board member in the `pudding` repo.
It follows the conventions in `board/HANDOFF.md` and produces output that matches the
`board/08-ali-abdaal.md` template exactly.

**One member per invocation.** Do not batch multiple members.

## Step 0: Identify the target member

If the user passed a number or name, use it. Otherwise:
1. Read `board/README.md` — find the first member whose row is `not ingested`.
2. Confirm the target with a one-line status before proceeding.

## Step 1: Pull the latest and branch

```bash
git pull origin main --rebase
git checkout -b ingest-<member-slug> origin/main
```

If the worktree is already on a branch ahead of main with no un-shipped work, rebase it:
```bash
git rebase origin/main
```

## Step 2: Read context files (required before writing anything)

Read all four in parallel:
- `career-coach-profile.md` — the owner's profile (needed for "How they'd coach ME")
- `board/README.md` — roster and universal engagement rules
- `board/DESIGN-NOTES.md` — thought_patterns framework + living board principles
- `board/08-ali-abdaal.md` — the exact format template; match it section-for-section
- `board/NN-member.md` for the target member — existing charter (Mandate, What they push on, Voice, Disagreement role)

Also read `board/HANDOFF.md §D` to find the approved source manifest for this member.

## Step 3: Fetch sources

### YouTube transcripts — use yt-dlp

```bash
yt-dlp --write-auto-sub --skip-download --sub-lang en --convert-subs srt \
  -o "/tmp/%(id)s" "https://www.youtube.com/watch?v=VIDEO_ID"
```

Then read the `.en.srt` file from `/tmp/`. Transcripts are long — read in chunks if needed.

**Only quote the subject's own voice.** If a video turns out to be narrated by a third party
about the subject (not the subject speaking), use it for framework context only, not quotes.

**TED talk pages** — `ted.com` only returns metadata. Use yt-dlp on the YouTube URL instead.
Most TED talks have a `youtube.com/watch?v=` equivalent.

**Apple Podcasts links** — unfetchable. Look for the same episode on YouTube or a transcript
host (podscripts.co, Spotify, the show's own site).

### Web pages — use WebFetch

Works well on: news articles (Fortune, CNBC, Guardian), book-summary sites
(grahammann.net, ericsandroni.com, tosummarise.com), open-access blog posts, publisher pages.

Returns only metadata on: ted.com talk pages (use yt-dlp instead), some personal sites.

May return 403 on: aliabdaal.com (all pages), some CNBC video pages, some personal sites.

### Delegation strategy

For heavy source work (multiple transcripts + multiple web pages), spawn a research
subagent (model: haiku or sonnet) to fetch and summarize. Pass it the exact URLs and
ask for key frameworks, phrasings, and verbatim quotes. Keep synthesis here in the main
session (Opus, if available).

### Source hygiene

- **No fabrication.** Every quote must be verifiable. If you can't confirm verbatim, write
  "(paraphrase)" after it.
- Dead links → drop the source, note it in the "Dropped / flagged" table row.
- For any source you couldn't open, try an alternate URL (YouTube vs. Apple Podcasts,
  transcript host vs. direct site) before dropping.
- Go beyond the manifest: look for recent 2025–2026 content especially for AI/tech and
  creator seats. The manifest is a starting point, not a ceiling.

## Step 4: Write the persona card

Fill the target `board/NN-member.md` file. **Preserve the existing charter sections**
(Mandate / What they push on / Voice & style / Productive-disagreement role) — add the
ingestion content below them, not instead of them.

### Front matter fields to fill

```yaml
status: ingested
ingested: YYYY-MM-DD          # today's date
sources_to_ingest:            # replace placeholder with real verified entries
  - name: "Source title"
    platform: YouTube | book | podcast | web
    url: https://...
    date: "YYYY-MM"
thought_patterns:             # see schema below
  adaptability: "RATING — one sentence rationale"
  hype_vs_fundamentals: "RATING — one sentence rationale"
  openness_to_counterargument: "RATING — one sentence rationale"
  explanatory_clarity: "RATING — one sentence rationale"
  load_bearing_axes:
    - axis_name
    - axis_name
```

Ratings: LOW / MEDIUM / MEDIUM-HIGH / HIGH / VERY HIGH. Include only the load-bearing axes
(2–4 per member). See `board/DESIGN-NOTES.md` for axis definitions and weighting guidance.

### Persona card sections (under `## Sources / Ingested Content`)

Open with `_as of YYYY-MM-DD_`.

**### Core philosophy** — 3–5 sentences: their fundamental worldview, the central inversion
or insight that makes them a distinctive voice. Not a bio — a lens.

**### Signature frameworks** — named models, methods, coined phrases with brief explanations.
Bolded framework names. Enough depth that a reader could actually apply them.

**### How they'd coach ME** — highest-value section. Apply their specific frameworks to the
owner's profile directly:
  - The fit-and-finish / trim-work handoff pattern
  - Momentum, AuDHD operating system, novelty vs. depth
  - The YouTube "Burn Notice" channel (if relevant to their seat)
  - Chore Cheerleader stall (if their frameworks speak to it)
  - Income urgency / runway pressure (if their frameworks speak to it)
  - Be specific — name their frameworks, not generic advice

**### Voice & phrasings** — 8–15 items. Characteristic vocabulary, coinages, sentence
structures. Short phrases, not full quotes.

**### Representative quotes** — 5–10 SHORT quotes. Format:
```
> "Quote text"

— [Source title](URL), Platform, Date
```
No fabrication. Paraphrase-and-label if unverified. Drop if can't verify.

**### Sources ingested** — table:
```
| Source | URL | Date | Notes |
```
Last rows: **Dropped / flagged:** — list every source that failed (403, unfetchable, AI-
narrated, Apple Podcasts, etc.) with a brief reason.

## Step 5: Update the README roster

In `board/README.md`, flip the member's row:
```
| not ingested |  →  | ingested (YYYY-MM-DD) |
```

## Step 6: Land the work

```bash
# Commit
git add board/NN-member.md board/README.md
git commit -m "Ingest <Name> persona card + thought patterns; update roster"

# Push + PR
git push -u origin ingest-<member-slug>
gh pr create \
  --title "Ingest <Name> persona card + thought patterns; update roster" \
  --body "..."

# Self-merge immediately (pre-authorized)
gh pr merge <number> --squash --delete-branch
```

If `gh pr merge --delete-branch` fails because `main` is checked out elsewhere (worktree
collision), use the GitHub API directly:
```bash
gh api repos/ryanthecubfan/pudding/pulls/<number>/merge \
  -X PUT -f merge_method=squash \
  -f commit_title="Ingest <Name> persona card + thought patterns; update roster (#<number>)"
```

## Quality checklist before committing

- [ ] Front matter complete: status, ingested date, sources_to_ingest (real URLs), thought_patterns
- [ ] Existing charter sections preserved unchanged
- [ ] Core philosophy: 3–5 sentences, distinctive lens (not a bio)
- [ ] Signature frameworks: named, bolded, actionable
- [ ] How they'd coach ME: specific to the owner's profile; names their frameworks
- [ ] Voice & phrasings: 8–15 items
- [ ] Representative quotes: 5–10, all attributed with URL + date; none fabricated
- [ ] Sources ingested table: complete; dropped sources listed
- [ ] README row flipped to `ingested (YYYY-MM-DD)`

## Member-specific notes

### Finisher seat members (Cal Newport, Oliver Burkeman, David Allen)
Bias toward **foundational frameworks over recent takes**. Their core work (Deep Work,
Four Thousand Weeks, GTD) is the payload; recent content is supplementary.

### Creator seat members (Colin and Samir, Paddy Galloway)
Surface **current platform mechanics** — what's working *right now* matters as much as
philosophy.

### AI builder seat members (Marchese, Herk)
Bias toward **2025–2026 content**; go past the manifest; prefer the most recent thinking
on Claude Code and frontier models.

### Known tool failures (update as discovered)
- `aliabdaal.com` — HTTP 403 on all pages. Use Goodreads, book-notes sites, YouTube transcripts.
- `ted.com` talk pages — returns metadata only. Use yt-dlp on the YouTube URL instead.
- Apple Podcasts links — unfetchable. Look for YouTube or transcript-host equivalent.
- CNBC video pages — sometimes 403. Try the article version of the same story.
- The Futur (thefutur.com) — article bodies may not load.
