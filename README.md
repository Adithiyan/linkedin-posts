# LLM Engineering — LinkedIn Content System

Weekly LinkedIn post automation for the "practical LLM engineer" niche.
Runs as a **scheduled Claude Code agent** — no API key, no hosting, no
LinkedIn API app. See `content-system.md` for the actual voice/format rules.

## How it works

A Sonnet agent runs on a weekly schedule (see `/schedule` config). Each run:

1. Scans GitHub trending, Hacker News, and ArXiv for the week's practical
   LLM-engineering-relevant items, filtered by the post-worthy/skip table in
   `content-system.md`.
2. Picks one candidate and a format (Crisp Take / Micro Story / Meme + Dry
   Take / Trend Connect), rotating per the cadence targets and what's
   already in `post-log.md`.
3. Verifies any stat/date/version claim with a live web search before using
   it — never states an unverified number as fact.
4. Drafts the post in voice (the always-do / never-do rules in
   `content-system.md`).
5. Appends the entry to `post-log.md` and messages you the finished draft +
   an image idea for review.

**Publishing is always manual.** The agent never posts anything — you copy
the approved text into LinkedIn yourself.

## Files

- `content-system.md` — the single source of truth: niche, voice rules, the
  4 formats, the post-worthy/skip filter, and the fact-checking requirement.
  Edit this to change how drafts are written.
- `post-log.md` — history of every drafted post (topic, format, status,
  citations). Used to rotate formats and avoid repeating topics.

## Changing the schedule or prompt

Run `/schedule` to view or edit the scheduled agent (cadence, day/time, and
the prompt it runs with). The prompt should just point at
`content-system.md` and `post-log.md` rather than duplicating the rules, so
there's one place to edit voice/format changes.
