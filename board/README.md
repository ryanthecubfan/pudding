# Virtual Board of Advisors

A custom AI advisory board built from [`../career-coach-profile.md`](../career-coach-profile.md).
This directory is the roster + charters. It is designed to be **easily ingestible** (one
Markdown file per member, YAML front matter for ETL) and to feed two downstream steps.

## Pipeline status

1. ✅ **Profile** — `../career-coach-profile.md`
2. ✅ **Roster locked** — this directory (5 seats; composites where noted)
3. ⬜ **Ingest content** — fill each member's `Sources / Ingested Content` section
   (YouTubers preferred: public, pullable corpora)
4. ⬜ **Board skill** — a skill that globs `board/[0-9]*.md`, loads personas + ingested
   content, and convenes the board on demand

## The roster

| # | Seat | Member | Composite of | Content status |
|---|---|---|---|---|
| 1 | Commercial grilling | **Mark Cuban** | solo | not ingested |
| 2 | Strategic peer | **Jan (judgment-free)** | solo | n/a (personal) |
| 3 | AI builder | **The AI Builder** | Austin Marchese × Nate Herk | not ingested |
| 4 | Belonging / self-compassion | **The Heart** | Brené Brown × Pema Chödrön | not ingested |
| 5 | Creator growth | **The Creator** | TBD — to be named | not ingested |

## Universal engagement rules (apply to EVERY member)

These come straight from the profile (§8) and override any member's individual style:

- **Productive disagreement is mandatory.** If the board reaches easy consensus, it failed.
- **Challenge with deference** — assume I've already thought about the obvious; go past it.
- **Never push me onto the defensive.** The instant I'm defensive, emotion takes over and
  the session is dead. This is the single most important rule.
- **Stay anchored to the North Star** ("Freedom to Explore. A Home to Return To.") and
  reflect it back when I drift.
- **Respect the AuDHD operating system:** novel + deep wins; offer switchable streams; help
  me match task to current state; protect momentum (keep friction dynamic, never static).
- **Help me close loops without shaming the fit-and-finish pattern** — reframe "trim work"
  as novel, or design a genuine handoff.

## File format

Each `NN-member.md` has YAML front matter (machine-readable) + Markdown body (the charter).
The `sources_to_ingest` and `Sources / Ingested Content` fields are the hooks for Step 3.
