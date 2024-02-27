# Trixel Art Conversion Specification

```note
This specification explains conversion process of Trixel Arts. If you wish to know what Trixel Art is and how it's processed by the game, consult the [Trixel Art Specification](/wiki/game/trixels) page.
```

Both of content formats using Trixel Arts ([Art Objects](/wiki/content/formats/fezao) and [Trile Sets](/wiki/content/formats/fezts)) are converted to a similar file bundle, consisting of this set of files:

- `.obj` - Wavefront OBJ file containing all geometry of given asset's.
- `.png` - PNG image containing trixel art cubemap albedo texture.
- `.apng` - Optional PNG image containing trixel art cubemap emission mask.
- `.json` - JSON file containing asset's additional information.

## OBJ geometry

OBJ file should be a valid Wavefront OBJ model. Because of how the game stores model data, certain parameters cannot be converted one-to-one. Here are all important notes related to model conversion:

- Vertex positions are converted with no change.
- Faces are expected to be triangulated.
- Normals are replaced with the nearest cardinal direction, resulting in only six possible normal vectors. It doesn't affect surface rendering (angled surfaces work properly) and is mostly used to cubemap projection, which will be explained later on.
- UV coordinates are converted with no change, but Art Objects ignore them and recalculate them in a cubemap projection process explained in the [Trixel Art Specification](/wiki/game/trixels) page. Repacker will perform the same process during conversion.
- All other properties (groups, materials, line segments etc.) are ignored.
- Multiple objects in a file are interpreted differently depending on the asset type.

## Cubemap textures

In the original form, FEZ stores cubemap as a single texture, with emission map encoded into alpha channel. Repacker splits those into two files:

- PNG file contains trixel art cubemap albedo texture. Alpha channel is not used, meaning it's not possible to create triles and art objects with transparent texture.
- APNG file contains trixel art cubemap grayscale emission mask. Only red channel is used by Repacker.

## JSON file

Each asset type defines its own properties. For details, consult the page of specific format:

- [.FEZAO format](/wiki/content/formats/fezao)
- [.FEZTS format](/wiki/content/formats/fezts)
