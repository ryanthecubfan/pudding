# CLAUDE.md — working conventions for this repo

## What this repo is

A personal career-coaching project. `career-coach-profile.md` is the owner's profile;
`board/` is a **13-member virtual board of advisors** (AI personas) built from it.

Pipeline: profile ✅ → roster ✅ → **Step 3: ingest each member's content** (in progress) →
Step 4: build the board skill.

## The repo state IS the source of truth

Do **not** maintain a separate status / hand-off tracker, and don't trust one. To see what's
done and what's next, read the repo itself:

- `board/README.md` — the roster table (Content status column).
- `board/NN-*.md` front matter — `status: ingested` means that member is done; anything else
  means it still needs ingesting.
- `board/08-ali-abdaal.md` — the completed card; use it as the exact format template.

`board/HANDOFF.md` remains a useful **reference** (per-member source manifest + tool
limitations + session conventions), but it is **not** the status tracker — trust the member
files, not a checklist.

## Ship through a PR, self-merge immediately — no approval, no draft gating

The owner has **pre-authorized autonomous merges** in this repo, and wants **every change to
go through a PR** so the history is preserved. For any change:

1. `git pull origin main` first (multiple sessions run in parallel).
2. Branch off the latest `main`, commit, push.
3. **Always open a PR** — never commit directly to `main` (we keep the PR history).
4. **Merge it yourself, immediately** — `gh pr merge --squash --delete-branch`. Do not leave
   PRs as drafts; do not wait for approval.
5. **Merge races:** whoever loses reconciles — rebase onto the new `main` and re-push.

## Step 3 ingestion conventions

- **One board member per session.** Don't batch.
- Match the schema in `board/08-ali-abdaal.md` exactly: persona card (Core philosophy /
  Signature frameworks / How they'd coach ME / Voice & phrasings / Representative quotes /
  Sources ingested) + a `thought_patterns:` block (load-bearing axes only) + flip the
  member's row in `board/README.md`.
- **No fabricated quotes** — pull real transcripts with `yt-dlp`; paraphrase-and-label when
  unverified; drop and flag dead links. See `board/HANDOFF.md` §B–§D for tool limitations
  and the per-member source manifest.

## Recommended Claude Code settings (Max20 plan)

- **Model:** Opus 4.8 (`claude-opus-4-8`) for the driver session; `high` effort for
  ingestion, `xhigh` for the Step 4 board skill (coding).
- **Subagents → cheaper models:** delegate transcript pulls / fetches / link verification to
  **Haiku 4.5** or **Sonnet 4.6**; reserve Opus for synthesis.
- **One member per session** keeps context lean despite the 1M window; Max20 usage is metered
  on rolling windows, so chunk member-by-member.
