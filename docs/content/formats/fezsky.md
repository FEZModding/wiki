# FEZSKY format

## Overview

`.fezsky` file contains sky metadata stored in JSON format. This documentation presents a structure and purpose to each property in this file format. Descriptions are incomplete in some cases, and they might be incorrect due to lack of proper testing in the game itself, but that'll improve over time.

## Property definitions

### Sky

|Property name|Type|Description|
|-|-|-|
|Name|String|The unique name of the sky. This should be the same as the folder name containing all the sky assets for this sky.|
|Background|String|The name of the texture2d file to use for the background.|
|WindSpeed|Float|Behaviour currently unknown.|
|Density|Float|Multiplier affecting the number of Clouds in the sky.|
|Layers|[SkyLayer](#skylayer)[]|The sky layers.|
|Clouds|String[]|The names of the texture2d files to use for the clouds.|
|Shadows|String|If not null, the name of the texture2d file to use for the shadows.|
|Stars|String|If not null, the name of the texture2d file to use for the stars.|
|CloudTint|String|If not null, the name of the texture2d file to use for the cloud tint.|
|VerticalTiling|Boolean|Behaviour currently unknown.|
|HorizontalScrolling|Boolean|Behaviour currently unknown.|
|LayerBaseHeight|Float|Behaviour currently unknown.|
|InterLayerVerticalDistance|Float|Behaviour currently unknown.|
|InterLayerHorizontalDistance|Float|Behaviour currently unknown.|
|HorizontalDistance|Float|Behaviour currently unknown.|
|VerticalDistance|Float|Behaviour currently unknown.|
|LayerBaseSpacing|Float|Behaviour currently unknown.|
|WindParallax|Float|Behaviour currently unknown.|
|WindDistance|Float|Behaviour currently unknown.|
|CloudsParallax|Float|Behaviour currently unknown.|
|ShadowOpacity|Float|Behaviour currently unknown.|
|FoliageShadows|Boolean|Behaviour currently unknown.|
|NoPerFaceLayerXOffset|Boolean|Behaviour currently unknown.|
|LayerBaseXOffset|Float|Behaviour currently unknown.|

### SkyLayer

|Property name|Type|Description|
|-|-|-|
|Name|String|The names of the texture2d file for this sky layer.|
|InFront|Boolean|If true, this layer will always be on top.|
|Opacity|Float|The opacity of this layer.|
|FogTint|Float|Behaviour currently unknown.|

