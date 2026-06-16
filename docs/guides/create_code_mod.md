# Creating your first code HAT mod

This guide shows how to create a small HAT mod that runs custom C# code in FEZ. For a real example of a larger code mod, see [FEZUG](https://github.com/FEZModding/FEZUG), which adds debug functionality.

Code mods are different from asset mods: instead of only replacing game assets, they include a compiled `.dll` file. HAT loads the library listed in `Metadata.xml`, creates one or more game components inside it, and runs them as part of the game's update and draw loop.

```tip
You can combine an asset and code mod together as a single mod package.
```

## Before starting

FEZ is written in C# and uses FNA, an XNA-compatible framework. HAT code mods are also written in C#, and their components inherit from XNA's `GameComponent` or `DrawableGameComponent` classes.

If you are new to XNA, [RB Whitaker's XNA tutorials](http://rbwhitaker.wikidot.com/xna-tutorials) are a useful introduction to the framework concepts used by FEZ and HAT code mods.

## Requirements

Before creating a code mod, you need:

1. A copy of FEZ with [HAT installed](/wiki/guides/hat_install).
2. The [.NET SDK](https://dotnet.microsoft.com/en-us/download).
3. A C# editor or IDE, such as Visual Studio, Rider, or VS Code.

```tip
It is useful to inspect the game code before writing a code mod. See the [game decompilation](/wiki/guides/game_decompilation) page for a short guide.
```

## Creating the project

Create a new C# class library. HAT code mods are usually built as `netstandard2.0` libraries so they can be loaded by the game.

For example, a minimal project file can look like this:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Library</OutputType>
    <TargetFramework>netstandard2.0</TargetFramework>
    <AppendTargetFrameworkToOutputPath>false</AppendTargetFrameworkToOutputPath>
  </PropertyGroup>

  <Import Project="$(ProjectDir)UserProperties.xml" />

  <ItemGroup>
    <Reference Include="FEZ">
      <!-- You can also point to vanilla executable -->
      <HintPath>$(FezDir)\HAT.exe</HintPath>
      <Private>False</Private>
    </Reference>

    <Reference Include="FezEngine">
      <HintPath>$(FezDir)\FezEngine.dll</HintPath>
      <Private>False</Private>
    </Reference>

    <Reference Include="FNA">
      <HintPath>$(FezDir)\FNA.dll</HintPath>
      <Private>False</Private>
    </Reference>
  </ItemGroup>
</Project>
```

Keep the game references as `Private` set to `False`. These files already exist next to the game executable, so the mod should not ship its own copies of `HAT.exe`, `FezEngine.dll`, or `FNA.dll`. `HAT.exe` is the patched game executable, so it can be referenced like the original `FEZ.exe` assembly.

Create `UserProperties.xml` next to the project file and point it at your local FEZ directory:

```xml
<Project>
  <PropertyGroup>
    <FezDir>C:\Program Files (x86)\Steam\steamapps\common\FEZ</FezDir>
    <MonoModDir>C:\Program Files (x86)\Steam\steamapps\common\FEZ\HATDependencies\MonoMod</MonoModDir>
    <ModOutputDir>C:\Program Files (x86)\Steam\steamapps\common\FEZ\Mods\ExampleCodeMod</ModOutputDir>
  </PropertyGroup>
</Project>
```

`MonoModDir` is only needed if your mod references MonoMod directly. `ModOutputDir` is optional. If you leave it empty, copy the build output into your mod folder manually.

## Adding code

HAT loads components in one of two ways:

1. If `Metadata.xml` contains an `Entrypoint`, HAT creates only that component.
2. If no `Entrypoint` is set, HAT uses the backwards-compatible behavior and creates every public, non-abstract class in the library that inherits from `GameComponent`.

The entrypoint approach is recommended for new code mods because it gives the mod one clear starting point. That entrypoint can then create or register any other components the mod needs.

The simplest way to create a HAT component is to inherit from `GameComponent` or `DrawableGameComponent`.

Use `GameComponent` when the mod only needs update logic. Use `DrawableGameComponent` when it also needs to draw.

```csharp
using Microsoft.Xna.Framework;

namespace ExampleCodeMod;

public class ExampleCodeMod : GameComponent
{
    public ExampleCodeMod(Game game) : base(game)
    {
    }

    public override void Initialize()
    {
        base.Initialize();
        // Your setup code goes here.
    }

    public override void Update(GameTime gameTime)
    {
        base.Update(gameTime);
        // Your per-frame code goes here.
    }
}
```

For more advanced changes, a code mod can also use services from `FezEngine`, HAT public methods, or MonoMod runtime detours.

If you need MonoMod detours, add the required MonoMod references to the project file:

```xml
<Reference Include="MonoMod.RuntimeDetour">
  <HintPath>$(MonoModDir)\MonoMod.RuntimeDetour.dll</HintPath>
  <Private>False</Private>
</Reference>

<Reference Include="MonoMod.Utils">
  <HintPath>$(MonoModDir)\MonoMod.Utils.dll</HintPath>
  <Private>False</Private>
</Reference>
```

## Creating the metadata

Create `Metadata.xml` in the root of your mod folder. The important fields for a code mod are `LibraryName`, which must match the name of the compiled DLL, and `Entrypoint`, which names the component HAT should create.

```xml
<Metadata>
   <Name>ExampleCodeMod</Name>
   <Description>Example code mod.</Description>
   <Author>Gomez</Author>
   <Version>1.0</Version>
   <LibraryName>ExampleCodeMod.dll</LibraryName>
   <Entrypoint>ExampleCodeMod.ExampleCodeMod</Entrypoint>
   <Dependencies>
      <DependencyInfo Name="HAT" MinimumVersion="2.0"/>
   </Dependencies>
</Metadata>
```

`Entrypoint` must use the fully qualified class name, including the namespace. In the example above, the namespace is `ExampleCodeMod` and the class name is also `ExampleCodeMod`.

For older mods, `Entrypoint` may be omitted. In that case, HAT loads all public `GameComponent` classes from the library.

For more details about metadata fields and dependency loading, see [HAT mod structure](/wiki/guides/hat_mod_structure).

## Native libraries

Most code mods only need a managed `.dll` file. If your mod depends on native libraries, such as a Windows `.dll`, Linux `.so`, or macOS `.dylib`, list them in `Metadata.xml` under `NativeDependencies`.

HAT selects native libraries by platform and process architecture, then loads the matching file from the mod directory or archive. For example:

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

Only add this section when your managed mod library actually calls into a native library.

## Building the mod

Build the project from your IDE or with:

```bash
dotnet build
```

After building, your mod folder should contain at least `Metadata.xml` and your compiled DLL:

```text
├── ExampleCodeMod/
│   ├── Metadata.xml
│   └── ExampleCodeMod.dll
```

If your mod depends on another library that is not already part of FEZ, HAT, or another loaded mod, place that library next to your mod DLL. If your mod also replaces assets, add an `Assets/` directory using the same layout described in [Creating your first asset HAT mod](/wiki/guides/create_asset_mod).

## Testing the mod

Copy the mod folder, or a `.zip` archive of it, into the `Mods` directory in your FEZ install. Start the game through `HAT`.

If the mod does not load, check the latest log file in the `Debug Logs` directory inside FEZ's local save folder. Also make sure:

1. `Metadata.xml` is at the root of the mod folder or archive.
2. `LibraryName` exactly matches the DLL filename.
3. `Entrypoint`, if used, exactly matches the component's fully qualified class name.
4. The DLL targets `netstandard2.0`.
5. Game assemblies referenced by the project were not copied into the mod folder.

## Sharing your code mod

Create a GitHub repository for your mod and commit the project files, source code, and `Metadata.xml`. Add a `README.md` that explains what the mod does and how to install it.

Tag your release with the same version number used in `Metadata.xml`. Create a release from that tag, attach a `.zip` file containing the built mod folder, and publish it.

Once the release is ready, you can share it in the modding section of the [FEZ Community Discord](https://discord.gg/wwVB86HhJz).
