# HANDOFF — Web session → Laptop Claude Code session

**Purpose:** Transfer everything built in the web Claude session so a **Claude Code session
on your laptop** (where web fetch works and `git push` works with your own credentials) can
run **Step 3: ingestion** and then **Step 4: the board skill**.

**Key fact:** The repo *is* the transfer. Everything is committed to branch
`claude/busy-bohr-2vktsh`. The web session could NOT fetch web content (YouTube/TED/etc.
returned 403) or `git push` (the GitHub App lacked push rights), which is why ingestion was
deferred to your laptop. Nothing is stranded in the chat — it's all in these files.

---

## A. What's already in the repo (read these first)

- `career-coach-profile.md` — the full profile (role, North Star, strengths, blockers,
  trusted people, AuDHD operating system, constraints, dealbreakers).
- `board/README.md` — roster (13 members), universal engagement rules, pipeline status.
- `board/DESIGN-NOTES.md` — two cross-cutting principles: **capture thought patterns**
  (adaptability, hype-vs-fundamentals, openness to counterargument, explanatory clarity —
  weighted per member) and the **living board** (members evolve past their source material).
- `board/NN-member.md` (01–13) — each member's charter (seat, mandate, voice, disagreement
  role) with empty `Sources / Ingested Content` sections waiting to be filled.
- `board/HANDOFF.md` — this file (the plan + the approved source manifest in §D).

## B. Laptop setup (one time)

1. Install Claude Code on your laptop (desktop app or CLI).
2. Clone + check out the branch:
   ```bash
   git clone https://github.com/ryanthecubfan/pudding.git
   cd pudding
   git checkout claude/busy-bohr-2vktsh
   git pull origin claude/busy-bohr-2vktsh   # get the latest
   ```
3. (Recommended) Enable real video ingestion — pick one:
   - A YouTube-transcript MCP server, or
   - `yt-dlp --write-auto-sub --skip-download <url>` / an existing transcript API, or
   - just let Claude Code use its built-in web fetch for articles/blogs and transcripts
     where available.
4. Open Claude Code in the `pudding` repo and paste the kickoff prompt (§E).

## C. The ingestion task (what the laptop session should do, per member)

For each `board/NN-member.md`, fetch the approved sources in §D and fill in:

1. Put the approved links into the file's `sources_to_ingest:` front-matter block.
2. Write a **persona card** in the `Sources / Ingested Content` section using this schema:
   ```
   ### Core philosophy        # 3–5 sentences: their fundamental worldview
   ### Signature frameworks    # named models/methods, briefly
   ### How they'd coach ME     # their lens applied to MY profile (highest-value part)
   ### Voice & phrasings       # 8–15 characteristic phrasings / vocabulary
   ### Representative quotes    # 5–10 SHORT, attributed, with source link + date
   ### Sources ingested        # the URLs actually pulled, dated "as of"
   ```
3. Add the `thought_patterns` block from DESIGN-NOTES.md, rating only the **load-bearing
   axes** for that member (don't force all four where they don't matter).
4. Flip that member's row in `board/README.md` from `not ingested` to `ingested (YYYY-MM-DD)`.

**Rules (from DESIGN-NOTES + the session):**
- **No fabrication.** Quotes must be real, short, and attributed with a working link. If you
  can't verify, paraphrase and label it "(paraphrase)". Drop dead links; flag what you drop.
- **Recency bias for the AI/tech seats** (Marchese, Herk) and any tech content — prefer
  2025–2026. **Foundational bias for the Finishers + Belonging seats** (the core frameworks).
- **Living board:** treat each card as a base layer with an "as of" date; it can be
  refreshed later.

## D. APPROVED SOURCE MANIFEST (all 13)

