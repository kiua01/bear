# Bear Performance Strategy

## Principles

1. **Do less at boot** — lazy where safe  
2. **Do work once** — cache discovery & resolution  
3. **Parallelize pure work** — never race game state  
4. **Avoid mandatory transforms** — registry mods stay lightweight  
5. **Measure** — built-in phase timings in the log  

## Boot budget (targets)

| Phase | Target overhead |
|-------|------------------|
| Discovery | &lt; 50ms for dozens of mods (SSD) |
| Resolve | &lt; 50ms typical |
| Load entrypoints | proportional to mod count |
| Init + Register | mod-owned; loader overhead minimal |

Exact numbers depend on hardware and mod set; targets guide design.

## Techniques

- Index jars (`bear.mod.json` only first) before full classpath scan  
- Parallel JSON parse  
- Shared API classloader (no duplicate API types)  
- Registry freeze avoids concurrent maps at runtime  
- Optional transform layer skipped when unused  

## Runtime smoothness

- Event bus with low allocation in hot paths  
- Tick events are opt-in  
- Networking codecs avoid needless copies  

## Profiling

Bear logs phase timings:

```
[Bear] discover 12ms | resolve 8ms | load 40ms | init 120ms | register 90ms
```

Mods can enable finer traces via config.