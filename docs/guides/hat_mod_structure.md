# HAT mod structure

HAT loads mods from the `Mods` directory in the FEZ install directory. A mod can be either a directory or a `.zip` archive. In both cases, `Metadata.xml` must be placed at the root of the mod.

The directory or archive name is not the mod identifier. HAT uses it only for `ignorelist.txt` and `prioritylist.txt`.

## Basic layout

A simple mod directory looks like this:

```text
├── ExampleMod/
│   ├── Metadata.xml
│   ├── ExampleMod.dll
│   ├── Assets/
```

Only `Metadata.xml` is required for HAT to recognize the mod. The other files depend on the mod type:

1. Asset mods use `Assets/` or `Assets.pak`.
2. Code mods use a managed `.dll` file referenced by `LibraryName`.
3. Mixed mods can include both code and assets.

## Metadata

`Metadata.xml` describes the mod and tells HAT what to load.

```xml
<Metadata>
   <Name>YourModName</Name>
   <Description>Short description of your mod.</Description>
   <Author>YourName</Author>
   <Version>1.0</Version>
   <LibraryName>YourModName.dll</LibraryName>
   <Entrypoint>YourModName.YourModComponent</Entrypoint>
   <Dependencies>
      <DependencyInfo Name="HAT" MinimumVersion="2.0"/>
   </Dependencies>
</Metadata>
```

`Name` is required. It is the mod's unique identifier and is compared case-sensitively. If multiple loaded mods use the same name, HAT keeps the newest version.

`Version` is required. HAT parses it as a .NET `Version`, so use numeric versions such as `1.0`, `1.2.3`, or `2.0.0.0`.

`Description` and `Author` are informational and are shown in the mods menu.

`LibraryName` is optional. If set, it must point to a `.dll` file at the root of the mod. HAT loads that file as the mod's managed assembly.

`Entrypoint` is optional, but recommended for code mods. It must be the fully qualified name of a public `GameComponent` class in the managed assembly. If it is omitted, HAT uses the backwards-compatible behavior and loads every public, non-abstract `GameComponent` class in the assembly.

`Dependencies` is optional, but code mods should declare a HAT dependency. If the dependency is missing, HAT assumes `HAT` version `1.0` for compatibility with older mods. For other mods, add a `DependencyInfo` entry with the dependency mod's `Name` and, if needed, `MinimumVersion`.

## Native Dependencies

If a code mod depends on native libraries, list them with `NativeDependencies`.

```xml
<NativeDependencies>
   <NativeLibrary Architecture="X86" Platform="Windows">
      bin\win-x86\example.dll
   </NativeLibrary>
   <NativeLibrary Architecture="X64" Platform="Linux">
      bin\linux-x64\libexample.so
   </NativeLibrary>
   <NativeLibrary Architecture="X64" Platform="OSX">
      bin\osx\libexample.dylib
   </NativeLibrary>
</NativeDependencies>
```

HAT selects the entry that matches the current platform and process architecture, then loads the native library from the mod directory or archive.

Valid `Platform` values are `Windows`, `Linux`, and `OSX`. Valid `Architecture` values are `X86`, `X64`, `Arm`, and `Arm64`.

## Asset Mods

Asset mods place replacement or additional assets under `Assets/`. HAT uses the path relative to `Assets/` as the asset path. If the path matches an existing asset from the game or an earlier loaded mod, the new asset replaces it.

For example:

```text
├── ExampleAssetMod/
│   ├── Metadata.xml
│   ├── Assets/
│   │   └── background planes/
│   │       └── gomez_house_c.png
```

HAT can load raw asset files such as `.xnb`, `.ogg`, and `.fxc`. It can also convert supported source formats through FEZRepacker.Core before loading them.

HAT also supports an `Assets.pak` file at the root of the mod. Assets inside `Assets.pak` are loaded directly and are expected to already be valid raw assets.

Music is handled specially. To replace a music track, place the `.ogg` file under `Assets/Music/` and keep the path relative to the game's music path. For example, to replace `villageville\bed`, use:

```text
├── ExampleAssetMod/
│   ├── Assets/
│   │   └── Music/
│   │       └── villageville/
│   │           └── bed.ogg
```

For a step-by-step example, see [Creating your first asset HAT mod](/wiki/guides/create_asset_mod).

## Code Mods

Code mods include a managed `.dll` file at the root of the mod and set `LibraryName` in `Metadata.xml`.

HAT loads the assembly, creates the selected `GameComponent` instances, and adds them to the game after the game's services are available. Components can inherit from `GameComponent` for update logic or `DrawableGameComponent` for update and draw logic.

New code mods should use `Entrypoint` to select one public component:

```xml
<LibraryName>ExampleCodeMod.dll</LibraryName>
<Entrypoint>ExampleCodeMod.ExampleCodeMod</Entrypoint>
```

If `Entrypoint` is omitted, HAT loads every public, non-abstract `GameComponent` class from the assembly.

For project setup and a minimal component example, see [Creating your first code HAT mod](/wiki/guides/create_code_mod).

## Dependency and Load Order

HAT resolves mod dependencies before loading mods. If a dependency is missing, has a version older than `MinimumVersion`, or is part of a circular dependency, the dependent mod is not loaded.

Dependencies also affect load order: a dependency is loaded before the mod that requires it. `prioritylist.txt` can influence the order of otherwise unrelated mods. `ignorelist.txt` can exclude directories or `.zip` archives from loading.

Because assets can replace earlier assets, load order matters for mods that edit the same files.