Legend: ✅ verified · ⚠️ best-effort (verify in browser; web session couldn't click-confirm).
Per the user: keep best-effort links and re-verify from the laptop where fetch works.

### 01 — Mark Cuban (Commercial grilling)
1. Lex Fridman Podcast #422 (2024) — https://www.youtube.com/watch?v=80nE6l2NxhY ✅
2. "How to start a successful business" (Lex clip, 2024) — https://www.youtube.com/watch?v=yLFt0hdBMaI ✅
3. Blog Maverick — "Success & Motivation" (2009) — https://blogmaverick.com/2009/05/13/success-motivation/ ⚠️403
4. Blog Maverick — "The Sport of Business" (2009) — https://blogmaverick.com/2009/12/09/the-sport-of-business-3/ ⚠️403
5. Book — *How to Win at the Sport of Business* (2011) — https://diversionbooks.com/books/how-to-win-at-the-sport-of-business/ ✅
6. Fortune — "AI will be a baseline skill…" (Jul 2025) — https://fortune.com/2025/07/22/exclusive-mark-cuban-ai-business-success-entrepreneurs-investing/ ✅
7. Berkeley SCET talk — disrupting industries in an AI world (2024/25) — https://scet.berkeley.edu/mark-cuban-disrupting-industries-finding-opportunities-and-navigating-your-twenties-in-an-ai-world/ ✅
8. CNBC Make It — "$20 to launch a business…" (Jul 2025) — https://www.cnbc.com/2025/07/28/mark-cuban-how-to-launch-a-successful-business-with-zero-money.html ✅

### 02 — Austin Marchese (AI builder) — lens: explainer + "follow Anthropic/top AI people"
1. "You're Not Behind (Yet): How to become AI-Native in 2026" (~Dec 2025) — https://www.youtube.com/watch?v=F5tzbJwUjDk ✅
2. "You're Not Behind: Become AI-Native (without the overwhelm)" (2025/26) — https://www.youtube.com/watch?v=j63bBK_ct-M ⚠️date unverified
- Channel — https://www.youtube.com/@austin.marchese · "AI Must Watch" playlist — https://www.youtube.com/playlist?list=PLlaDCSpHX5Wy27pSh9det-V027sEGVSdo · site austinmarchese.tech · newsletter "The AI Playbook" (newsletter.the-ai-playbook.com)
- ⚠️ Thin/hard-to-index corpus. On laptop: pull the playlist's individual titles and find the videos where he urges following Anthropic / quotes Karpathy & top researchers. (He cites them — that's the angle the user wants.)

### 03 — Nate Herk (AI builder) — lens: Claude Code & frontier models, NOT n8n
1. "Master 95% of Claude Code in 36 Mins (beginner)" (~Jan 2026) — https://www.youtube.com/watch?v=saggDHHnmtQ ✅
2. "Master 95% of Claude Code Skills in 28 Minutes" (~Feb 2026) — https://www.youtube.com/watch?v=zKBPwDpBfhs ✅
3. "Google's New Tool Just 10x'd Claude Code" (~Mar 2026) — https://www.youtube.com/watch?v=Wu67lLD8bB0 ✅
4. "Claude Code just got 10X Better (Codex + Gemini)" (~Apr 2026) — https://www.youtube.com/watch?v=ETvz1qhQDXE ✅
5. "From Zero to Your First Agentic AI Workflow in 26 Min (Claude Code)" (~Feb 2026) — https://www.youtube.com/watch?v=tDGiWn0flK8 ✅
- ⚠️ Title-verified, ID-unconfirmed: "Claude Code 2.0 Is Finally Here" (~Mar 2026); "100 Hours Testing Clawdbot vs Claude Code" (2026). Channel — https://www.youtube.com/@nateherk

