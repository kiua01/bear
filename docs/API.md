# Bear API Sketch

## Entrypoint

```java
public interface BearMod {
    void onInit(BearContext ctx);
    default void onRegister(RegistryContext registries) {}
    default void onPostInit(BearContext ctx) {}
}
```

L form:

```l
obj CoolMod : BearMod {
  ovrd fn onInit(ctx: BearContext) { }
  ovrd fn onRegister(registries: RegistryContext) { }
}
```

## Context

```java
public interface BearContext {
    ModContainer mod();
    Logger logger();
    Path configDir();
    EventBus events();
    Network network();
}
```

## Events

```java
bus.on(PlayerJoin.class, event -> { ... });
bus.on(ServerTick.class, event -> { ... }, Priority.NORMAL);
```

Events are typed. Cancelable events expose `cancel()`.

## Registry

```java
registries.blocks().register(id("cool_stone"), new Block(...));
```

After Freeze, registration throws.

## Networking

```java
network.play().register(MyPayload.TYPE, MyPayload.CODEC, handler);
```

Prefer codec-based payloads over raw buffers for new code.

## Config

Simple typed config API in Bear API; file format TBD (JSON/TOML).