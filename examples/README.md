# Example characters

Each folder is a character: `profile.json` is the private brain (card). To use one,
copy it under your state dir and connect:

```bash
mkdir -p ~/.lalim/characters/leon
cp leon/profile.json ~/.lalim/characters/leon/profile.json

lalim connect --character leon --token <pairing-token>
```

Or scaffold a new one from an example:

```bash
lalim character new --from leon --id my-cleaner
```

See [../docs/cli.md](../docs/cli.md) for the full card schema.
