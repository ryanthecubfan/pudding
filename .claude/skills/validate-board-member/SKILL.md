---
name: validate-board-member
description: Validate one or all board member persona cards by cross-referencing against hold-out sources (sources not in the ingested set). Produces a structured report: frameworks present ✅ / missing ⚠️ / contradicted ❌, quote authenticity, and overall confidence rating. Use when the user invokes /validate-board-member, asks to "validate [name]", or says "validate the board".
argument-hint: <member-name-or-number | all>
allowed-tools: Read, Bash, Edit, Write, WebFetch, WebSearch, Agent
---

# Validate Board Member

Cross-reference a persona card against sources that were **not** ingested, to surface gaps,
inaccuracies, and hallucinated frameworks.

## Overview

After ingestion, each persona card is a synthesis of a specific source set. This skill
checks quality by fetching **hold-out sources** — real content about the same person that
was intentionally excluded from the ingestion — and comparing what those sources say against
what the card claims.

Output: a structured validation report per member. Not a rewrite — a diff.

## Step 0: Identify the target(s)

If the user passed a name or number, validate that member only.
If the user passed `all`, validate all members with `status: ingested` in their front matter.
For `all`, spawn one sub-agent per member (see §Parallel execution) and aggregate results.

## Step 1: Pull latest and read context

```bash
git pull origin main --rebase
```

Read in parallel:
- `career-coach-profile.md` — owner profile (needed to evaluate "How they'd coach ME")
- `board/README.md` — roster; use to confirm ingestion status
- `board/DESIGN-NOTES.md` — thought_patterns axis definitions
- `board/NN-member.md` for the target — this is what you're validating

From the target's front matter, extract the `sources_to_ingest` list — these are the
**already-ingested sources**. Hold-out sources must NOT appear in this list.

## Step 2: Select hold-out sources

Choose 3–5 sources per member based on the tier below. The only requirement: they must
be reachable and must NOT be in the member's `sources_to_ingest` list.

### Tier 1 — well-documented public figures
*Brené Brown, Pema Chödrön, Cal Newport, Oliver Burkeman, David Allen, Mark Cuban, Ali Abdaal*

Priority order:
1. **Wikipedia** — factual framework inventory, career timeline, canonical work titles
2. **Official site** (calnewport.com, brenebrown.com, gettingthingsdone.com, etc.) — their own framing
3. **A book-level summary** not used in ingestion (book-notes sites, publisher excerpts, Goodreads)
4. **A print or long-form interview** not in the manifest (Guardian, Atlantic, New Yorker, Inc., Tim Ferriss blog)
5. **A recent piece (2024–2026)** — checks for drift; are there new frameworks or retractions?

### Tier 2 — moderately documented
*Pieter Levels, Jessica McCabe, Paddy Galloway, Colin and Samir*

1. Wikipedia (if it exists)
2. Their **personal site / blog** not used in ingestion
3. A **recent video or post** from 2025–2026 not in the manifest
4. Press coverage (TechCrunch, Wired, creator-industry outlets)

### Tier 3 — niche creators (limited hold-outs)
*Austin Marchese, Nate Herk*

1. Their **personal site / newsletter** not used in ingestion
2. **GitHub profile** (for AI/dev builders — shows what they actually ship)
3. A **recent video** from 2025–2026 not in the manifest
4. Community mentions (Reddit, X/Twitter) — lower reliability, label accordingly

Note: Tier 3 validation is shallower by necessity. Flag low hold-out coverage explicitly
in the report.

### Per-member hold-out suggestions

Use these as starting points; verify URLs before fetching. Supplement with search if a
URL is dead.

