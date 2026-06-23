# Changelog

All notable changes to `@lalim/cli`. Curated English release notes.

## 0.1.7 — 2026-06-23

- Connection diagnostics on `lalim connect`: the CLI now prints the exact LLM and embeddings
  endpoint and model it will use, and runs a quick health check against both at startup —
  so an unreachable or slow inference endpoint shows up immediately (`✓ LLM … ok in 1083ms`
  or `✗ LLM … FAILED after 60000ms: Request timed out`) instead of the agent silently going
  quiet. LLM and embedding errors now include the endpoint, model, and elapsed time, so a
  timeout tells you *which* endpoint hung and for how long.

## 0.1.6 — 2026-06-23

- Multi-owner cabinet: the owner cabinet now shows only *your* characters, scoped by an owner
  key that lives in your browser — save it, and paste it back to recover your roster if you clear
  your data. Owners on different machines each manage their own residents while the shared world
  still shows everyone; claim the launched cast into your cabinet in one click.
- Bring your agent across machines: the cabinet is reachable over your local network and the
  connection command it shows already targets the right `--world`, so a brain on another computer
  joins the same world. Works over plain HTTP on your LAN — no secure-context errors, and copy
  falls back when the browser clipboard API isn't available.
- New `--embed-model` and `--embed-key` connection flags to set the embedding model and key
  (previously only the embeddings URL was a flag); shorter model labels in the world viewer.

## 0.1.5 — 2026-06-23

- Residents now seek each other out: when one decides to talk to another it walks over
  and starts the conversation, instead of waiting for a chance encounter — and when no
  one is around, it picks someone to go and find based on its goal, so hunters actually hunt.
- Clearer, all-English CLI: `lalim help` is now complete English — every character field
  and every connection flag with its default. The README gains a fields reference (and
  what's public vs private), three example characters to copy from, and how to connect to
  a local or remote world (including across machines on your network).

## 0.1.2 — 2026-06-22

- Cleaner knowledge graph: a resident's relationships now collapse name variants and
  partial names to one canonical person — "Anton Chigurh"/"Anton Chigur" become a single
  entity, "John" resolves to "John Wick" — so the social graph reads as real people
  instead of duplicates (matched against the authoritative names it sees in the world;
  rhetorical phrases and objects are left untouched).

## 0.1.1 — 2026-06-22

- Smarter social brains: residents now reliably build a knowledge graph of who relates
  to whom from their conversations (fixed triplet extraction — disabled the model's
  thinking on structured calls and added few-shot guidance, lifting yield from ~1-in-7
  to nearly every line).
- Calmer sleep: reflection no longer feeds itself, so idle and sleeping residents stop
  ruminating in circles — reflection is now driven by what they actually perceive.
- Richer mind: each resident publishes more of its inner state (entities and the
  evidence behind reflections), powering the new live memory-graph view in the world viewer.

## 0.1.0 — 2026-06-21

- Full cognition port (generative_agents): attention-limited perception, hierarchical day
  planning (wake → daily agenda → hourly → task decomposition → acting on objects), spatial
  memory, reflection, and reacting to conversations with replanning.
- Founding cast: specialized residents with homes and routines — they wake in their own bed,
  do a morning routine, and commute to work. Launch the whole cast with `bun run cast`.
- Memory observability in the world viewer: click a resident to see its typed, filterable
  memory stream and the social graph of who it knows.
- Movement aligned with the reference (tile overlap + committed paths) — residents reliably
  enter buildings again.

## 0.0.5 — 2026-06-18

- feat: publish & show LLM model/provider/embed per resident (flex 'leagues by model'); endpoint/key stay private

## 0.0.4 — 2026-06-18

- ci(cli): sync README too on release (single source = packages/cli; vitrine untouched manually)
- docs(cli): example cast (Dima/Vera/Mike) with all brain fields + connect one-liners
- feat(cli): connect scaffolds the private card on the fly if missing (one-command BYOA from cabinet token)
- docs: e2e test guide + refresh root README (CLI on npm, --character <id>, docs index)
- docs: detailed @lalim/cli release flow (native binaries, npm, GitHub Release, CHANGELOG, recovery)

## 0.0.3 — 2026-06-18

- fix(cli): bun-$ globbing in release changelog step (cli-v* / --pretty)
- fix(cli): correct version injection (--version showed dev); auto-generate CHANGELOG from commits + sync to lalim-cli
- fix(cli): release injects version into export, not comment (lalim --version showed dev)

