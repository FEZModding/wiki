# FEZNPC format

## Overview

`.feznpc` file contains NPC metadata stored in JSON format.

## Property definitions

### NpcMetadata

|Property name|Type|Description|
|-|-|-|
|WalkSpeed|Float|How fast this NPC can move.|
|AvoidsGomez|Boolean|If true, this NPC will attempt to flee if the player gets too close.|
|SoundPath|String|The name of the file in the `"Sounds/"` directory that will be used for values in NpcInstance.Actions (as seen in FEZLVL files) where NpcActionContent.SoundName is `null`.|
|SoundActions|[NpcAction](#npcaction)[]|The NpcActions that the SoundPath should be used should the above condition be true. (i.e., SoundPath will be used only if `NpcInstance.Actions[key].SoundName == null && SoundActions.Contains(key)`|

### Enum

All enums are stored as PascalCamelCase string parameters.

### NpcAction

[Enum](#enum) specifying NPC's action - **None**, **Idle**, **Idle2**, **Idle3**, **Walk**, **Turn**, **Talk**, **Burrow**, **Hide**, **ComeOut**, **TakeOff**, **Fly** or **Land**.

