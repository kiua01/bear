# L and Bear

## Relationship

| Project | Role |
|---------|------|
| **[L](https://github.com/kiua01/L)** | Language + compiler |
| **Bear** | Mod loader runtime |

L currently ships Fabric support so authors can target production loaders **today**.

Bear is the **native** long-term home for L mods:

- `bear.mod.json` generation from L CLI  
- Entrypoints mapped from L `obj` + `onInit`  
- Registry DSL lowers directly to Bear registry APIs  
- Dual vocabulary (`fn` / `ret` / `obj`) works unchanged  

## Migration path (planned)

1. Write mods in L against Fabric (now)  
2. Bear API stabilizes  
3. L adds `l bear-json` + Bear backend  
4. Optional compatibility shims where feasible  

## Why not only L?

Bear stays language-agnostic at the JVM level. Java and Kotlin mods are first-class. L gets the best integrated DX.