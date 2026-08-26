# LLM Engineering — LinkedIn Content System

Niche: practical LLM engineering — "the engineer who tests things, breaks
things, and translates what it means for people who build." Not a news
aggregator. Cadence: 1 post/week.

Voice: Karpathy precision + Hamel bluntness. Specific, direct, dry when
something's absurd. The observation carries the weight, not personality —
keep personality-on-display low.

## Always do
- Start with a specific claim, not a question
- Name the day, the error, the exact thing
- Let the observation carry the weight
- End with a real question or nothing
- Start sentences with "And" or "But" sometimes
- Add one detail only the author would know, if given
- Read it as if reading aloud before finalizing

## Never do
- "In today's rapidly evolving landscape..."
- "Let that sink in."
- "Unpopular opinion:" followed by a popular one
- "I've been thinking a lot about X lately"
- One-word-per-line fake-drama paragraphs
- Emoji as decoration
- Fake vulnerability
- External links in the post body
- Explain the joke or the meme
- "Thoughts?" alone as the closer

## The 4 formats

**Crisp Take** — weekly default. 800-1000 chars, 4-8 lines.
Hook (specific claim) → non-obvious layer underneath → your take → real
question or nothing.

**Micro Story** — ~2x/month. 1200-1500 chars.
What you tried (specific, past tense) → expected → what actually happened
(specific detail) → new rule → dry closer.

**Meme + Dry Take** — ~2x/month. 200-400 chars.
Name the meme format (e.g. "[Drake meme]") → 2-line dry engineering take →
optional real question. Never explain the meme.

**Trend Connect** — monthly. 1300-1600 chars.
Pattern stated as fact → 3 specific verified data points → what it means for
builders → what's being watched next.

Format rotation is decided by what's in `post-log.md`: default to Crisp
Take unless the rolling 4-week history is short on Micro Story, Meme, or
Trend Connect relative to their target cadence above.

## Post-worthy filter

The weekly filter question: "Does this change how I'd build something?"
Yes → candidate. Just impressive → skip.

| Post-worthy | Skip |
|---|---|
| Model deprecated / migrated | New SOTA benchmark (usually noise) |
| Pricing changed significantly | Funding round announcement |
| New capability breaks old assumption | "X says AI will change everything" |
| A pattern seen 3x just got a name | New model, no practical difference |
| Something tried failed/worked | Anything requiring a faked take |
| Architecture decision now looks wrong | Already covered by 5 newsletters |

## Sources to check each week

- GitHub trending (AI/ML repos, past week)
- Hacker News front page (AI/LLM threads)
- ArXiv new papers (cs.CL, cs.AI, cs.LG) — only if a result has a concrete
  practical implication
- Primary sources on demand: anthropic.com/news, openai.com/news,
  deepmind.google/discover/blog, ai.meta.com/blog, huggingface.co/blog

## Fact-checking rule (hard requirement)

Every number, date, or version claim in a post must be verified with a live
web search at draft time, with the source URL recorded in `post-log.md`.
Never state a stat as fact without a citation. If a number can't be
confirmed, soften it or drop it. See the Opus 4.1→4.8 mixup from
2026-08-24 as the concrete failure mode this rule exists to prevent — a
draft claimed Opus 4.1 users were redirected to Opus 5 on deprecation; the
real migration target was Opus 4.8, an unrelated model.

## Output per run

For each weekly run, produce:
1. WHAT — one line, what happened, with source URL
2. TAKE — one line, what you actually think
3. Format used, and why (per rotation logic above)
4. The full drafted post text
5. An image idea (one line — bold text card / meme template / annotated
   screenshot / side-by-side / digest card, per the doc's image system)
6. Citation URL(s) for any stat used

Then append the entry to `post-log.md` with status `drafted`, and message
the user the finished draft for review — never post it. Publishing is
always manual: the user copies the approved text into LinkedIn themselves.
