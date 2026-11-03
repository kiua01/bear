# Bear

**Bear** is a next-generation Minecraft mod loader: **modern**, **fast**, and **smooth**.

Designed to work hand-in-hand with the **[L](https://github.com/kiua01/L)** language — and friendly to Java/Kotlin mods as well.

> Status: **Design phase.** Implementation starts after core design is locked.

---

## Why Bear?

| Goal | What it means |
|------|----------------|
| **Modern** | Clean APIs, structured events, first-class tooling, no legacy baggage |
| **Fast** | Minimal launch overhead, parallel init, efficient classloading |
| **Smooth** | Stable lifecycle, clear errors, predictable mod order, great DX |
| **L-native** | Mods written in L feel first-class; Java remains fully supported |

Bear is **not** a Fabric/Forge fork. It is a new loader with lessons learned from the ecosystem.

---

## Pillars

1. **Simple mod format** — one manifest, clear entrypoints, no mystery flags  
2. **Fast boot** — lazy registries, parallel mod init where safe  
3. **Clean events** — typed, cancellable, priority-ordered  
4. **Registry model** — explicit, freezeable, datapack-friendly  
5. **Tooling** — CLI, Gradle plugin, L compiler integration  
6. **Safety** — sandbox options, better crash reports, version gates  

---

## Quick vision (mod in L)

```l
pkg com.example.coolmod

obj CoolMod : BearMod {
  ovrd fn onInit(ctx: BearContext) {
    println("Loaded on Bear!")
    reg.block("coolmod:smooth_stone") { }
  }
}
```

Java-style entrypoint will also be supported.

---

## Docs

| Doc | Description |
|-----|-------------|
| [Goals](docs/GOALS.md) | Goals & non-goals |
| [Architecture](docs/ARCHITECTURE.md) | Loader architecture |
| [Mod Format](docs/MOD_FORMAT.md) | `bear.mod.json` and layout |
| [Lifecycle](docs/LIFECYCLE.md) | Init phases |
| [API Sketch](docs/API.md) | Core API surface |
| [Performance](docs/PERFORMANCE.md) | Speed strategy |
| [Roadmap](ROADMAP.md) | Phases |
| [Relation to L](docs/L_AND_BEAR.md) | How L + Bear fit |

---

## Relation to Fabric

The **L** language currently targets **Fabric** so mods can ship today.

**Bear** is the long-term native loader for L (and others). Migration paths will be documented when APIs stabilize.

---

## License

MIT