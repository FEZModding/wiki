# Creating your first asset HAT mod

This will be a guide to show you how to replace a few different assets in the game. For a great example of a more complete asset mod, check out [FezSonez](https://github.com/FEZModding/FezSonezSkin).

## Unpacking your game assets

One you have HAT installed and setup. The first thing that is needed is [FezRepacker](https://github.com/FEZModding/FEZRepacker/releases/latest) so we can see the directory structure, file names and file content which we need to match for the asset mod.

Run FezRepacker.exe to unpack all the FEZ assets into a local folder. Find your FEZ install directory and go into the folder `Content/`. Now run:

```bash
FEZRepacker.exe --unpack-fez-content . Unpacked
```

## Creating your new assets

Now navigate around the `Unpacked` folder to get a feel for where everything is. For this mod we'll modify a few example files to just demonstrate the approach.

Mayor McMayor's hat isn't green enough. Let's make it green. Go to `character animations/mayor mcmayor/` and we'll want to modify each of the `.gif` files contained to have the hat be green. This can be done through your image editor of choice, but [LibreSprite](https://libresprite.github.io/) has a lot of really nice stuff for pixel art and animation so I'd recommend it. Hold onto those files for now, we'll add them to our mod in the next step.

The mice in Villageville keep running away from Gomez, but he's friend-shaped, so let's change that. Go to `character animations/mouse/metadata.feznpc.json` and change `AvoidsGomez`'s value to `false`.

The back wall of Gomez's room is a bit too empty. Let's spice it up by modifying `background planes/gomez_house_c.png` and add some cool decoration.

The sound when you enter a door doesn't communicate how great of an achievement it is. Let's replace it with something more happy like the happy sound when Gomez gets his fez. Replace `sounds/gomez/enterdoor.wav` with `sounds/collects/collectfez.wav`. Make sure to keep the name `enterdoor.wav` since that will tell HAT what asset to replace.

## Making your asset mod

Create a new directory for your asset mod. Start by creating your `Metadata.xml` for HAT. Here is one for this example:

```xml
<Metadata>
   <Name>ExampleAssetMod</Name>
   <Description>Example asset mod.</Description>
   <Author>Gomez</Author>
   <Version>1.0</Version>
   <LibraryName></LibraryName>
   <Dependencies>
      <DependencyInfo Name="HAT" MinimumVersion="1.0"/>
   </Dependencies>
</Metadata>
```

Within this directory create a folder called `Assets/` which is where HAT will look for game assets to replace when loading in. Now lets move all those assets we created over here. If you are just copying the above, your whole mod should look something like:

```txt
ExampleAssetMod/
├── Metadata.xml
└── Assets/
    ├── background planes/
    │   └── gomez_house_c.png
    ├── character animations/
    │   ├── mayor mcmayor/
    │   │   ├── idle.gif
    │   │   ├── panic.gif
    │   │   ├── talk.gif
    │   │   └── walk.gif
    │   └── mouse/
    │       └── metadata.feznpc.json
    └── sounds/
        └── gomez/
            └── enterdoor.wav
```

Now copy this folder over to the `Mods/` folder in your FEZ install directory (doesn't matter if it's zipped or not). Now run `MONOMODDED_FEZ.exe` and you should be able to see your mod in the `Mods` menu option and (if everything went right) all your changes in-game.

## Sharing your asset mod

Create a github repository for your mod and commit your folder to it. Give it a `README.md` to tell others what it's about.

Tag your commit with a release number matching what's in `Metadata.xml`. Make a new release from that tag, add the version number in the title and some information on changes if this is not the first release. Then add a zip file of your mod folder (e.g. `ExampleAssetMod.zip`) to the `Assets` section of the release page and publish it.

Once all that's done, drop a message in the modding section of the [Fez Community Discord](https://discord.gg/wwVB86HhJz) to share your work with others.
