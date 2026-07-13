# Voice Keeper — a Walrus Memory prompt that never forgets how you write

> Submission for **Walrus Session 5: Walrus Memory Prompt Jam**.
> A system prompt that makes an AI writing agent remember your *voice* across sessions
> using [Walrus Memory](https://memory.walrus.xyz), so you never re-explain your tone,
> banned words, or formatting from scratch again.

## The problem

Anyone who writes with AI hits the same wall: every new session, the agent forgets your
voice and snaps back to generic, corporate defaults — so you re-explain your tone, banned
words, and formatting for the hundredth time. Writers, ghostwriters, newsletter authors,
and marketers who juggle multiple channels (a punchy LinkedIn voice, a warm newsletter
voice, a formal client voice) pay this tax every single day.

## The prompt

Full copy-pasteable prompt: [`voice-keeper-prompt.md`](./voice-keeper-prompt.md)

Paste it into any MCP client (Claude Desktop, Cursor, Cline, …) with the Walrus Memory MCP
server connected. It works with the standard tools `remember` / `recall` / `analyze` /
`restore`.

## How it works

- **Namespace per channel.** Each voice lives in its own namespace (`voice:newsletter`,
  `voice:linkedin`, `voice:client-acme`) so voices never leak into each other.
- **Recall-first.** Before writing a single sentence, the agent recalls the channel's
  rules, banned list, and before/after examples — starting every session already knowing
  how you write.
- **Signal vs. noise.** It stores only *durable* voice signals ("I always prefer short
  sentences"), never one-off edits ("shorten this paragraph"). When unsure, it asks.
- **Three structured memory types.** `[RULE]`, `[BANNED]`, and `[EXEMPLAR]` (before→after),
  each in a fixed format so memories stay searchable and de-duplicatable.
- **Append-only discipline.** Because Walrus Memory is append-only, the agent recalls
  before writing, skips duplicates, and marks changed rules with `SUPERSEDES '<old rule>'`
  so the newest instruction always wins — keeping memory clean instead of a landfill.
- **Self-audit.** Before handing over any draft, it silently checks the draft against the
  recalled banned list and rules, fixes violations, and reports what it caught.

## Why it belongs in the docs

The pain is the most universal one for anyone writing with AI, and the prompt demonstrates
three reusable Walrus Memory patterns that apply far beyond writing: **recall-before-act**,
**namespace-per-context**, and **append-only-aware supersede**. It's a reference
implementation, not a one-off.

## Proof it works

- **Agent ID:** `<paste your MEMWAL_AGENT_ID>`
- **Blob count:** `<paste count after running>`
- **Demo video:** `<Walrus link>`

See [`SUBMISSION.md`](./SUBMISSION.md) for the full submission package (problem statement,
proof steps, and a shot-by-shot demo script) and [`FORM-FILL-GUIDE.md`](./FORM-FILL-GUIDE.md)
for how each submission-form field maps to this repo.

## Files

| File | What it is |
|---|---|
| [`voice-keeper-prompt.md`](./voice-keeper-prompt.md) | The full copy-pasteable system prompt |
| [`SUBMISSION.md`](./SUBMISSION.md) | Submission package + demo script |
| [`FORM-FILL-GUIDE.md`](./FORM-FILL-GUIDE.md) | Field-by-field guide for the submission form |
| [`GITHUB-ISSUES.md`](./GITHUB-ISSUES.md) | Ready-to-file feedback issues (bug bounty) |

## License

MIT — use it, remix it, ship it.
