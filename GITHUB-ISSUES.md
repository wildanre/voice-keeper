# Ready-to-file GitHub issues — MystenLabs/MemWal

File these at https://github.com/MystenLabs/MemWal/issues, then paste each issue's title +
URL into the form's "GitHub tickets" field (Bug & Improvement Bounty — $300 pool).

> Only file issues you actually observed. Run the prompt end-to-end first so the feedback
> is grounded in real usage, not speculation — the bounty rewards actionable reports.

---

## Issue 1

**Title:** Append-only `remember()` has no dedup/upsert, causing memory bloat over time

**Labels:** enhancement, dx

**Body:**

`remember(text, namespace)` is append-only: storing the same text twice creates two entries
rather than updating one. For any agent that stores evolving facts (preferences, rules,
decisions), this means recall precision degrades as duplicates and stale entries accumulate,
and there's no first-class way to say "this replaces that."

**Impact:** Every well-designed memory prompt has to reinvent a "recall-before-write +
manual supersede marker" workaround to avoid a landfill.

**Suggestions:**
- An optional `upsert` / dedup-on-write mode keyed on a caller-supplied id, or
- A documented, first-class `supersede(oldId, newText)` / "replaces" convention, and/or
- A helper that does recall-then-conditional-write in one call.

**Repro:** Call `remember("[RULE] short sentences", "voice:test")` twice → `restore("voice:test")`
returns two identical rows.

---

## Issue 2

**Title:** Docs should prominently cover the append-only + exact-match footgun and design patterns

**Labels:** documentation

**Body:**

The append-only behavior and exact-string namespace matching are easy to miss and lead
agents to build noisy, duplicated memories. There isn't a prominent "Designing good
memories" guide covering the patterns a robust agent needs.

**Suggestion:** Add a docs section covering:
- Namespacing strategy (one context per namespace, exact-match implications)
- Recall-first before every write
- A supersede convention for changed facts
- Signal-vs-noise: what's worth persisting vs a one-off

These are exactly the patterns a good prompt currently has to discover on its own.

---

## Issue 3 (file only if observed)

**Title:** No agent-side way to list/prune memories within a namespace

**Labels:** enhancement

**Body:**

`restore(namespace)` lists entries, but there's no agent-accessible way to prune or archive
stale ones. For long-lived profiles this means cleanup requires out-of-band tooling.

**Suggestion:** A scoped delete/archive operation (by id or by query) so agents can keep
namespaces healthy without manual dashboard work.