### 04 — Brené Brown (Belonging / self-compassion)
1. "The Power of Vulnerability" — TED (2010) — https://www.ted.com/talks/brene_brown_the_power_of_vulnerability ✅
2. "Listening to Shame" — TED (2012) — https://www.ted.com/talks/brene_brown_listening_to_shame ✅
3. *The Gifts of Imperfection* (2010) — https://brenebrown.com/book/the-gifts-of-imperfection/ ✅
4. *Daring Greatly* (2012) — https://brenebrown.com/book/daring-greatly/ ✅
5. *Dare to Lead* (2018) — https://brenebrown.com/book/dare-to-lead/ ✅
6. *Atlas of the Heart* (2021) — https://brenebrown.com/book/atlas-of-the-heart/ ✅
7. *The Call to Courage* — Netflix (2019) — https://www.netflix.com/title/81010166 ✅
8. Tim Ferriss Show #409 (2020) — https://tim.blog/2020/02/06/brene-brown-striving-self-acceptance-saving-marriages/ ✅
- Self-hosted podcasts (Unlocking Us / Dare to Lead) — https://brenebrown.com/podcasts/

### 05 — Pema Chödrön (Belonging / self-compassion)
1. *When Things Fall Apart* (1997) — https://www.penguinrandomhouse.com/books/642782/when-things-fall-apart-by-pema-chodron/ ✅
2. *Start Where You Are* (1994) — https://www.shambhala.com/start-where-you-are-2.html ⚠️url
3. *The Places That Scare You* (2001) — https://www.shambhala.com/the-places-that-scare-you-2.html ⚠️url
4. *The Wisdom of No Escape* (1991) — (find canonical publisher URL) ⚠️
5. Oprah Super Soul — "Welcoming the Unwelcome" (2019) — https://www.oprah.com/own-podcasts/super-soul-special-pema-chodron-welcoming-the-unwelcome ✅ (full ep https://www.youtube.com/watch?v=d8_ZKUQFFMg)
6. *Fail, Fail Again, Fail Better* (2015, Sounds True) — https://www.soundstrue.com/products/fail-fail-again-fail-better ✅

### 06 — Paddy Galloway (Creator growth)
1. Creator Science #209 — "How he makes any niche go viral" (2024) — https://podcast.creatorscience.com/paddy-galloway-2/ ✅
2. Creator Science #152 — packaging deep-dive — https://podcast.creatorscience.com/paddy-galloway/ ✅
3. "Meet the Man Who Solved YouTube" (Colin & Samir) — https://www.youtube.com/watch?v=HEiAiPGatwc ✅
4. "The New Rules of YouTube (2025)" (Colin & Samir, Apr 2025) — https://www.youtube.com/watch?v=L9CO1FcRHCM ✅ (writeup https://www.colinandsamir.com/resources/the-new-rules-of-youtube-from-paddy-galloway)
5. Jon Youshaei pod — "MrBeast's Secret YouTube Consultant" — https://creators.spotify.com/pod/profile/youshaei/episodes/Meet-MrBeasts-Secret-YouTube-Consultant-Paddy-Galloway-Interview-e21i5jo ✅
6. X thread — "3.3 Billion views to decode YouTube Shorts" (2023) — https://x.com/PaddyG96/status/1646898356419981315 ✅
7. X thread — "10 YouTube videos to study inside out" (2022) — https://x.com/PaddyG96/status/1516434710335045645 ✅
8. X thread — "5 most important learnings in visuals" (2025) — https://x.com/PaddyG96/status/1943710293982687622 ✅
- Channel — https://www.youtube.com/channel/UClga3ybuyyjpvqsh-cf3DvQ (pull 1–2 of his own uploads)

### 07 — Colin and Samir (Creator growth)
1. "MrBeast Reflects on Beast Games…" (5th interview, Jan 2025) — https://podcasts.apple.com/lc/podcast/mrbeast-reflects-on-beast-games-feastables-and-the/id1379942034?i=1000686682973 ✅
2. "An Unfiltered Conversation with MrBeast" — https://www.colinandsamir.com/resources/an-unfiltered-conversation-with-mrbeast ✅
3. "How to Make it on YouTube in 2025" (Jack Conte, Feb 2025) — https://www.youtube.com/watch?v=cNYw32X-WAU ✅
4. "Interview With the CEO of YouTube" (Neal Mohan, Nov 2023) — https://www.youtube.com/watch?v=Mf8g2qZ61Ms ✅
5. "The New Rules of YouTube (2025)" w/ Paddy — https://www.youtube.com/watch?v=L9CO1FcRHCM ✅
6. CNBC — creator-economy thesis (Sep 2025) — https://www.cnbc.com/video/2025/09/03/the-colin-samir-showa-co-hosts-on-the-creator-economy-economics-of-youtube.html ✅
7. The Futur — "Navigate Today's Creator Economy" — https://www.thefutur.com/content/how-to-navigate-todays-creator-economy---with-colin-and-samir ✅

