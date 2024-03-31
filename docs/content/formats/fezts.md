# FEZTS format

FEZ's `TrileSet` asset type is converted by Repacker into `.fezts` file bundle. This file bundle consists of four file types:

- `.obj` - Wavefront OBJ file containing geometry of all triles in a trile set.
- `.png` - PNG image containing an atlas for cubemap albedo textures of all triles in a trile set.
- `.apng` - Optional PNG image containing an atlas of cubemap emission mask of all triles in a trile set.
- `.json` - JSON file containing information about trile set and its triles.

The purpose of these files is explained in more details in the [Trixel Art Conversion Specification](/wiki/content/trixel_art_conversion) page.

## OBJ data

Apart from properties explained in the Trixel Art conversion specification, Trile Sets contain each individual trile as a separate object with a name representing an ID of the trile.

Unlike Art Objects, UV coordinates of each individual trile are used as-is. This means you can customize UV projection and arrange texture atlas to your liking.

## JSON Data

`.fezts.json` files contain trile set data stored in a JSON format. This documentation presents a structure and purpose to each property in this file format. Descriptions are incomplete in some cases, and they might be incorrect due to lack of proper testing in the game itself, but that'll improve over time.

### Trileset

Top-level object stored in `.fezts.json` JSON file.

|Property name|Type|Description|
|-|-|-|
|Name|String|Name of the trile set used internally in the game.|
|Triles|[Trile](#trile)|Dictionary of definitions for each individual trile, with keys being trile IDs|

### Trile

|Property name|Type|Description|
|-|-|-|
|Name|String|Internal name for the trile.|
|CubemapPath|String|Unused, as triles use giant atlas texture. Should always be the same as `Name` property.|
|Size|[Vector3](#vector3)|In-game size of a trile.|
|Offset|[Vector3](#vector3)|In-game offset position from trile emplacement.|
|Immaterial|Boolean|If true, Gomez can pass through this block. This trile lacks any and all collision. Usually used for decorative triles.|
|SeeThrough|Boolean|If true, the camera can render whatever is behind the trile through its transparent spots.|
|Thin|Boolean|Like Immaterial, Gomez can pop through these triles, even if he is behind them. Note this property otherwise does not affect collision.|
|ForceHugging|Boolean|If true, the trile will "hug" (snap to) the nearest trile.|
|Faces|[CollisionType Dictionary](#collisiontype-dictionary)|Defines how Gomez should interfact with each face of a trile.|
|Type|[ActorType](#actortype)|Defines a type of the trile, which can give it special properties (mushroom bounce, door unlocking, bomb, etc.).|
|Face|[FaceOrientation](#faceorientation)|Initial facing direction for the trile.|
|SurfaceType|[SurfaceType](#surfacetype)|Determines the footsteps sound effect to play when the player lands on this trile.|
|AtlasOffset|[Vector2](#vector2)|X and Y offsets for the image, describing where the trile's six-faced texture begins.|

### Vector3

Geometry structure containing X, Y and Z coordinates. It's stored as an array of three floating point numbers, simirarly to how GeoJSON does it.

### CollisionType Dictionary

A Dictionary of [CollisionType](#collisiontype)s, linked to a [FaceOrientation](#faceorientation), defining how Gomez should collide with this trile when facing each direction (it's possible to create triles that can be collided with only from certain perspective orientations, like `arch` invisible platforms).

### Enum

All enums are stored as PascalCamelCase string parameters.

### FaceOrientation

[Enum](#enum) specifying one of six possible trile face orientations - **Left**, **Down**, **Back**, **Right**, **Top** or **Front**. In [CollisionType Dictionary](#collisiontype-dictionary), **Top** and **Down** are not used.

### CollisionType

[Enum](#enum) specifiying a type of a collision for a trile. Must be one of  **"None"**, **"AllSides"**, **"Immaterial"**, **"TopOnly"**, or **"TopNoStraightLedge"**.

[Click here for Renaud Bédard's explaination of collision and physics in FEZ](https://theinstructionlimit.com/behind-fez-collision-and-physics)

![collision_types.png](/wiki/assets/images/collision_types.png)

|CollisionType|Description|
|-|-|
|        AllSides  | for blocking level boundaries or obstacles. Also used for triles that can be picked up. Gomez cannot go through these triles. |
|        TopOnly   | for fall-through/climbable platforms |
|        None      | no-collide triles |
|        Immaterial| no-collide triles that DON’T make Gomez go in front of them. Mostly unused; use CollisionType `None` and set `Trile.Immaterial` instead.|
|TopNoStraightLedge| for platforms that Gomez cannot grab onto the ledge, and cannot fall through, but can stand on. (e.g., the shelves in the kitchen)|

### ActorType

[Enum](#enum) specifying a type of actor used by a Trile. Depending on a type of actor, specified object can be treated differently. A list of all actor types along with their behaviours will be provided in the future.

### SurfaceType

[Enum](#enum) specifying a surface type of a trile, changing the sound it emits when Gomez steps on it. Must be either **Grass**, **Metal**, **Stone**, or **Wood**.

### Vector2

Geometry structure containing X and Y coordinates. It's stored as an array of two floating point numbers, simirarly to how GeoJSON does it.
