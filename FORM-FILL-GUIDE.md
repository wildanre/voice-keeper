# Voice Keeper — Panduan Isi Form Submission

Form: https://walform.wal.app/f?formId=0x308876d0ae9c09d3e805580ac89ea8bd6a3eec7f5535969b267bde80ef3049d4

Legend: ✅ = draft siap pakai (di bawah) · 🔴 = hanya kamu yang bisa isi · ⚪ = opsional

---

## Peta field form → status

| Field form | Status | Isi |
|---|---|---|
| Email | 🔴 | `mw18804@gmail.com` (atau email yang kamu pakai) |
| "Select an option" (dropdown) | 🔴 | pilih kategori yang sesuai (mis. role: non-dev/writer, atau "individual") |
| Sudah join Discord? (required) | 🔴 | join https://discord.gg/walrusprotocol dulu → pilih **Yes** |
| Discord handle | 🔴 | handle Discord kamu |
| Public link ke prompt/repo (`https://example.com`) | 🔴 (butuh publish) | lihat **"Langkah wajib: publish prompt"** di bawah |
| Explanation: apa yang prompt lakukan | ✅ | §A |
| Video demo (<3 min) | 🔴 (butuh rekam) | rekam pakai skrip di `SUBMISSION.md` §6, upload ke Walrus |
| MEMWAL_AGENT_ID | 🔴 (butuh run) | dashboard → Delegate keys → bagian **Public key** |
| Proof it works? (Yes/No) | 🔴 | **Yes** — setelah kamu jalankan & ada blob writes |
| Link proof/video (`https://example.com`) | 🔴 | URL video Walrus / link write-up |
| GitHub tickets (bug bounty) | ⚪ ✅ | §B (draft tiket — kejar prize $300) |
| Feedback developer experience | ⚪ ✅ | §C |
| Tag consent | 🔴 | setuju di-tag di pengumuman pemenang |
| Referrer? (Yes/No + Discord) | 🔴 | isi handle referrer kalau ada; kalau tidak → **No** |
| Feedback sesi | ⚪ ✅ | §D |
| Feedback DeepSurge | ⚪ ✅ | §E |

---

## Langkah wajib sebelum submit (gap yang belum lewat)

1. **Jalankan proof.** Buat akun di https://memory.walrus.xyz, sambungkan MCP server ke
   client, tempel `voice-keeper-prompt.md`, jalankan 2–3 sesi menulis dengan koreksi nyata
   di ≥2 namespace. Ini menghasilkan blob writes.
2. **Ambil Agent ID.** Dashboard → **Delegate keys** → salin bagian **Public key** = MEMWAL_AGENT_ID.
3. **Rekam video <3 menit** (skrip: `SUBMISSION.md` §6), upload ke Walrus, salin link.
4. **Publish prompt** supaya ada public link. Cara tercepat: GitHub repo publik berisi
   `voice-keeper-prompt.md` + `SUBMISSION.md`, atau GitHub Gist. Salin URL-nya untuk field
   "public link".

---

## §A — Explanation (what it remembers, when, how) — SIAP PAKAI

Voice Keeper is a system prompt that makes an AI writing agent remember the user's writing
voice across sessions with Walrus Memory, so the user never re-explains their tone from
scratch. It stores three durable memory types — [RULE] (tone, sentence length, formatting),
[BANNED] (words/phrases the user rejects), and [EXEMPLAR] (before→after rewrite examples) —
each in its own per-channel namespace (voice:newsletter, voice:linkedin, voice:client-acme).

WHAT it remembers: only durable voice signals, never one-off edits. It applies a
signal-vs-noise test ("make this shorter" = ignore; "I always prefer short sentences" =
store) and asks the user when unsure.

WHEN it writes: it recalls the full voice profile before writing a single sentence at the
start of every session, and it stores a new memory the moment the user gives a durable
correction, rejects a word, or praises a passage.

HOW it uses Walrus Memory thoughtfully: it respects the append-only model by recalling
before every write to skip duplicates, and marks changed rules with "SUPERSEDES '<old
rule>'" so the newest instruction always wins instead of piling up stale entries. Before
delivering any draft it self-audits the text against the recalled banned-list and rules,
fixes violations, and reports what it caught. The result: consistent, meaningful blob
writes and an agent that stops making the user repeat themselves.

---

## §B — GitHub tickets untuk Bug & Improvement Bounty ($300) — DRAFT

> Buat tiket di https://github.com/MystenLabs/MemWal, lalu tempel judul + link di form.
> Ini feedback asli yang kami temukan saat mendesain prompt.

**Ticket 1 — Append-only writes cause memory bloat; no dedup / upsert path.**
`remember()` is append-only, so re-storing an unchanged fact creates duplicate entries and
degrades recall precision over time. Suggest either an optional `upsert`/dedup-on-write, or
a documented `recall-before-write` helper, plus a first-class "supersede" convention so
agents can express "this replaces that" without leaving stale rows.

**Ticket 2 — Docs don't surface the append-only footgun prominently.**
The append-only + exact-string-match behavior is easy to miss and leads agents to build
landfill memories. Suggest a prominent "Designing memories" doc section covering namespacing,
recall-first, and supersede patterns — the exact patterns a good prompt has to reinvent.

---

## §C — Developer experience feedback — DRAFT (opsional)

What worked: recall-first + namespace isolation made it straightforward to keep multiple
writing voices separate, and semantic recall handled fuzzy queries well. Challenge: the
append-only model required designing an explicit supersede convention in the prompt to avoid
duplicate/stale memories — this would be smoother as a built-in feature or a documented
pattern. Missing feature: a lightweight way to list/prune memories in a namespace from the
agent side would help keep profiles clean.

---

## §D — Session feedback — DRAFT (opsional)

Clear, well-scoped challenge with strong example directions that opened up thinking without
prescribing an answer. The explicit judging emphasis on "real problem + proof of writes"
over technical flash was motivating and fair. More worked end-to-end examples (prompt →
agent ID → blob count) in the docs would lower the setup barrier for first-timers.

---

## §E — DeepSurge feedback — DRAFT (opsional)

(Isi hanya kalau kamu benar-benar memakai DeepSurge. Kalau tidak, tulis jujur:)
Did not use DeepSurge for this submission.
