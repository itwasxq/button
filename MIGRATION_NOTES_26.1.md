# Inventory Buttons 26.1 source-port notes

This package is a best-effort source migration of `afranz29/Inventory-Buttons` from the 1.21.11 Yarn/intermediary build to the Minecraft 26.1 unobfuscated runtime.

## What was changed

- Gradle plugin changed from `net.fabricmc.fabric-loom-remap` to `net.fabricmc.fabric-loom`.
- Yarn mappings dependency was removed, because Minecraft 26.1 no longer uses the old obfuscated/intermediary runtime path.
- Dependencies were changed from `modImplementation` to `implementation` for Fabric 26.1 style builds.
- Java target changed from 21 to 25.
- `fabric.mod.json` now targets Fabric Loader `>=0.19.3`, Minecraft `>=26.1 <=26.1.2`, Java `>=25`, and client environment.
- Source imports were moved toward the 26.1/official names, including `Screen`, `GuiGraphics`, `Component`, `Identifier`, `DataComponents`, `BuiltInRegistries`, `ItemStack`, `Items`, and `AbstractContainerScreen`.
- Fabric client command import was changed from `ClientCommandManager` to `ClientCommands`.
- Mixins now target `AbstractContainerScreen` and use official field names: `leftPos`, `topPos`, `imageWidth`, `imageHeight`.
- The old `drawMouseoverTooltip` injection target was changed to `renderTooltip`.
- Player head profile construction was changed to use `GameProfile#getProperties()` and `ResolvableProfile`.

## Build steps

Use Java 25. Then run:

```bash
./gradlew clean build
```

On Windows:

```bat
gradlew.bat clean build
```

The intended jar output should be under:

```text
build/libs/
```

Remove any old `inventorybuttons-1.2.0-26.1-metadata-unlocked.jar` from your `mods` folder before testing this build.

## Not locally verified

This environment could not compile the project because it has no internet access to download Gradle/Minecraft/Fabric dependencies and only Java 21 is installed here. If compilation still fails, the most likely remaining fixes are method/field signature differences around `GuiGraphics`, `EditBox`, `ResolvableProfile`, or `AbstractContainerScreen#renderTooltip`.
