# Changelog

All notable changes to `@lalim/cli`. Auto-generated from commits on release.

## 0.1.0 — 2026-06-21

- feat(web): наблюдаемость памяти — типы, фильтры, граф «Знает»
- feat(cognition): port perceive att_bandwidth+retention + per-persona params
- fix(web): roster shows first name only + model tag (was overflowing)
- docs: map.md — the_ville structure, layers, connectivity, Tiled + Tiled MCP
- fix(map): main component = building cluster (by object count), not largest area
- fix(movement): align with generative_agents — tile overlap + committed path, drop band-aids
- fix(agent): anti-stuck backoff + raise LLM timeout
- feat: in-media-res opening — spread spawn + 08:00 start
- feat: 'bun run cast' — launch whole cast in one command
- docs: founding-cast + living_area across docs and root README
- feat(server): seed spawn-at-home for founding cast
- feat(server): seed-cast — pre-register founding cast (public bio/sprite/token)
- docs: wall-clip diagnosis — collision correct, fix A (block Wall) seals buildings, fix B (y-depth) is the real cosmetic fix
- feat(persona): restore living_area + honor home/routine (founding cast)
- feat(plan): react to conversations — planning thought + replan (step 5)
- fix(plan): don't leak emoji-placeholder 'E' into activities
- docs: mark plan.py chain ported (steps 3a-3d) in backlog
- feat(plan): task_decomp + revise_identity (steps 3c, 3d)
- feat(plan): hierarchical day planning — wake_up + daily_req + hourly (step 3b)
- feat(plan): resolve activity address to object (step 3a) + split brain into modules
- feat(spatial): port spatial_memory MemoryTree (step 2)

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

