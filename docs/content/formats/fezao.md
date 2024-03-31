# FEZAO format

FEZ's `ArtObject` asset type is converted by Repacker into `.fezao` file bundle. This file bundle consists of four file types:

- `.obj` - Wavefront OBJ file containing art object's geometry.
- `.png` - PNG image containing art object's cubemap albedo texture.
- `.apng` - Optional PNG image containing art object's cubemap emission mask.
- `.json` - JSON file containing art object's additional information.

The purpose of these files is explained in more details in the [Trixel Art Conversion Specification](/wiki/content/trixel_art_conversion) page.

## JSON Properties

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

```note
ArtObjects have no collision themselves, but instead have invisible collision triles placed into the level at the same location
```

## OBJ geometry

Apart from properties explained in the Trixel Art conversion specification, Art Objects ignore all of the additional objects contained within the OBJ file, and only use the first one.

UV coordinates of the object is completely ignored, and instead is recalculated by the game when it's loaded, using cubemap projection process explained in the [Trixel Art Specification](/wiki/game/trixels) page. Repacker does this job automatically when deconverting an asset.
