# AutoRenamingTool: 26.3.x (ZP5) notes

Local fork branch of Sinytra's AutoRenamingTool (itself a fork of NeoForged's ART), used by the unofficial
Sinytra Connector 26.3 port for the Zoompack 5 modpack. All credit goes to the original authors. The
licence is unchanged. Not published.

## Change
`ClassProviderImpl.ClassInfo` collected fields into a map keyed by name with `Collectors.toMap`, so a
class declaring two fields with the same name and different descriptors (legal bytecode, common in
obfuscated code) threw `IllegalStateException: Duplicate key`. Connector hit this with Emotecraft's
bundled `game-sdk` and the whole game failed to start. Now the first field wins; ART's field lookups are
by name only.

## Building
Upstream has no git tags and the gradleutils version needs one. Locally:
`git tag 2.1 f2eaac9`, then `./gradlew publishToMavenLocal -x test -x createChangelog` with a
placeholder `build/changelog.txt` (createChangelog fails without tags). JDK 21 for Gradle; the
toolchain targets Java 8. Result: `org.sinytra:AutoRenamingTool:2.1.1-26.3.x` in `~/.m2`.

Good upstream PR candidate (one line). Once released, point Connector's `auto-renaming-tool` back to it.
