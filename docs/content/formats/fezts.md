# FEZTS format

## Overview

`.fezts.json` files contain trile set data stored in a JSON format. This documentation presents a structure and purpose to each property in this file format. Descriptions are incomplete in some cases, and they might be incorrect due to lack of proper testing in the game itself, but that'll improve over time.

## Format differences
Unsure. Ask the FEZRepacker team!

## Property definitions

### Trileset
Top-level object stored in `.fezts.json` JSON file.

|Property name|Type|Description|
|-|-|-|
|Name|String|Name of the trile set used internally in the game.|
|Triles|[Trile](#trile)|Definitions of each individual trile.|

### Trile

|Property name|Type|Description|
|-|-|-|
|Name|String|Internal name for the trile.|
|CubemapPath|String|Name of the cube map texture used to render the trile.|
|Size|[Vector3](#vector3)|In-game size of a trile.|
|Offset|[Vector3](#vector3)|In-game offset position from trile emplacement.|
|Immaterial|Boolean|If true, Gomez can pass through this block. Usually used for decorative triles.|
|SeeThrough|Boolean|If true, the camera can render whatever is behind the trile through its transparent spots.|
|Thin|Boolean|If true, the trile is thin. Not sure what this means.|
|ForceHugging|Boolean|If true, the trile will "hug" (snap to) the nearest trile.|
|Faces|[FaceRender](#facerender)|How the Trixel engine should render certain faces of the trile.|
|Type|String|What Gomez can modify about this trile (bounce on it like a mushroom, unlock it like a door...).|
|Face|[FaceOrientation](#faceorientation)|Initial facing direction for the trile.|
|SurfaceType|String|What type of surface the trile is. Not sure what this means.|
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

[Enum](#enum) specifiying **"None"**, **"AllSides"**, or **"TopOnly"**. Not sure what these mean.

### Vector2

Geometry structure containing X and Y coordinates. It's stored as an array of two floating point numbers, simirarly to how GeoJSON does it.

### Enum

All enums are stored as PascalCamelCase string parameters.
