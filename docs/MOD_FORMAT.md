# Bear Mod Format

## Manifest: `bear.mod.json`

```json
{
  "schema": 1,
  "id": "coolmod",
  "version": "1.0.0",
  "name": "Cool Mod",
  "description": "Smooth stone and good vibes",
  "authors": ["You"],
  "entrypoints": {
    "main": ["com.example.coolmod.CoolMod"],
    "client": [],
    "server": []
  },
  "depends": {
    "bear": ">=0.1.0",
    "minecraft": ">=1.21"
  },
  "conflicts": [],
  "language": "l",
  "mixins": []
}
```

## Entrypoints

| Name | When |
|------|------|
| `main` | Common init |
| `client` | Client only |
| `server` | Dedicated server only |

## On-disk layout

```
coolmod.bear.jar
  bear.mod.json
  com/example/coolmod/...
  assets/coolmod/...
  data/coolmod/...
```

## L projects

The L toolchain will emit `bear.mod.json` the same way it emits `fabric.mod.json` today.

```bash
l bear-json coolmod "Cool Mod" out com.example.coolmod.CoolMod
```

(Planned in the L CLI.)