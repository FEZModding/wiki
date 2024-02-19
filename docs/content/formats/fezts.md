# FEZTS format

FEZ's `TrileSet` asset type is converted by Repacker into `.fezts` file bundle. This file bundle consists of four file types:

- `.obj` - Wavefront OBJ file containing geometry of all triles in a trile set.
- `.png` - PNG image containing an atlas for cubemap albedo textures of all triles in a trile set.
- `.apng` - Optional PNG image containing an atlas of cubemap emission mask of all triles in a trile set.
- `.json` - JSON file containing information about trile set and its triles.

The purpose of these files is explained in more details in the [Trixel Art Conversion Specification](/wiki/content/trixel_art_conversion) page.

## OBJ data

Apart from properties explained in the Trixel Art conversion specification, Trile Sets contain each individual trile as a separate object with a name representing an ID of the trile.

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
|CubemapPath|String|Name of the cube map texture used to render the trile.|
|Size|[Vector3](#vector3)|In-game size of a trile.|
|Offset|[Vector3](#vector3)|In-game offset position from trile emplacement.|
|Immaterial|Boolean|If true, Gomez can pass through this block. Usually used for decorative triles.|
|SeeThrough|Boolean|If true, the camera can render whatever is behind the trile through its transparent spots.|
|Thin|Boolean|If true, the trile is thin. TODO.|
|ForceHugging|Boolean|If true, the trile will "hug" (snap to) the nearest trile.|
|Faces|[FaceRender](#facerender)|How the Trixel engine should render certain faces of the trile.|
|Type|String|What Gomez can modify about this trile (bounce on it like a mushroom, unlock it like a door...).|
|Face|[FaceOrientation](#faceorientation)|Initial facing direction for the trile.|
|SurfaceType|String|Determines the footsteps sound effect to play when the player lands on this trile. Must be either **Grass**, **Metal**, **Stone**, or **Wood**.|
|AtlasOffset|[Vector2](#vector2)|X and Y offsets for the image, describing where the trile's six-faced texture begins.|

### Vector3

Geometry structure containing X, Y and Z coordinates. It's stored as an array of three floating point numbers, simirarly to how GeoJSON does it.

### FaceRender

Structure defining how the Trixel engine should render specified faces of a trile(?)

|Property name|Type|Description|
|-|-|-|
|Face|[FaceOrientation](#faceorientation)|Which face to customize rendering for.|
|Render Option|[RenderOption](#renderoption)|How that rendering should be customized.|

### FaceOrientation

[Enum](#enum) specifying one of six possible trile face orientations - **Left**, **Down**, **Back**, **Right**, **Top** or **Front**.

### RenderOption

[Enum](#enum) specifiying **"None"**, **"AllSides"**, **"Immaterial"**, **"TopOnly"**, or **"TopNoStraightLedge"**. TODO.

### Vector2

Geometry structure containing X and Y coordinates. It's stored as an array of two floating point numbers, simirarly to how GeoJSON does it.

### Enum

All enums are stored as PascalCamelCase string parameters.
