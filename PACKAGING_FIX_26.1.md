# 26.1 packaging fix

The previous GitHub Actions build was marked successful but produced an empty jar:
only `META-INF/MANIFEST.MF` and the license were packaged.

Reason: the mod uses `loom { splitEnvironmentSourceSets() }`, and all actual Java
sources are under `src/client/java`. Gradle's default `jar` task packages only
`sourceSets.main` unless `sourceSets.client.output` is added explicitly.

This package fixes `build.gradle` by adding:

```gradle
jar {
    from(sourceSets.client.output)
}

tasks.named('sourcesJar') {
    from(sourceSets.client.allSource)
}
```

After GitHub Actions succeeds, the real mod jar should be much larger than 3 KB
and should contain `fabric.mod.json` plus `com/panda/inventorybuttons/...` class files.
