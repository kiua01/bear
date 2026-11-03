# Bear Architecture (Draft)

## Layers

```
┌─────────────────────────────────────────┐
│  Mods (L / Java / Kotlin)               │
├─────────────────────────────────────────┤
│  Bear API (events, registry, networking)│
├─────────────────────────────────────────┤
│  Bear Core (discover, load, lifecycle)  │
├─────────────────────────────────────────┤
│  Transform layer (optional bytecode)    │
├─────────────────────────────────────────┤
│  Minecraft + JVM                        │
└─────────────────────────────────────────┘
```

## Core components

| Component | Role |
|-----------|------|
| **Discovery** | Find mods in `mods/` and classpath |
| **Resolver** | Dependency & version resolution |
| **Classloader** | Isolated + shared layers for speed |
| **Lifecycle** | Ordered init phases |
| **Registry** | Content registration + freeze |
| **Events** | Typed bus |
| **Networking** | Simple payload channels |
| **Diagnostics** | Structured logging & crashes |

## Design choices

- **Explicit phases** — no “random static init” as the main API  
- **Parallel where safe** — discovery and pure registration can parallelize  
- **Freeze registries** — after bootstrap, registries become immutable  
- **Thin core** — gameplay helpers live in libraries, not the loader kernel  

## Classloading sketch

- **Parent** — Minecraft + Bear API  
- **Mod layer** — each mod or mod group  
- Shared API packages stay in the parent for performance and type identity  

## Optional transforms

ASM/Mixin-style transforms are supported as a **plugin layer**, not required for registry-only mods. That keeps simple mods fast and easy.