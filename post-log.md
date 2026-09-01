# Post Log

One entry per weekly run. Newest first. Used to decide format rotation
(see `content-system.md`) and to avoid repeating a topic.

## 2026-09-01 — Weekly run (Crisp Take, Micro Story, Trend Connect + Meme alt)

### 1. Claude Code's "25% increase" is a 17% cut — Crisp Take
- **WHAT:** Anthropic announced a permanent 25% increase to Claude Code's
  standard weekly limits (Pro, Max, Team, seat-based Enterprise), effective
  September 14, 2026. The catch: Claude Code has been running a temporary
  50%-over-baseline promotional boost that also expires September 14. Net
  effect measured against today's boosted levels: a 17% cut, which
  Anthropic itself confirmed once users worked out the math. (Baseline
  100 → temporary boost 150 → new permanent limit 125.)
- **TAKE:** The 25% figure isn't false, it's just measured against the
  wrong baseline for anyone who's been living on the promo levels for
  months. A useful reminder to always ask "up from what?" when a vendor
  announcement gives you a bare percentage.
- **Format:** Crisp Take (weekly default; specific claim + non-obvious
  layer + take fits this cleanly).
- **Draft:**
  > Anthropic announced a 25% increase to Claude Code's weekly limits,
  > starting September 14. It applies across Pro, Max, Team, and
  > seat-based Enterprise plans.
  >
  > For anyone actually using Claude Code right now, that 25% increase is
  > a 17% cut.
  >
  > Here's the trick: today's limits include a temporary 50%-over-baseline
  > boost that also expires September 14. The new "25% increase" is
  > measured against the original floor, not against what you've been
  > running on for months. Baseline 100, temporary boost 150, new
  > permanent limit 125.
  >
  > Anthropic confirmed the 17% number once people did the math on it. The
  > announcement still read "25% increase."
  >
  > If a usage-limit announcement gives you a percentage, the next
  > question is always: up from what?
  >
  > Is anyone budgeting differently for the 14th?
- **Image idea:** Bold text card, black bg / white text — "100 → 150 →
  125." with "25% increase. Also a 17% cut." underneath.
- **Status:** drafted
- **Citations:**
  - https://www.bleepingcomputer.com/news/artificial-intelligence/anthropic-is-cutting-claude-codes-current-weekly-limits-by-17-percent/
  - https://www.notebookcheck.net/Anthropic-announces-a-25-increase-to-Claude-Code-limits-but-there-s-a-17-catch.1382735.0.html
  - https://www.manton.org/2026/08/29/anthropic-announced-a-limits-change.html

