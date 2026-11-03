# Bear Lifecycle

## Phases (in order)

1. **Discover** — scan mods, read manifests  
2. **Resolve** — dependencies, conflicts, version gates  
3. **Load** — construct classloaders, load entrypoint classes  
4. **PreInit** — early hooks (config, mixins applied if any)  
5. **Init** — main entrypoints (`BearMod.onInit`)  
6. **Register** — content registration (blocks, items, …)  
7. **Freeze** — registries lock  
8. **PostInit** — cross-mod wiring  
9. **Ready** — game continues to title / server start  

Client-only and server-only entrypoints run in parallel tracks after common Init where possible.

## Rules

- Mods must not assume registry writes after **Freeze**  
- Failures in Resolve abort with a clear dependency report  
- Init failures name mod id + phase + exception  

## Parallelism

| Phase | Parallel? |
|-------|-----------|
| Discover | Yes |
| Resolve | No (global graph) |
| Load | Limited |
| Init | Optional, if mod opts in and has no hard deps pending |
| Register | Batched, deterministic order by mod id |
| Freeze | No |

Determinism beats maximum parallelism when they conflict.