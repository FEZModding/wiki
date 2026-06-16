# Game decompilation

Before creating a code mod, it is useful to inspect the game's assemblies with a .NET decompiler. FEZ is written in C#, so you can use [ILSpy](https://github.com/icsharpcode/ILSpy), which can show and produce mostly readable C#-like code from the compiled game files.

```note
The game code is not obfuscated.
```

Decompilation is mainly a reference tool. Use it to understand how the game is structured, which services and components already exist, and which methods are useful to call or patch.

```warning
Do not redistribute decompiled game code as part of your mod or repository!
```

## Files to open

Open the assemblies from the FEZ install directory. The most useful files are:

| File            | Contents        |
| --------------- | --------------- |
| `FEZ.exe`       | Main game code. |
| `FezEngine.dll` | Trixel engine.  |
| `Common.dll`    | Common helpers. |

```tip
In ILSpy, use `C# 5.0 / VS 2012` for more accurate decompilation results.
```

## What to look for

Start with the type or system you want to change. For example, if your mod affects menus, search for menu components. If it affects rendering, search in rendering-related classes in `FezEngine.dll`. If it affects level data, search for the relevant level, trile, volume, or art-object types.

Useful things to note while browsing:

1. Class names and namespaces.
2. Public services exposed through `ServiceDependency`.
3. Methods that can be called directly from your mod.
4. Methods that may need a MonoMod detour.
5. The order in which components initialize, update, and draw.

```warning
Decompiled code is not guaranteed to look exactly like the original source. Some variable names may be generic, compiler-generated code may appear in some places, and control flow can look more complicated than the original code was. Treat it as a map of the compiled behavior, not as a perfect copy of the original project!
```

## Finding services

Many FEZ systems are accessed through services. In decompiled code, service fields usually look like this:

```csharp
[ServiceDependency]
public ILevelManager LevelManager { private get; set; }
```

A code mod can use the same pattern in a `GameComponent` or `DrawableGameComponent`. HAT adds the component to the game after services are available, so service dependencies can be filled before your component starts running.

## Finding patch targets

If calling public APIs is not enough, inspect the method you want to change and decide whether it is a good patch target. A good target is usually small, specific, and close to the behavior you want to modify.

For runtime patches, HAT mods commonly use MonoMod detours.

Avoid patching broad methods unless there is no better option. Large methods are harder to reason about and more likely to conflict with other mods.

## Using the information in a code mod

After finding the classes and methods you need, return to [Creating your first code HAT mod](/wiki/guides/create_code_mod) and set up the mod project. Use the decompiled assemblies as references for names, types, and behavior, but write your mod as a separate project with its own source code.