### 1a. Same story, alt version — Meme + Dry Take
- **WHAT:** Same as above.
- **TAKE:** Same underlying fact, played for the joke instead of the
  analysis — this is genuinely meme-shaped (a company doing the "up to
  50% off, but not really" pricing move on its own usage caps).
- **Format:** Meme + Dry Take (alt version of story #1, per weekly output
  rule requiring at least one lighter treatment where the material
  supports it).
- **Draft:**
  > [Confused math lady meme, equations floating around her head]
  >
  > Anthropic: "25% increase to your weekly limits."
  > Also Anthropic: your effective limit on Sept 14 is 17% lower than it
  > is today.
  >
  > Same announcement. Different baseline.
- **Image idea:** Meme template (confused math lady / equations), no
  caption overlay needed beyond the two lines above.
- **Status:** drafted
- **Citations:** same as story #1.

### 2. Agent KV cache compaction: eager trimming hurts, waiting one turn fixes it — Micro Story
- **WHAT:** A new empirical study ("Practical Online KV Cache Compaction
  for LLM Agents: An Empirical Study," arXiv 2608.00902, submitted
  2026-08-02) tested online KV cache compaction for long agent
  trajectories. Compacting immediately after each turn, using cheap
  boundary-heuristic proxies, hurt task accuracy substantially. Delaying
  compaction by one turn — using the agent's actual next query as the
  proxy instead — recovered most of the lost accuracy. Plain token
  eviction (TE) was more robust than attention-matching (AM) pruning under
  noisy proxies, and delayed TE cut KV cache size by roughly 80% across
  model scales while preserving most accuracy.
- **TAKE:** If you're building context-compaction into a live agent loop,
  the naive "compact as you go" implementation is the one the paper's own
  data argues against. Batching/delaying compaction by even one turn is a
  cheap, concrete change worth testing before reaching for fancier
  attention-based pruning.
- **Format:** Micro Story (log was short on this format; the
  tried-something → expected → actual → new-rule arc fits an empirical
  study's findings even though the "trying" was done by the paper's
  authors, not the account — framed accordingly, not as a personal test).
- **Draft:**
  > A new empirical study on agent KV cache compaction tried the obvious
  > approach first: compact the context right after every turn, using a
  > cheap proxy signal — a boundary heuristic, standing in for the query
  > you don't have yet — to guess what later steps would need.
  >
  > The expectation was that immediate compaction would be roughly as good
  > as waiting, just easier to wire into a live agent loop.
  >
  > It wasn't. Compacting immediately, before the agent's next real query
  > existed to check the guess against, cratered task accuracy. Delaying
  > compaction by even one turn — using the agent's actual next query as
  > the proxy instead of the boundary heuristic — recovered most of the
  > lost performance. Plain token eviction also held up better than
  > attention-based pruning once the proxy signal got noisy, which in a
  > live agent loop it always is. Delayed token eviction cut KV cache size
  > by roughly 80% across model scales while keeping most of the accuracy.
  >
  > New rule if you're trimming an agent's context window online: don't
  > compact the moment a turn ends. Let the next turn arrive, then decide
  > what the one before it actually needed.
  >
  > The paper calls itself "practical." The practical finding turned out
  > to be: wait.
- **Image idea:** Annotated screenshot / diagram — simple before/after bar
  comparing immediate-compaction accuracy vs. delayed-compaction accuracy
  vs. no-compaction baseline.
- **Status:** drafted
- **Citations:**
  - https://arxiv.org/abs/2608.00902

### 3. Capability-threshold safety frameworks are now actually gating releases — Trend Connect
- **WHAT/pattern:** Three separate frontier labs have had a model trip a
  capability-threshold safety framework in the last 16 months, moving
  those frameworks from policy documents to actual release-timing gates:
  (1) Anthropic activated ASL-3 protections for Claude Opus 4 in May 2025,
  precautionary, after the model outperformed prior Claude models on
  CBRN-related proxy tasks, without Anthropic confirming it had actually
  crossed the threshold; (2) Google DeepMind's Frontier Safety Framework
  report for Gemini 3 Pro (November 2025) found no Critical Capability
  Level was reached, but the model did trip the lower early-warning alert
  threshold for cybersecurity, triggering accelerated mitigation work; (3)
  OpenAI paused parts of its unreleased Astra model's development in
  August 2026 after internal testing couldn't rule out the model crossing
  the "critical" cyberattack-capability threshold in its Preparedness
  Framework, adding network restrictions, sandboxing, and tighter weight
  security before continuing.
- **TAKE:** None of these confirm a model definitively crossed a top-tier
  threshold — all three are precautionary or alert-level responses. But
  the pattern is real: safety evals are now upstream of the release
  calendar at all three major labs, not a post-hoc checkbox. For anyone
  building on frontier APIs, expect more agentic/tool-use capabilities to
  ship gated, monitored, or delayed going forward.
- **Format:** Trend Connect (monthly target, log had zero to date; three
  verified data points across three labs support the pattern format
  directly).
- **Draft:**
  > Frontier labs' capability-threshold safety frameworks stopped being
  > paper policy this year. They're now actually gating what ships.
  >
  > Three data points, three labs:
  >
  > Anthropic activated ASL-3 protections for Claude Opus 4 in May 2025 —
  > a precautionary move after the model outperformed prior Claude models
  > on CBRN-related proxy tasks, even though Anthropic said it hadn't
  > confirmed the model had actually crossed the threshold.
  >
  > Google DeepMind's Frontier Safety Framework report for Gemini 3 Pro
  > (November 2025) found the model didn't reach a Critical Capability
  > Level, but did trip the lower early-warning alert threshold for
  > cybersecurity — enough to trigger accelerated mitigation work.
  >
  > OpenAI paused parts of its unreleased Astra model's development in
  > August 2026 after internal testing couldn't rule out the model
  > crossing the "critical" threshold for cyberattack capability —
  > restricting network access, sandboxing execution, and tightening
  > weight security before work continued.
  >
  > None of these confirm a model definitively crossed a top-tier
  > threshold. But the pattern holds across all three labs: safety evals
  > are now upstream of the release calendar, not a checkbox after it.
  >
  > For anyone building on frontier APIs, that means agentic and tool-use
  > capabilities increasingly ship gated, monitored, or delayed — not
  > because the model failed benchmarks, but because it passed ones nobody
  > wanted it to pass.
  >
  > What's next to watch: which lab is first to confirm a model actually
  > crossed a top-tier threshold, and what changes once the "precautionary"
  > label comes off.
- **Image idea:** Side-by-side card — three columns (Anthropic / Google
  DeepMind / OpenAI), each with model name, date, and threshold tripped.
- **Status:** drafted
- **Citations:**
  - https://www.anthropic.com/activating-asl3-report
  - https://deepmind.google/models/fsf-reports/gemini-3-pro/
  - https://openai.com/index/responding-next-frontier-critical-cyber-capabilities/
  - https://techcrunch.com/2026/08/07/openai-says-it-slowed-astra-model-development-over-security-concerns/

### Bank — shortlisted, not drafted this run
- Claude Code's "auto mode" became the default for new sessions on Pro,
  Max, and Team plans starting 2026-08-14; Anthropic's own controlled test
  (1,053 paid testers) found human review caught 13.6% of dangerous
  commands vs. 89% for the auto-mode classifier.
  (https://techcrunch.com/2026/08/09/anthropic-is-turning-claude-codes-auto-mode-on-by-default/)
  — **Status:** bank
- DeepSeek open-sourced "DeepSeek Harness" (v0.1, developer preview,
  released 2026-08-13), an MIT-licensed agent runtime built on an
  "everything is a plugin" architecture (models, tools, skills, sessions,
  sandboxes, even the UI are all replaceable plugins). Reported star
  counts (200k+) look inflated for a 2.5-week-old repo and weren't
  independently confirmable this run — re-verify before drafting.
  (https://github.com/deepseek-ai/deepseek-harness)
  — **Status:** bank

## 2026-08-31 — Crisp Take
- **WHAT:** Anthropic, OpenAI, and Google all encrypted hidden reasoning
  tokens with one shared, provider-wide key (not per session/user/model
  tier). Researchers from ELLIS Institute Tübingen, Max Planck Institute,
  MATS Research, and Snyk exploited this to replay a strong model's
  encrypted reasoning block into a weaker sibling model and get it
  transcribed in plaintext — no jailbreak of the strong model required.
  Scanning 6,708 public agent trajectories scraped from GitHub/Hugging
  Face, they decoded 315,320 reasoning blocks and recovered 182 live
  credentials plus 367 PII artifacts from logs developers had already
  published. Anthropic said via its bug bounty program it did not see
  security implications when first notified.
- **TAKE:** Teams building/logging agent trajectories treated "encrypted"
  reasoning traces as safe to keep and share for debugging. They aren't —
  if a trajectory log with reasoning blocks lands in a public repo, you've
  published whatever the model was actually thinking that turn, not an
  opaque blob.
- **Format:** Crisp Take (weekly default; first run, no post history yet
  to indicate otherwise).
- **Draft:**
  > Anthropic, OpenAI, and Google encrypt their models' hidden reasoning
  > with one key per provider. Not per session, per user, or per model
  > tier.
  >
  > Researchers from the ELLIS Institute, Max Planck, and Snyk found you
  > can take an encrypted reasoning block from a guarded frontier model,
  > replay it into a cheap sibling model, and ask that weaker model to
  > transcribe it. No jailbreak needed. They scraped 6,708 public agent
  > trajectories off GitHub and Hugging Face, decoded 315,320 blocks, and
  > pulled 182 live credentials out of logs people had already published.
  >
  > The trace was never sold as a security boundary. But every team
  > logging agent runs for debugging treated "encrypted" as "safe to
  > keep." Anthropic's own read, via its bug bounty program, was that
  > this had no security implications.
  >
  > If your framework snapshots reasoning into a trajectory log and that
  > log lands in a public repo, you're not publishing a blob. You're
  > publishing whatever the model was thinking that turn.
  >
  > What's sitting in your debug logs right now?
- **Image idea:** Bold text card, black bg / white text — "One key. Every
  reasoning trace. Every provider." with a smaller line underneath.
- **Status:** drafted (backfilled with full text after the fact — this
  run predates the "save full draft text" rule)
- **Citations:**
  - https://arxiv.org/abs/2608.09867 (paper: "Stealing Reasoning Traces
    from Proprietary LLM APIs", submitted 2026-08-10)
  - https://thehackernews.com/2026/08/openai-anthropic-google-api-flaw-let.html

<!-- The weekly automation appends new entries above this line, below the header. -->
