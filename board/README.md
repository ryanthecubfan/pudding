# Virtual Board of Advisors

A custom AI advisory board built from [`../career-coach-profile.md`](../career-coach-profile.md).
One Markdown file per member, YAML front matter for ETL. Designed to feed two downstream
steps (content ingestion, then a board skill).

**Big board by design:** there's no harm in many members — we convene the relevant *few*
for any given topic, ingest everyone's content, and prune later if a voice isn't earning its
seat. **Every member must have a real, ingestible public corpus** (that's why the private
"Jan" seat was retired — no public content to draw on).

## Pipeline status

1. ✅ **Profile** — `../career-coach-profile.md`
2. ✅ **Roster locked** — 13 members (below), each its own file
3. ⬜ **Ingest content** — fill each member's `Sources / Ingested Content` section
   (YouTubers/public corpora). User will provide the Step 3 prompt.
4. ⬜ **Board skill** — globs `board/[0-9]*.md`, loads personas + ingested content, convenes
   the relevant members on demand

## The roster

> File numbers are non-contiguous (02 retired with the Jan seat); this is cosmetic only —
> the board skill globs by pattern, not by sequence.

| # | Seat | Member | Content status |
|---|---|---|---|
| 01 | Commercial grilling | Mark Cuban | not ingested |
| 03 | AI builder | Austin Marchese | not ingested |
| 04 | AI builder | Nate Herk | not ingested |
| 05 | Belonging / self-compassion | Brené Brown | not ingested |
| 06 | Belonging / self-compassion | Pema Chödrön | not ingested |
| 07 | Creator growth | Paddy Galloway | not ingested |
| 08 | Creator growth | Colin and Samir | not ingested |
| 09 | Finisher | Ali Abdaal | not ingested |
| 10 | Finisher | Cal Newport | not ingested |
| 11 | Finisher | Oliver Burkeman | not ingested |
| 12 | Finisher | David Allen | not ingested |
| 13 | AuDHD / solo-builder peer | Pieter Levels | not ingested |
| 14 | AuDHD / solo-builder peer | Jessica McCabe | not ingested |

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
`sources_to_ingest` and `Sources / Ingested Content` fields are the hooks for Step 3.