### 08 — Ali Abdaal (Finisher)
1. *Feel-Good Productivity* (book, 2023) — https://aliabdaal.com/feel-good-productivity/ ✅
2. "How to Stop Procrastinating (Forever)" (2023) — https://www.youtube.com/watch?v=hJZ5v7dpKKM ⚠️id
3. "How to Stop Procrastinating and Finally Take Action" (2025) — https://aliabdaal.com/videos/how-to-stop-procrastinating-and-finally-take-action/ ✅
4. "How to Beat Procrastination" (Pressfield/Resistance) — https://www.youtube.com/watch?v=RP0oVOH4Zz4 ⚠️id
5. Diary of a CEO — "How To Finally Stay Productive" (2021) — https://podcasts.apple.com/ie/podcast/e93-productivity-expert-how-to-finally-stay-productive/id1291423644?i=1000532111442 ✅
6. *Deep Dive* podcast (his own) — https://aliabdaal.com/podcast/ ✅

### 09 — Cal Newport (Finisher)
1. *Deep Work* (2016) — https://calnewport.com/books/ ✅
2. *Digital Minimalism* (2019) — https://calnewport.com/books/ ✅
3. *Slow Productivity* (2024) — https://calnewport.com/books/ ✅ (most relevant to "finishing")
4. "Quit Social Media" — TEDxTysons (2016) — https://www.youtube.com/watch?v=3E7hkPZ-HTk ⚠️id
5. *Deep Questions* podcast — https://www.thedeeplife.com/ (Apple id1515786216) ✅
6. Study Hacks "Deep Habits" essays — https://calnewport.com/blog/ ✅
7. New Yorker columns — https://www.newyorker.com/contributors/cal-newport ✅

### 10 — Oliver Burkeman (Finisher)
1. *Four Thousand Weeks* (2021) — https://www.oliverburkeman.com/fourthousandweeks ✅
2. *Meditations for Mortals* (2024) — https://www.oliverburkeman.com/books ✅
3. Guardian — "the eight secrets to a (fairly) fulfilled life" (2020) — https://www.theguardian.com/lifeandstyle/2020/sep/04/oliver-burkeman-last-this-column-will-change-your-life ⚠️slug
4. *The Imperfectionist* newsletter — https://www.oliverburkeman.com/the-imperfectionist ✅
5. Ezra Klein Show — "Burned Out? Start Here." (2025) — https://podcasts.apple.com/us/podcast/burned-out-start-here/id1548604447?i=1000682997984 ✅
6. TED — "How to make the most of a finite life" — https://www.ted.com/podcasts/how-to-make-the-most-of-a-finite-life-oliver-burkeman-transcript ⚠️403

### 11 — David Allen (Finisher)
1. *Getting Things Done* (2001, rev. 2015) — https://gettingthingsdone.com/ ✅
2. TED — "Are you out of your mind?" — https://www.ted.com/talks/david_allen_are_you_out_of_your_mind ⚠️403
3. TEDxAmsterdam (2014) — https://www.youtube.com/watch?v=kOSFxKaqOm4 ⚠️id
4. Talks at Google — id `Qo7vUdKTlhk` — ⚠️UNCONFIRMED, re-check authorship
5. Tim Ferriss Show — "The Art of Getting Things Done" (2018) — https://tim.blog/2018/04/03/david-allen-getting-things-done/ ⚠️slug
6. GTD methodology hub — https://gettingthingsdone.com/what-is-gtd/ ✅

