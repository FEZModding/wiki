# Converted Content Specification

All content of the game is hidden behind multiple formats and a layer of compression (for more information, read [FEZ Content Formats](./FEZ Content Formats.md)), which makes them very hard to access for modders. In order to work around this, [FEZRepacker](https://github.com/FEZModding/FEZRepacker) was created to allow an easy conversion between these proprietary formats and more user-friendly ones. Additionally, Repacker is included as part of [HAT mod loader](https://github.com/FEZModding/HAT), allowing the game to directly access the content without having to convert it back to its own format, giving us a seamless modding experience.

```note
This specification explains a general approach of content conversion and a structure of converted assets. To get more detailed information about the specific asset format, consult the specific format reference.
```

## File bundles

Some asset types are converted to multiple files - for example, Art Objects are converted into a PNG, OBJ and JSON to store texture, model and properties respectively. Additionally, some of the types use common formats like JSON. In order to allow easy identification of asset type through converted file, as well as grouping of files belonging to the same asset, a concept of **file bundles** was introduced.

Repacker uses multiple extensions in a file name to identify a file. For instance, a file `bellao.fezao.png` has a primary extension `.png` which allows common softwares to easily identify it as an image file, and secondary extension of `fezao` which allows Repacker to identify it as a part of FEZ's Art Object asset. File bundles are a set of multiple files sharing common name and secondary extension. In the process of deconversion, Repacker bundles them together and converts them into a single content object that can be read by the game.

## Asset formats

All formats have been chosen to represent their in-game counterparts as accurately as possible. However, there are some differences, which are specified in details in the specifications of given format.

Here's a list of all 13 asset types handled by FEZ and file types Repacker associates them with:

|XNB content type name|Main purpose|Conversion format|
|-|-|-|
|[Texture2D](/wiki/content/formats/texture2d)|Sprites and textures|PNG images|
|[AnimatedTexture](/wiki/content/formats/animatedtexture)|Animated textures|WebP animation|
|[ArtObject](/wiki/content/formats/fezao)|3D models of art objects|Custom `.fezao` file bundle|
|[TrileSet](/wiki/content/formats/fezts)|Texture and models of level blocks (triles)|Custom `.fezts` file bundle|
|[SpriteFont](/wiki/content/formats/fezfont)|Bitmap font|Custon `.fezfont` file bundle|
|[Dictionary\[String,Dictionary\[String,String\]\]](/wiki/content/formats/fezdata)|Language texts|`.fezdata.json` JSON file|
|[Level](/wiki/content/formats/fezlvl)|Level data|`.fezlvl.json` JSON file|
|[MapTree](/wiki/content/formats/fezmap)|World map data|`.fezmap.json` JSON file|
|[NpcMetadata](/wiki/content/formats/feznpc)|NPC behaviour information|`.feznpc.json` JSON file|
|[Sky](/wiki/content/formats/fezsky)|Skybox structure|`.fezsky.json` JSON file|
|[TrackedSong](/wiki/content/formats/fezsong)|Song information|`.fezsong.json` JSON file|
|[Effect](/wiki/content/formats/fxc)|Binary XNA effect file container|Binary FNA effect file|
|[SoundEffect](/wiki/content/formats/sound)|WAV sound effect container|WAV sound file|
