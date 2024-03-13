# FEZSKY format

## TODO

## Overview

`.fezsky` file contains sky metadata stored in JSON format.

## Property definitions

### Sky

|Property name|Type|Description|
|-|-|-|
|Name|String|The unique name of the sky. This should be the same as the folder name containing all the sky assets for this sky.|
|Background|String|The name of the texture2d file to use for the background.|
|WindSpeed|Float|TODO|
|Density|Float|Multiplier affecting the number of Clouds in the sky.|
|Layers|[SkyLayer](#skylayer)[]|The sky layers.|
|Clouds|String[]|The names of the texture2d files to use for the clouds.|
|Shadows|String|If not null, the name of the texture2d file to use for the shadows.|
|Stars|String|If not null, the name of the texture2d file to use for the stars.|
|CloudTint|String|If not null, the name of the texture2d file to use for the cloud tint.|
|VerticalTiling|Boolean|TODO|
|HorizontalScrolling|Boolean|TODO|
|LayerBaseHeight|Float|TODO|
|InterLayerVerticalDistance|Float|TODO|
|InterLayerHorizontalDistance|Float|TODO|
|HorizontalDistance|Float|TODO|
|VerticalDistance|Float|TODO|
|LayerBaseSpacing|Float|TODO|
|WindParallax|Float|TODO|
|WindDistance|Float|TODO|
|CloudsParallax|Float|TODO|
|ShadowOpacity|Float|TODO|
|FoliageShadows|Boolean|TODO|
|NoPerFaceLayerXOffset|Boolean|TODO|
|LayerBaseXOffset|Float|TODO|

### SkyLayer

|Property name|Type|Description|
|-|-|-|
|Name|String|The names of the texture2d file for this sky layer.|
|InFront|Boolean|If true, this layer will always be on top.|
|Opacity|Float|The opacity of this layer.|
|FogTint|Float|TODO|

