# HAT mod structure

On startup, HAT iterates through the `Mods` directory in the main game's directory in search for valid mods. Every directory and `.zip` archive within `Mods` directory containing `Metadata.xml` file at its root is considered to be a valid mod. The name of the directory/archive is used only by the ignore/priority lists and doesn't have any other internal usage.

The `Metadata.xml` file should have the following structure:

```xml
<Metadata>
   <Name>YourModName</Name>
   <Description>Short description of your mod.</Description>
   <Author>YourName</Author>
   <Version>1.0</Version>
   <LibraryName></LibraryName>
   <Dependencies>
      <DependencyInfo Name="HAT" MinimumVersion="1.0"/>
   </Dependencies>
</Metadata>
```

`Name` tag is required and is treated as an unique case-sensitive identifier of your mod - mod loader will load only one mod with the same name (it'll choose the one with the most recent version). It doesn't have to match the name of the directory/archive the mod is placed in.

`Version` tag is also required. Mod loader compares two version strings by putting them in an alphanumberical order, however, each number is treated as a separate token, which order is determined by numberical value (this means `1.2beta` will be treated as older version to `1.11`).

`LibraryName` is used to determine a DLL library with C# assembly the mod loader will load. The library should end with `.dll` extension and should be placed in your mod's directory. This tag is optional, as your mod doesn't have to add any new logic.

`Dependencies` is a list of `DependencyInfo` tags. If your mod requires a specific version of HAT mod loader or relies on another mod, your can use these tags to prevent mod loader from loading this mod if given dependencies aren't present. It's entirely optional.

All other fields (`Description`, `Author`) are purely informational and will be displayed in the mods list menu.

## Asset mod

HAT will attempt to load all files recursively from `Assets` subdirectory of a mod (if one exists) and try to use them as in-game assets. A path relative to the `Assets` subdirectory will be used to identify specific asset. If a path and a filename matches an asset already existing in the game (in any of the `.pak` asset packages) or in any previously loaded mod, it will be overwritten.

By default, HAT expects the files to be raw asset files (XNB, OGG or FXC files) and will load them as such. However, if any of the files have matching asset formats (see 
[FEZ Asset Formats](/wiki/content/content_conversion#asset-formats)), it will additionally try to convert the raw bytes with FEZRepacker, providing a more straight-forward modding experience.

In addition to loading all files within `Assets` subdirectory, HAT will also attempt to load `Assets.pak` archive, and use all assets contained within it. Unlike files in the `Assets` directory, assets contained within the package will not be converted and are expected to be valid raw asset files.

Note that music files (stored by the game in `Music.pak` package) are handled by a separate subsystem in the game, and while it normally expects the OGG music tracks to be located in the root directory, HAT expects them to be located in the `Music` subdirectory of `Assets` directory/package of the mod. For example, in order to replace `villageville\bed` music file, new music file needs to be located at `[Mod directory]/Assets/Music/villageville/bed.ogg`.

## Custom logic mod

Mod loader loads library file given in metadata as an assembly, then attempts to create an instance of every public class inheriting from game's `IGameComponent` interface contained within loaded assembly before game initialization (before any services are created). After the game has been initialized (that is, as soon as all necessary services are initiated), it adds created instances into the list of game's components and initializes them, allowing their `Update` and `Draw` (when using `DrawableGameComponent`) to be properly executed within the game's loop.

For basic project setup, referencing `FEZ.exe` and `FezEngine.dll` should be sufficient (avoid shipping mods with copies of these files by setting "Copy Local" to "False" for both). References to other mods should be automatically resolved, assuming referenced mods have been included in Dependencies section of the mod's metadata. References to any other mod-specific external library should also be resolved by putting the library in the root directory of the mod (next to the mod's library).

More advanced game logic modifications might need more than an entry point. For that, it is recommended to use either hooks provided by auto-generated `FEZ.Hooks.mm.dll` library included in HAT or MonoMod's detours.

For help, you can see an example of already functioning custom logic mod: [FEZUG](https://github.com/Krzyhau/FEZUG).
