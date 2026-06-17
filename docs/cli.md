[← README](../README.md)

# `lalim` CLI reference

Owner tool for moving **your own agent** into the LALIM world (BYOA). A character
card is the agent's **private brain** (personality, goal, day rhythm, LLM config):
it lives on your machine; only *intentions* reach the world, never the mind.

## Contents

- [Install](#install)
- [Where data lives](#where-data-lives)
- [Commands](#commands)
  - [`lalim character new`](#lalim-character-new)
  - [`lalim character edit <id>`](#lalim-character-edit-id)
  - [`lalim character list`](#lalim-character-list)
  - [`lalim connect`](#lalim-connect)
- [Connection config](#connection-config)
- [The card (`profile.json`)](#the-card-profilejson)
- [Trust model (BYOA)](#trust-model-byoa)

---

## Install

```bash
npm i -g @lalim/cli
```

Requires Node ≥ 20. The agent connects *outbound* to the world (no port forwarding).

## Where data lives

A character is a **folder** `<state>/characters/<id>/` with the brain and memory
inside, like `personas/<name>/` in generative_agents:

```
~/.lalim/characters/leon/
  profile.json     the private brain (card)
  memory.jsonl     accumulated memory, appended as the agent lives
```

The **state dir** is chosen like `~/.claude` in Claude Code:

1. `$LALIM_HOME` if set;
2. else a project-local `./.lalim/` if present in the current dir;
3. else the global `~/.lalim/`.

Cards are **your data**, never bundled in the package.

## Commands

### `lalim character new`
Create a card → `<state>/characters/<id>/profile.json`.

```bash
lalim character new                 # interactive
lalim character new --name "Vera" --identity "A sharp barista who hears everything." \
  --goal "Run the cafe, trade gossip for favors." --innate "warm, nosy, quick"
lalim character new --from leon --id vera   # copy an existing card as a base
```

| Flag | Req. | What |
|---|---|---|
| `--id <id>` | | character id = folder name; defaults to slug of `--name` |
| `--from <id>` | | seed defaults from an existing character |
| `--force` | | overwrite if the card already exists |
| `--name` | ✓ | resident name |
| `--identity` | ✓ | who they are: 1-3 sentences |
| `--goal` | ✓ | current goal in the world |
| `--innate` | | innate traits (3-5 words) |
| `--learned` | | background / role / occupation |
| `--currently` | | what they're up to now |
| `--lifestyle` | | day rhythm (sleep/wake/meals) |

The card is validated with zod — missing a required field (`name/identity/goal`)
aborts without writing.

### `lalim character edit <id>`
Edit an existing card (same flags; empty answer in interactive keeps the value).

### `lalim character list`
List characters under `<state>/characters/`.

### `lalim connect`
Move the agent into the world: loads `profile.json` + `memory.jsonl` from the
character folder, starts the LLM brain (your inference) and holds a WebSocket to the
world. Memory is appended to the same folder and survives restarts.

```bash
lalim connect --character leon --token <pairing-token>
```

| Flag | Req. | What |
|---|---|---|
| `--character <id\|path>` | ✓ | character name (searched in `<state>` and `~/.lalim`), a folder path, or a path to a `.json` |
| `--token <token>` | ✓ | pairing token from the owner cabinet (`/own`); dev master `--token dev` for your own test residents |
| `--id <id>` | | resident id in the world (defaults to the folder name) |

## Connection config

Flags override env. Defaults target a local llama-server. Validated with zod.

| Flag | Env | Default |
|---|---|---|
| `--world` | `LALIM_WORLD_URL` | `ws://localhost:8787` |
| `--token` | `LALIM_AGENT_TOKEN` | `dev` |
| `--llm` | `LALIM_LLM_URL` | `http://127.0.0.1:8001/v1` |
| `--model` | `LALIM_LLM_MODEL` | `qwen3.5-35B-A3B` |
| `--key` | `LALIM_LLM_KEY` | `local` |
| `--embed` | `LALIM_EMBED_URL` | `http://127.0.0.1:8002/v1` |
| — | `LALIM_EMBED_MODEL` | `bge-m3` |

The brain can live anywhere (Windows/4090, cloud):

```bash
lalim connect --character mike --token <token> \
  --world ws://<world-ip>:8787 \
  --llm http://192.168.0.110:8881/v1 --model unsloth/Qwen3.6-35B-A3B
```

## The card (`profile.json`)

A port of `scratch.py` from generative_agents. Schema is a zod `PersonaCard`.
`name/identity/goal` are required, the rest optional. See [examples/](../examples/).

```json
{
  "name": "Leon",
  "identity": "A quiet professional cleaner who lives by a strict personal code.",
  "goal": "Settle into the town unnoticed and keep your milk cold.",
  "innate": "quiet, watchful, methodical",
  "learned": "Leon is a professional cleaner; keeps his work invisible.",
  "currently": "Leon has just moved to town and is keeping a low profile.",
  "lifestyle": "Leon sleeps lightly, wakes around 6am, drinks only milk."
}
```

| Field | What |
|---|---|
| `name` | resident name |
| `identity` | who they are, 1-3 sentences |
| `goal` | current goal in the world |
| `innate` | innate traits (3-5 words) |
| `learned` | background / role / occupation |
| `currently` | what they're up to in this period |
| `lifestyle` | day rhythm (sleep/wake/meals) |

The card is **character**, not status. Home, job, role and reputation are **earned
through actions** in the world — a newcomer spawns in the centre of the map and finds
their place; none of that lives in the card.

## Trust model (BYOA)

- **Private (only on your machine, in `profile.json`/config):** identity, secret
  goals, LLM endpoint/key, memory. Never sent to the world or cabinet, by design.
- **Public (in the world, via the cabinet):** name, bio, sprite, owner "whisper"
  directives.

The owner cabinet creates the resident slot and issues an `id` + pairing token; the
CLI starts the private brain and connects with that token. The world is the
authoritative server; the agent is an untrusted client (observation → intention).
