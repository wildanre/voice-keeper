# Running Voice Keeper — Setup

Voice Keeper is a **system prompt for an AI agent**, not a script. It runs inside an MCP
client (Claude Desktop, Cursor, Cline) that has the Walrus Memory MCP server connected. The
agent then autonomously calls `memwal_remember` / `memwal_recall` following the prompt's rules.

> The Walrus Memory **Developer Playground** (dashboard) is only for manual SDK testing — it
> is NOT where the prompt runs. Use it to seed a few proof blobs if you like; use an MCP
> client for the real demo.

## Claude Desktop (recommended)

**1. MCP server config.** Add this to
`~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "memwal": {
      "command": "npx",
      "args": ["-y", "@mysten-incubation/memwal-mcp", "--namespace", "voice:newsletter"],
      "env": {
        "MEMWAL_SERVER_URL": "https://relayer.memory.walrus.xyz",
        "MEMWAL_WEB_URL": "https://memory.walrus.xyz",
        "MEMWAL_CLIENT_LABEL": "voice-keeper",
        "MEMWAL_NAMESPACE": "voice:newsletter"
      }
    }
  }
}
```

**2. Fully quit and reopen Claude Desktop** (Cmd+Q — a window close is not enough) so it
reloads the config. The `memwal_*` tools should appear in the tools menu.

**3. Log in.** In a new chat, ask: *"Run memwal_login."* Complete the wallet flow and
connect the same account you use on the dashboard.

**4. Load the prompt.** Paste [`voice-keeper-prompt.md`](./voice-keeper-prompt.md) as the
chat's system prompt (or as Project instructions).

**5. Use it.** Write naturally and give durable corrections, e.g.:
- "Help me draft a newsletter intro about remote work."
- "I never open with a rhetorical question — lead with a number."
- "Keep sentences under 15 words. That's a rule for all my newsletter writing."

The agent recalls first, captures durable rules with `memwal_remember`, and self-audits —
each write is a real blob on Walrus Mainnet.

**6. Get your proof.**
- Blob count: ask the agent to run `memwal_restore` for the namespace, or check the dashboard.
- **MEMWAL_AGENT_ID:** dashboard → **Delegate keys** → the **Public key** value.

## Multiple voices

The MCP server pins one namespace via `--namespace`. To run a second voice, add another
server entry (e.g. `"memwal-linkedin"` with `--namespace voice:linkedin`). For a first demo,
one namespace is enough to show recall-first, capture, supersede, and cold-start recall.

## Fastest proof (no MCP)

Dashboard → Developer Playground → step 2 (**remember**) → paste a memory in Voice Keeper
format and click Run. Each Run writes one real blob. Good for seeding proof; use Claude
Desktop for the demo video.
