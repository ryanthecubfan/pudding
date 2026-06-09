# pudding

A personal career-coaching project: the owner's profile plus a **virtual board of advisors**
(13 AI personas) built from it.

## Layout

- **`career-coach-profile.md`** — the profile: current role, North Star, strengths, blockers,
  trusted people, AuDHD operating system, constraints, dealbreakers.
- **`board/`** — the 13-member board:
  - `NN-*.md` — one charter / persona file per member.
  - `README.md` — roster table + universal engagement rules.
  - `DESIGN-NOTES.md` — thought-pattern axes + the "living board" principle.
  - `HANDOFF.md` — per-member source manifest + ingestion conventions (reference).
  - `08-ali-abdaal.md` — the completed card; the format template for the rest.
- **`CLAUDE.md`** — working conventions for Claude Code sessions (repo state is the source of
  truth; ship and self-merge immediately).

## Pipeline

profile ✅ → roster ✅ → **Step 3: ingest each member's content** (in progress) →
Step 4: build the board skill.

Progress lives in the repo, not a tracker: a member is done when its `board/NN-*.md` front
matter says `status: ingested` (and its row in `board/README.md` is flipped).
