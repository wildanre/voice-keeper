# Voice Keeper — Walrus Session 5 Submission Package

A copy-paste-ready submission for the **Walrus Memory Prompt Jam**. Fill in the two
placeholders (Agent ID, blob count, links) after you run the proof step.

---

## 1. The Prompt

Full copy-pasteable text is in [`voice-keeper-prompt.md`](./voice-keeper-prompt.md).
It's a system prompt that drops into any MCP client connected to the Walrus Memory server.

---

## 2. Problem Statement (2–4 sentences)

Anyone who writes with AI hits the same wall: every new session, the agent forgets your
voice and snaps back to generic, corporate defaults — so you re-explain your tone, banned
words, and formatting for the hundredth time. Writers, ghostwriters, newsletter authors,
and marketers who juggle multiple channels (a punchy LinkedIn voice, a warm newsletter
voice, a formal client voice) pay this tax every single day. Voice Keeper fixes it by
persisting your writing voice to Walrus — one profile per channel — and reloading it
automatically at the start of every session.

---

## 3. What It Does (plain language)

Voice Keeper gives the agent clear rules for **what** to remember, **when**, and **how**:

- **Namespaces per channel.** Each voice lives in its own namespace (`voice:newsletter`,
  `voice:linkedin`, `voice:client-acme`), so voices never leak into each other.
- **Recall-first.** Before writing a single sentence, the agent recalls the channel's
  rules, banned list, and before/after examples — so it starts every session already
  knowing how you write.
- **Signal vs. noise.** It only stores **durable** voice signals ("I always prefer short
  sentences"), never one-off edits ("shorten this paragraph"). When unsure, it asks.
- **Three structured memory types.** `[RULE]`, `[BANNED]`, and `[EXEMPLAR]` (before→after),
  each in a fixed format so memories stay searchable and de-duplicatable.
- **Append-only discipline.** Because Walrus Memory is append-only (writing the same text
  twice creates two entries, not an update), the agent recalls before writing, skips
  duplicates, and marks changed rules with `SUPERSEDES '<old rule>'` so the newest
  instruction always wins. This keeps the memory clean instead of a landfill.
- **Self-audit.** Before handing over any draft, it silently checks the draft against the
  recalled banned list and rules, fixes violations, and reports what it caught.

---

## 4. Why It Belongs in the Docs

The pain is the single most universal one for anyone writing with AI, and the prompt
demonstrates three reusable Walrus Memory patterns that apply far beyond writing:
**recall-before-act**, **namespace-per-context**, and **append-only-aware supersede**.
It's a reference implementation, not just a one-off.

---

## 5. Proof That It Works (fill in after running)

1. Create an agent/account at https://memory.walrus.xyz → get your **account ID** (agent ID).
2. Connect the Walrus Memory MCP server to your client and paste in the prompt.
3. Run 2–3 short writing sessions across two namespaces (e.g. `voice:newsletter` and
   `voice:linkedin`), giving durable corrections each time. Each session should produce
   several `remember()` writes → blobs on Walrus Mainnet.
4. Verify writes with `restore("voice:newsletter")` and `restore("voice:linkedin")`.

- **Agent ID:** `__________________________`  ← paste your Walrus Memory account ID
- **Blob count:** `______`  ← from restore()/dashboard after your sessions

> Tip: to generate a healthy, honest blob count, run the demo end-to-end twice with real
> corrections. Judges reward *consistent, meaningful* writes over a handful.

---

## 6. Demo Video Script (< 3 minutes)

**0:00–0:20 — The pain.** Show a fresh AI chat writing a generic, corporate paragraph.
"Every new session, it forgets how I write."

**0:20–0:45 — Session 1 (`voice:newsletter`).** Paste the prompt. Ask for a newsletter
intro. Correct it: "I never open with a rhetorical question — lead with a number," and
"keep sentences under 15 words." Show the agent calling `remember()` — point at the writes.

**0:45–1:10 — Append-only + supersede.** Change your mind: "actually under 12 words." Show
the agent recalling the old rule and writing a `SUPERSEDES` memory instead of duplicating.

**1:10–1:45 — Session 2, NEW chat, same channel.** Cold start. Show recall-first loading
"3 rules, 1 banned, 1 example," then a first draft that already matches your voice — with
zero re-explaining. This is the money shot.

**1:45–2:20 — Second voice (`voice:linkedin`).** Switch namespace. Show it does NOT apply
newsletter rules — voices stay isolated.

**2:20–2:50 — Self-audit + proof.** Ask for a draft; show the "Voice-check: fixed 2…" line.
Run `restore()` to show the stored memories and the blob count on Walrus.

**2:50–3:00 — Close.** Show the agent ID + total blob count on screen.

Upload the video to Walrus and paste the link into the form.

---

## 7. Submission Form Checklist

Submit at: https://walform.wal.app/f?formId=0x308876d0ae9c09d3e805580ac89ea8bd6a3eec7f5535969b267bde80ef3049d4

- [ ] The prompt (paste `voice-keeper-prompt.md` contents or a public link to it)
- [ ] Problem statement (section 2 above)
- [ ] What it does (section 3 above)
- [ ] Agent ID with writes (section 5)
- [ ] Blob count (section 5)
- [ ] Demo video link (uploaded to Walrus)
- [ ] Public link to prompt/repo/write-up
- [ ] (Optional) Referrer's Discord handle
- [ ] Post on X with #WalrusMemory tagging @WalrusProtocol

**Bonus — Bug & Improvement Bounty ($300):** while running the proof, log any friction
(append-only duplicate surprises, namespace quirks, recall relevance) as a GitHub issue at
https://github.com/MystenLabs/MemWal — that's a separate prize pool worth chasing.
