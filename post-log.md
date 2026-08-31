# Post Log

One entry per weekly run. Newest first. Used to decide format rotation
(see `content-system.md`) and to avoid repeating a topic.

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
- **Status:** drafted
- **Citations:**
  - https://arxiv.org/abs/2608.09867 (paper: "Stealing Reasoning Traces
    from Proprietary LLM APIs", submitted 2026-08-10)
  - https://thehackernews.com/2026/08/openai-anthropic-google-api-flaw-let.html

<!-- The weekly automation appends new entries above this line, below the header. -->
