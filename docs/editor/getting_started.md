---
sort: 2
---

# Getting Started

Before using the editor, you need to:

1. Obtain a copy of FEZ (preferably the PC 1.12 version, which is available on Steam or GOG).
2. Download [the stable release](https://github.com/FEZModding/FEZEditor/releases) of FEZEditor.

## Opening Assets

When you launch FEZEditor, the first thing you see is the splash screen:

![](/wiki/assets/images/editor/splash.png)

From here you can start working with assets depending on your goal:

1. **Open PAK file** - selects one of the PAK files. In this mode you cannot edit assets.

2. **Open mod assets directory** - select the `Assets` folder inside your mod directory.

3. **Open assets directory** - if you have assets extracted by FEZEditor or FEZRepacker, select the folder.

4. **Extract assets and open them** - select all 4 PAK files from the `Content` folder, then choose a destination folder. The editor will extract all files and automatically open the directory for editing.

5. **Open SaveSlot file to edit** - select the `FEZ` folder in the application data directory (the editor will open it for you).

If you're new to this, go with Option 4.

## Interface Overview

After opening a workspace, the editor would look like this:

![](/wiki/assets/images/editor/editor.png)

Here are the main elements:

- At the top left is **Main Menu**, and the **editor version** is shown on the top right.

- In the center left is the **File Browser**, which displays folders and assets in the workspace.

- On the right is the **editing area**. It shows the active editor with its toolbar, property panels, and viewport. Multiple assets can be open simultaneously, each in its own tab.

Here is an example with the level editor named Eddy:

![](/wiki/assets/images/editor/eddy.png)

## Asset Editors

In order to open an asset for editing or viewing, double-click it in the **File Browser**.

Each asset type opens its own dedicated editor or viewer. Each editor has its own proper name because:
- Giving editors names is fun.
- It gives an association of what each editor does.

Here is a list of editors and the assets each of them edits:

- [Eddy](/wiki/editor/levels) - Levels (`.fezlvl.json`)
- [Chris](/wiki/editor/triles_art_objects) - Trile Sets (`.fezts.glb`) and Art Objects (`.fezao.glb`)
- [Luke](/wiki/editor/skies) - Skies (`.fezsky.json`)
- [Jade](/wiki/editor/world_map) - World Map (`.fezmap.json`)
- [Mu](/wiki/editor/npcs) - NPC Metadata (`.feznpc.json`)
- [Diez](/wiki/editor/tracked_songs) - Tracked Songs (`.fezsong.json`)
- [Zu](/wiki/editor/sprite_fonts) - Sprite Fonts (`.fezfont.json`)
- [Po](/wiki/editor/localization) - Localization Files (`.feztxt.json`)
- [Sally](/wiki/editor/save_slots) - Save Slots (`SaveSlot*`)

Here is a list of viewers. You can use them to open resources that are edited externally:

- [Tex](/wiki/editor/animated_static_textures) - Texture assets (`.png`, `.gif`, `.fezanim`)
- [Rick](/wiki/editor/sounds) - Sounds and song loops (`.wav`, `.ogg`)

There are special cases described on separate pages:

- [Phil](/wiki/editor/diorama) - Export levels as GLTF scenes
- [FEXFX](/wiki/editor/shaders) - PC shaders (`.fxc`)
- [Scripting](/wiki/editor/scripting) - Level scripting
