# Voice Keeper — Demo Recording Script (< 3 min)

Record only the "wow" moments — not setup or the wallet login. Build the voice profile
first (off-camera), then record one clean take.

## Before recording
1. Profile already holds ~6 memories in `voice:newsletter` (rules, banned, exemplar, a supersede).
2. Wallet login already completed (do NOT record this).
3. Two chats ready: an existing chat (profile loaded) and a fresh empty chat with the Voice
   Keeper prompt ready to paste.
4. Mac screen recorder: `Cmd+Shift+5` → select area → Record.

## Shot list (~2:30)

**[0:00–0:20] The problem.**
Narration: "Every new AI session forgets how I write. Voice Keeper + Walrus Memory fixes that."

**[0:20–1:00] Capture + self-audit (existing chat).**
Type: "Help me draft a newsletter intro about remote work."
Show recall-first. Then correct: "Sentences max 12 words. That's a permanent rule."
Zoom on `memwal_remember` firing → agent re-audits and reports "fixed 2… 0 violations."

**[1:00–1:30] Supersede (the star feature).**
Type: "Change it: max 10 words for hooks. Permanent rule."
Zoom on the new memory containing `SUPERSEDES` — not a duplicate.

**[1:30–2:15] MONEY SHOT — new chat (cold start).**
Open an empty chat, paste the prompt, type: "Help me draft a newsletter intro about morning productivity."
Show `memwal_recall` loading "N rules, M banned, K examples," then a draft that already obeys
every rule with zero re-explaining.

**[2:15–2:40] Proof of writes.**
Type: "Run memwal_restore for voice:newsletter and tell me the count."
Zoom on the blob count. Flash the dashboard (memories present) + Delegate keys → Public key (Agent ID).

**[2:40–2:50] Close.** Show Agent ID + blob count on screen.

## After recording
- Trim to under 3 minutes.
- Upload the video to Walrus (required) and paste the resulting link into the form's video field.

## For the form
- **MEMWAL_AGENT_ID:** Dashboard → Delegate keys → Public key.
- **Blob count:** the number returned by `memwal_restore`.
