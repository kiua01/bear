# Bear + Mojo Launcher

**Mojo Launcher** (also **MJLauncher**) is an Android app that runs **Minecraft: Java Edition** on phones and tablets. It is based on PojavLauncher and supports mod loaders through **`.jar` installers** (the same path used for Fabric and Forge).

Bear is designed to **work in Mojo Launcher** as a first-class target — not only on desktop.

Official Mojo project: [MojoLauncher/MojoLauncher](https://github.com/MojoLauncher/MojoLauncher) · [mojolauncher.io](https://mojolauncher.io/)

---

## Goal

Players should be able to:

1. Install **Bear** in Mojo the same way they install Fabric/Forge (run the Bear installer `.jar`)
2. Drop Bear mods into the instance `mods/` folder
3. Launch smoothly on Android with clear errors and low overhead

---

## How Mojo installs loaders today

From Mojo’s own docs:

1. Pick a Minecraft version  
2. Download the loader **installer `.jar`**  
3. **Run the installer inside Mojo Launcher**  
4. Select **client** install → a new version/instance entry appears  
5. Add mod jars to `mods/`  
6. Play  

Bear will follow that pattern.

---

## Bear installer requirements (for Mojo)

| Requirement | Why |
|-------------|-----|
| **Single client installer `.jar`** | Mojo supports jar-only installers |
| **Writes a version profile** Mojo can see | Same as Fabric/Forge install layout |
| **No GUI-only desktop assumption** | Installer must work headless / simple CLI on Android |
| **Standard libraries + main jar layout** | Classpath must match what the game launch expects |
| **Reasonable memory defaults** | Phones are RAM-constrained |

### Installer modes

```text
java -jar bear-installer.jar client <minecraftVersion>
```

Optional:

```text
java -jar bear-installer.jar client <minecraftVersion> --dir <gameDir>
```

On Mojo, the launcher invokes the jar; Bear must not require a desktop-only UI.

---

## Runtime on Android (Mojo)

Bear should stay **fast and smooth** on mobile:

- Minimal boot work (see [PERFORMANCE.md](PERFORMANCE.md))
- Avoid heavy transforms unless a mod needs them  
- Clear OOM / crash messages (mod id + phase)  
- No assumption of high core counts or lots of RAM  

Mojo already provides:

- Android OpenJDK build  
- Graphics translation (GL4ES, LTW, Mesa, ANGLE, …)  
- Touch / gamepad input  

Bear focuses on **mod loading**, not replacing the launcher.

---

## Instance layout (expected)

```text
instances/<name>/
  .minecraft/          # or Mojo’s game dir
    mods/
      bear-api-....jar
      bear-loader-....jar
      mymod.bear.jar
    versions/
      <mc>-bear/
        ...
    bear.mod.json files inside mod jars
```

Exact folder names will match Mojo’s instance system when the installer is implemented.

---

## Mod packaging for Mojo

Same as desktop:

- Mod jar contains `bear.mod.json`  
- Entrypoints on the classpath  
- Assets under `assets/` / `data/` as usual  

Players on Mojo do **not** need a different mod format.

---

## Dev workflow (planned)

| Step | Desktop | Mojo |
|------|---------|------|
| Build mod | L / Gradle | same artifact |
| Install loader | Bear installer | Run installer jar in Mojo |
| Install mod | copy to `mods/` | copy to instance `mods/` |
| Launch | desktop MC | Mojo Play |

One mod jar → works on **PC and Mojo** when Bear is installed on both.

---

## Phased delivery

1. **Desktop Bear** loads mods (dev harness)  
2. **Installer jar** produces a launchable client profile  
3. **Verify on Mojo** (manual + community)  
4. **Tune** mobile boot (timings, memory)  
5. **Document** one-page “Bear on Mojo” player guide  

---

## Non-goals

- Forking Mojo Launcher  
- Shipping Minecraft or Microsoft auth  
- Replacing Mojo’s renderer / controls  

Bear is a **mod loader** that Mojo launches — like Fabric, but modern and L-friendly.