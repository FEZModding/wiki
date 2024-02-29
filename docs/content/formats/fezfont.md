# FEZFONT format

FEZ's `SpriteFont` asset type is converted by Repacker into `.fezfont` file bundle. This file bundle consists of two files:

- `.json` - JSON file containing fonts information and font character information.
- `.png` - PNG image containing font's texture.

```note
The character that will be substituted when a given character is not included in the font is " " (U+0020 Space) (hardcoded into FezEngine).
This means if a font doesn't have the space character for whatever reason, the game would likely crash.
```

## JSON Data

`.fezfont.json` files contain Font data  stored in a JSON format. This documentation presents a structure and purpose to each property in this file format. Descriptions are incomplete in some cases, and they might be incorrect due to lack of proper testing in the game itself, but that'll improve over time.

## Property definitions

### SpriteFont

Top-level object stored in `.fezfont.json` JSON file.

|Property name|Type|Description|
|-|-|-|
|LineSpacing|Number|The line spacing of this font.|
|Spacing|Number|The spacing of the font characters.|
|Glyphs|[Glyph](#Glyph)[]|List of character data in this font.|

### Glyph

```note
The origin point (0,0) for all Rectangles is the top left, with Y increasing while moving downwards.

For KerningData, the left and right sides should be 0, and the width should be the same as `Cropping.Width`.

Additionally, you'd probably want `Cropping.Height` to be the same for every character, so the vertical alignment is consistent.
```

|Property name|Type|Description|
|-|-|-|
|Character|String|The character this glyph data is for.|
|GlyphBounds|Rectangle|The rectangle in the font texture containing the target character.|
|Cropping|Rectangle|The cropping rectangle, which is applied to the corresponding GlyphBounds to calculate the bounds of the actual character.|
|KerningData|Vector3|The letters kernings (X - left side bearing, Y - width and Z - right side bearing).|