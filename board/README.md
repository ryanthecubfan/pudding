# Virtual Board of Advisors

A custom AI advisory board built from [`../career-coach-profile.md`](../career-coach-profile.md).
One Markdown file per member, YAML front matter for ETL. Designed to feed two downstream
steps (content ingestion, then a board skill).

**Big board by design:** there's no harm in many members — we convene the relevant *few*
for any given topic, ingest everyone's content, and prune later if a voice isn't earning its
seat. **Every member must have a real, ingestible public corpus** (that's why the private
"Jan" seat was retired — no public content to draw on).

> **See also [`DESIGN-NOTES.md`](DESIGN-NOTES.md)** — cross-cutting principles for ingestion:
> capture **thought patterns** (adaptability, hype-vs-fundamentals, openness to
> counterargument, explanatory clarity — weighted per member), and treat the board as
> **living** (members grow beyond their source material and keep up with the times).

## Pipeline status

1. ✅ **Profile** — `../career-coach-profile.md`
2. ✅ **Roster locked** — 13 members (below), each its own file
3. ⬜ **Ingest content** — fill each member's `Sources / Ingested Content` section AND the
   `thought_patterns` read (see DESIGN-NOTES). **Deferred to a laptop Claude Code session**
   (web fetch + `git push` are blocked in the web session). The approved source manifest for
   all 13 members and the full transfer plan live in **[`HANDOFF.md`](HANDOFF.md)**.
4. ⬜ **Board skill** — globs `board/[0-9]*.md`, loads personas + ingested content, convenes
   the relevant members on demand; supports refreshing/evolving each member over time.

## The roster

| # | Seat | Member | Content status |
|---|---|---|---|
| 01 | Commercial grilling | Mark Cuban | ingested (2026-06-09) |
| 02 | AI builder | Austin Marchese | ingested (2026-06-09) |
| 03 | AI builder | Nate Herk | ingested (2026-06-09) |
| 04 | Belonging / self-compassion | Brené Brown | not ingested |
| 05 | Belonging / self-compassion | Pema Chödrön | not ingested |
| 06 | Creator growth | Paddy Galloway | not ingested |
| 07 | Creator growth | Colin and Samir | not ingested |
| 08 | Finisher | Ali Abdaal | ingested (2026-06-09) |
| 09 | Finisher | Cal Newport | not ingested |
| 10 | Finisher | Oliver Burkeman | not ingested |
| 11 | Finisher | David Allen | not ingested |
| 12 | AuDHD / solo-builder peer | Pieter Levels | not ingested |
| 13 | AuDHD / solo-builder peer | Jessica McCabe | not ingested |

## Universal engagement rules (apply to EVERY member)

Straight from the profile (§8); they override any member's individual style:

- **Productive disagreement is mandatory.** If the convened members reach easy consensus, it
  failed.
- **Challenge with deference** — assume I've already thought about the obvious; go past it.
- **Never push me onto the defensive.** The instant I'm defensive, emotion takes over and the
  session is dead. The single most important rule.
- **Stay anchored to the North Star** ("Freedom to Explore. A Home to Return To.").
- **Respect the AuDHD operating system:** novel + deep wins; offer switchable streams; match
  task to current state; protect momentum (friction dynamic, never static).
- **Help me close loops without shaming the fit-and-finish pattern** — reframe "trim work" as
  novel, or design a genuine handoff.

## File format

Each `NN-member.md` has YAML front matter (machine-readable) + a Markdown charter. The
`sources_to_ingest` and `Sources / Ingested Content` fields are the hooks for Step 3, plus
the `thought_patterns` block described in DESIGN-NOTES.md.