### 12 — Pieter Levels (AuDHD / solo-builder peer)
1. Lex Fridman #440 (Aug 2024) — https://lexfridman.com/pieter-levels/ ✅ (YT https://www.youtube.com/watch?v=oFtjKbXKqbg)
2. A Cheeky Pint w/ John Collison (Ep. 4, Jul 2025) — https://www.youtube.com/watch?v=StkCdcZ1ovE ✅ (transcript https://cheekypint.transistor.fm/4/transcript/)
3. fly.pieter.com — AI-built flight sim, "vibe coding" landmark (2025) — https://fly.pieter.com ✅ (coverage https://www.indiehackers.com/post/tech/pieter-levels-used-ai-to-build-a-viral-flight-simulator-in-3-hours-with-no-background-in-game-development-7CPfMr1yRLEwH6cC8xhE)
4. 2025 Vibe Coding Game Jam — https://jam.pieter.com/ ✅
5. "12 Startups in 12 Months" (2014) — https://levels.io/12-startups-12-months/ ✅
6. "Bootstrapping side projects into profitable startups" — https://levels.io/bootstrapping/ ✅
7. "How I build my minimum viable products" — https://levels.io/how-i-build-my-minimum-viable-products ✅
8. "Go Fucking Do It" (2014) — https://levels.io/go-fucking-do-it/ ✅
- X @levelsio — daily build-in-public / revenue threads (pull a few live)

### 13 — Jessica McCabe (AuDHD / solo-builder peer)
1. "Failing at Normal" — TEDx (2017) — https://www.youtube.com/watch?v=JiwZQNYlGQI ✅ (TED https://www.ted.com/talks/jessica_mccabe_failing_at_normal_an_adhd_success_story)
2. *How to ADHD* (book, 2024) — https://www.penguinrandomhouse.com/books/710890/how-to-adhd-by-jessica-mccabe/ ✅
3. "How to ADHD" YouTube channel — https://www.youtube.com/c/HowtoADHD ✅ (on laptop, pick signature videos: interest-based nervous system, requesting accommodations, how ADHD motivation works, "What is ADHD?")
4. ADDitude webinar #491 — https://www.additudemag.com/webinar/how-to-adhd-jessica-mccabe/ ✅

## E. Kickoff prompt for the laptop Claude Code session

> Paste this into Claude Code, opened in the `pudding` repo on branch
> `claude/busy-bohr-2vktsh`:

```
Read career-coach-profile.md, board/README.md, board/DESIGN-NOTES.md, and board/HANDOFF.md.

We're doing Step 3 (ingestion). For each board member file board/NN-member.md, use the
approved source manifest in board/HANDOFF.md §D. Fetch/transcribe the sources (use web fetch
and a YouTube-transcript method), then fill each member file with:
- the approved links in `sources_to_ingest:`
- a persona card (Core philosophy / Signature frameworks / How they'd coach ME / Voice &
  phrasings / Representative quotes [short, attributed, linked] / Sources ingested [dated])
- a `thought_patterns` block (only the load-bearing axes per DESIGN-NOTES)
and flip that member's row in board/README.md to `ingested (today's date)`.

Rules: no fabricated quotes (paraphrase + label if unverified; drop dead links and tell me).
Recency bias for the AI/tech seats (Marchese=explainer who follows Anthropic/Karpathy & top
AI people; Herk=Claude Code & frontier models, not n8n). Foundational bias for the Finishers
and Belonging seats. Commit per member (or per seat) and push to this branch.

Start with ONE member as a sample (suggest Ali Abdaal), show me the finished card, and wait
for my approval on the format before doing the rest.
```

## F. After ingestion → Step 4

Build the **board skill**: globs `board/[0-9]*.md`, loads the personas, lets you convene the
relevant few members on a topic (productive disagreement required; never put the user on the
defensive), and supports refreshing/evolving members over time (the "living board").