| Member | Suggested hold-outs (check not already ingested) |
|---|---|
| Mark Cuban (#01) | Wikipedia, blog.dallasmavs.com, Inc. profile, Shark Tank press coverage |
| Austin Marchese (#02) | austinmarchese.com, GitHub profile, recent YouTube not ingested |
| Nate Herk (#03) | nateherk.com or newsletter, GitHub, recent YouTube not ingested |
| Brené Brown (#04) | Wikipedia, brenebrown.com/articles, The Gifts of Imperfection summary, Atlantic/Guardian profile |
| Pema Chödrön (#05) | Wikipedia, shambhala.com/author/pema-chodron, When Things Fall Apart summary, Lions Roar interview |
| Paddy Galloway (#06) | Wikipedia (if exists), recent YouTube not ingested, creator economy press |
| Colin and Samir (#07) | colinandsamir.com, recent YouTube not ingested, creator press (Tubefilter, etc.) |
| Ali Abdaal (#08) | Wikipedia, Feel-Good Productivity book summary, recent YouTube not ingested |
| Cal Newport (#09) | Wikipedia, calnewport.com blog posts, Deep Work book summary, So Good They Can't Ignore You summary |
| Oliver Burkeman (#10) | Wikipedia, theimperfectionist.com (newsletter), Four Thousand Weeks book summary, The Antidote summary |
| David Allen (#11) | Wikipedia, GTD book summary (tosummarise.com or similar), 43folders.com articles, recent interview |
| Pieter Levels (#12) | Wikipedia, levels.io blog posts not ingested, nomadlist.com about, recent X posts |
| Jessica McCabe (#13) | Wikipedia, howtoadhd.com articles not ingested, ADHD Experts podcast appearances |

## Step 3: Fetch and extract ground truth

For each hold-out source:

1. Fetch via `WebFetch` (web pages) or `yt-dlp` (YouTube).
2. Extract a **ground-truth inventory**:
   - Named frameworks / models / methods the person is known for
   - Canonical phrases or coinages in their own voice
   - Core philosophy / central worldview
   - Typical coaching advice style (prescriptive vs. exploratory, tough-love vs. compassionate, etc.)
   - Any claims about what this person does NOT believe or pushes back on

Label each item with its source URL. Do not fabricate — if a source is inaccessible, note
it and reduce the hold-out count.

**Delegation:** for members with 4+ hold-out sources, spawn a Haiku or Sonnet subagent to
fetch and extract. Pass it the URLs and ask for the ground-truth inventory. Keep synthesis
in the main agent (Opus if available).

## Step 4: Diff against the persona card

For each dimension below, mark each item:
- ✅ **Present** — card captures it accurately
- ⚠️ **Missing** — appears in hold-outs but not in the card
- ❌ **Contradicted** — card says X, hold-outs say Y (flag the discrepancy)
- 🔍 **Unverifiable** — in the card but not found in hold-outs (not necessarily wrong — may just be beyond hold-out coverage)

### Dimensions to check

**1. Framework completeness**
List every named framework/model from hold-outs. Is each one present in the card?
Pay special attention to the person's most canonical work (e.g., GTD for David Allen,
Deep Work for Cal Newport, vulnerability for Brené Brown).

**2. Quote authenticity**
For each representative quote in the card:
- Can it be found verbatim in any source (ingested OR hold-out)?
- If not, is it labelled "(paraphrase)"?
- Flag any quote that reads as fabricated (suspiciously generic, untraceable phrasing).

**3. Voice and register accuracy**
Does the card's "Voice & phrasings" section sound like the actual person? Compare against
the characteristic language in hold-out transcripts. Note any phrasings that feel off.

**4. Coaching fit for the owner's profile**
The "How they'd coach ME" section should apply the person's *specific* frameworks to the
owner's profile. Check: would this person actually say this, in this way, given their
philosophy? Flag generic advice that could apply to anyone.

**5. Thought patterns calibration**
Compare the card's `thought_patterns` ratings against what hold-outs reveal. Is
`hype_vs_fundamentals` calibrated correctly? Is `adaptability` consistent with how
the person actually responds to criticism or new information in interviews?

**6. Hallucination check**
Scan the card for any framework names, coined terms, or specific claims that do NOT
appear in any source (ingested or hold-out). These are 🔍 Unverifiable and worth
investigating. A term that doesn't appear anywhere in a search is a red flag.

## Step 5: Write the validation report

Produce a report in this format per member:

```markdown
## [Member Name] (#NN) — Validation Report

**Date:** YYYY-MM-DD
**Hold-out sources checked:** N
**Overall confidence:** HIGH / MEDIUM / LOW

### Hold-out sources used
| Source | URL | Reachable? |
|---|---|---|

### Framework inventory
| Framework | In card? | Source |
|---|---|---|
| Deep Work | ✅ Present | Wikipedia |
| ... | ⚠️ Missing | calnewport.com |

### Quote authenticity
| Quote (first 8 words) | Status | Notes |
|---|---|---|

### Voice accuracy
[1–3 sentences: does the voice section feel authentic?]

### Coaching fit
[1–3 sentences: does "How they'd coach ME" apply their specific frameworks?]

### Thought patterns calibration
[1–3 sentences: any axes that feel miscalibrated?]

### Issues to fix
- [ ] [Specific actionable fix if any]

### Verdict
[One sentence: overall quality of the card.]
```

If there are no issues, say so explicitly — a clean card is a valid result.

## Step 6: Aggregate (for `all` runs)

When validating all 13 members, produce:
1. Individual reports (one per member, in roster order)
2. A **summary table** at the top:

```markdown
| Member | Confidence | Missing frameworks | Suspect quotes | Issues |
|---|---|---|---|---|
| Cal Newport | HIGH | 0 | 0 | — |
| Oliver Burkeman | MEDIUM | 2 | 1 | See report |
```

3. A **priority fix list** — members ordered by issue severity, with one-line fix descriptions.

## Parallel execution (for `all`)

Spawn one sub-agent per member. Each agent runs Steps 1–5 for its member and returns a
completed validation report. Aggregate the results here.

```
Agent(name="validate-{slug}", model="sonnet", prompt="Validate board/NN-member.md per the validate-board-member skill. Run Steps 1–5 and return the completed report.")
```

After all agents return, run Step 6 synthesis here using Opus (if available).

## Quality notes

- **Do not rewrite the card** — this skill only produces a report. If fixes are needed,
  the user will decide whether to apply them (a separate task or a new PR).
- **Low hold-out coverage ≠ low quality.** Tier 3 members have fewer hold-outs; a LOW
  confidence rating there means *insufficient evidence*, not *evidence of problems*.
- **Missing ≠ wrong.** A framework missing from the card may be outside the ingested
  source set, not an error. Note it and let the user judge.
- **Be calibrated.** Most cards will be HIGH confidence after a thorough ingestion. Only
  flag real issues; do not manufacture concerns to seem thorough.
