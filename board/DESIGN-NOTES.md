# Board Design Notes

Cross-cutting design principles for ingestion (Step 3) and the board skill (Step 4).
These apply across members and should be revisited during the higher-fidelity laptop
ingestion pass.

## 1. Capture thought *patterns*, not just content

When ingesting each member, don't only collect quotes/frameworks — characterize **how they
think**. Assess each member along these axes (and record the read in their card):

- **Adaptability vs. conviction** — Do they readily change their mind and follow new trends,
  or do they hold core philosophies they stick to regardless of fashion?
- **Hype-follower vs. fundamentals-analyzer** — Do they chase what's hot, or do they dig into
  *why* something is hyped/viral and reason from fundamentals?
- **Openness to counterargument** — How well do they listen to and integrate reasonable
  arguments from others? Do they steelman, or dig in?
- **Explanatory clarity** — How good are they at explaining themselves, *especially* hard
  technical concepts to non-technical people?

**Weighting is per-member, not uniform.** These axes matter a lot for some seats (e.g. the
AI builders and the strategic/commercial voices, where trend-discernment and clear
explanation are central) and far less for others (e.g. the belonging/self-compassion seat,
where presence and warmth matter more than trend-analysis). During ingestion, note which
axes are *load-bearing* for each member and rate those; skip the irrelevant ones.

Suggested per-member front-matter hook (add during ingestion):

```yaml
thought_patterns:
  adaptability: "<read>"        # trend-following <-> fixed core philosophy
  hype_vs_fundamentals: "<read>"
  openness_to_counterargument: "<read>"
  explanatory_clarity: "<read>"
  load_bearing_axes: [list the ones that actually matter for this member]
```

## 2. The board is *living* — members grow on their own

Source material is the **starting point**, not the ceiling. Each member should be able to
evolve beyond what their ingested corpus generated and **keep up with the times** —
incorporating new developments, new work the real person publishes, and the changing
landscape (especially true for the AI/tech and creator-growth seats, where the field moves
fast).

Implications for Step 4 (the board skill) and beyond:
- Treat each card as a **base layer** that can be refreshed/extended over time, not frozen.
- Build a refresh path: periodically re-ingest recent work and let the persona update its
  views (while keeping its core voice/thought-patterns recognizable).
- A member may *change its mind* over time as the world changes — that's a feature, and it
  should be consistent with their `adaptability` read above (the high-conviction members
  should evolve more slowly than the trend-responsive ones).
- Keep a lightweight changelog per member (or a dated "as of" note) so evolution is legible.
