# FEZAO format

FEZ's `ArtObject` asset type is converted by Repacker into `.fezao` file bundle. This file bundle consists of three file types:

- `.obj` - Wavefront OBJ file containing art object's geometry.
- `.png` - PNG image containing art object's cubemap albedo texture.
- `.apng` - Optional PNG image containing art object's cubemap emission mask.
- `.json` - JSON file containing art object's additional information.

JSON file should contain these four properties:

|Property name|Type|Description|
|-|-|-|
|Name|String|Name of the art object. Usage is unknown, as the game uses the asset name for loading.|
|Size|Vector3|Extends from origin of this art object's boundaries.|
|ActorType|ActorType Enum|Actor type of this art objects. Used to handle special game logic.|
|NoSihouette|Boolean|Determines whether Gomez's silhouette should be rendered on top of this art object. Yes, there's a typo in the name.|

An example JSON file looks like this:

```json
{
  "Name": "1_BIT_DOORAO",
  "Size": [4, 4, 4],
  "ActorType": "OneBitDoor",
  "NoSihouette": false
}
```

## OBJ geometry

OBJ file should be a valid Wavefront OBJ model. Because of how the game stores model data, certain parameters cannot be converted one-to-one. Here are all important notes related to model conversion:

- Vertex positions are converted with no change.
- Faces are expected to be triangulated.
- Normals are replaced with the nearest cardinal direction, resulting in only six possible normal vectors. It doesn't affect surface rendering (angled surfaces work properly) and is mostly used to cubemap projection, which will be explained later on.
- Texture coordinates are unused and instead the game calculates own texture coordinates for the art object geometry based on its cubemap algorithm, which will be explained later on. Repacker attempts to replicate this behaviour on conversion process.
- Multiple objects in the file are not supported - converter will only save the first one in the file and ignore the rest.
- All other properties (groups, materials, line segments etc.) are ignored.

## Cubemap textures

In the original form, FEZ stores cubemap as a single texture, with emission map encoded into alpha channel. Repacker splits those into two files:

- PNG file contains Art Object's cubemap albedo texture. Alpha channel is not used, meaning it's not possible to create triles with transparent texture.
- APNG file contains Art Object's cubemap grayscale emission mask. Only red channel is used by Repacker.

The cubemap is made of six images with equal size arranged horizontally, each representing a different side of a cubemap in a following order: front, right, back, left, top and bottom. The game uses vertex normal vector to determine which side of a cubemap to use, and then projects vertex position onto the corresponding wall of an art object's bounding box - which is determined by `Size` property in JSON file - to calculate texture coordinates. That's why, in order to maintain an uniform size of pixels on all sides, it is recommended to use the same size on all axes.

To better illustrate the process of cubemap projection, here's an example cubemap texture of a model:

![ao1.png](/wiki/assets/images/ao/ao1.png)

Here's an image of a geometry which uses this cubemap texture:

![ao2.png](/wiki/assets/images/ao/ao2.png)

Boundaries of this art objects are defined as [4,4,4]. You can imagine a cubemap being a cube with such dimensions extending from origin:

![ao3.png](/wiki/assets/images/ao/ao3.png)

This cubemap is then projected on top of the geometry. Notice how faces which are behind other faces along their normal vector have the same texture (like the grass) as a result of the projection:

![ao4.png](/wiki/assets/images/ao/ao4.png)

Understanding this projection process is essential in order to create a cubemap texture that will be displayed on top of the model in the game properly. If you don't want to UV map your custom geometry manually, convert your model through Repacker into XNB assset and then back into FEZAO file bundle - this way you can let Repacker automatically handle the projection.

For those who bothered looking into this wiki page, here's an Art Object of Suzanne the monkey in Villageville as a reward:

![monke.png](/wiki/assets/images/ao/monke.png)
