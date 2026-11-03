# Bear Installer (Draft)

Used on **desktop** and inside **Mojo Launcher** (Android).

## CLI

```bash
java -jar bear-installer.jar client <minecraftVersion> [--dir <gameDir>]
```

Exit codes:

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Bad args |
| 2 | Network / download failure |
| 3 | IO / permission failure |
| 4 | Unsupported Minecraft version |

## Behavior

1. Resolve Bear version for the given Minecraft version  
2. Download Bear loader + API jars  
3. Write version JSON / libraries list the launcher understands  
4. Do **not** require a graphical installer UI (Mojo runs jar installers on device)  

## Mojo notes

- Prefer small downloads  
- Resume-friendly where possible  
- Log paths clearly for phone storage layouts  

## Output

A playable “Minecraft + Bear” profile/instance the host launcher can start.