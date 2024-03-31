# FEZLVL format

## Overview

`.fezlvl.json` files contain level data stored in a JSON format. This documentation presents a structure and purpose to each property in this file format. Descriptions are incomplete in some cases, and they might be incorrect due to lack of proper testing in the game itself, but that'll improve over time. Who doesn't love to experiment?

## Format differences

This format differs a little bit from how the level data is arranged in the game's structure in order to eliminate redundant and unnecessary data arrangement. Here's a list of all differences:
- [Level](#level)'s `Triles` property is a list of [TrileInstances](#trileinstance) instead of a dictionary with [TrileEmplacement](#trileemplacement) keys, which are now stored within [TrileInstance](#trileinstance) as `Position` property.
- `OverlappedTriles` property of [TrileInstance](#trileinstance) has been removed. All overlapped triles are stored in [Level](#level)'s `Triles` list.
- [TrileGroup](#trilegroup) stores a list of [TrileEmplacements](#trileemplacement) instead of an exact replica of a [TrileInstance](#trileinstance) structure.
- [Scripts](#script) have been completely changed to be stored in a more efficient syntax.

## Property definitions

### Level

Top-level object stored in `.fezlvl.json` JSON file.

|Property name|Type|Description|
|-|-|-|
|Name|String|Name of the level used internally by the game.|
|NodeType|[LevelNodeType](#levelnodetype)|Type of node used to represent level on the map.|
|Size|[Vector3](#vector3)|Size of the map.|
|StartingPosition|[TrileFace](#trileface)|Default location and camera orientation detailing where the player should start the level.|
|Flat|Boolean|If true, blocks player's ability to shift in this level.|
|Quantum|Boolean|If true, blocks are visually randomized.|
|Descending|Boolean|Behaviour currently unknown. Used only in ZU_CODE_LOOP.|
|Loops|Boolean|If true, level loops vertically.|
|Rainy|Boolean|Determines whether it should rain in the level.|
|BaseDiffuse|Float|Scale of a diffuse lighting.|
|BaseAmbient|Float|Scale of an ambient lighting.|
|SkyName|String|Name of a sky asset to use in this level.|
|SkipPostProcess|Boolean|If true, level is rendered without post-processing effects.|
|GomezHaloName|String|A name of a background plane texture used for halo effect around Gomez.|
|HaloFiltering|Boolean|Behaviour currently unknown.|
|BlinkingAlpha|Boolean|If true, the CMYK theme is used, and the world blinks to the music. See also: [TrileInstanceActorSettings](#trileinstanceactorsettings)|
|WaterHeight|Float|Height of water in this level.|
|WaterType|[LiquidType](#liquidtype)|Type of liquid to use for water in this level.|
|SongName|String|Name of the song to play.|
|MutedLoops|String[]|List of names of loops to mute in played song.|
|AmbienceTracks|[AmbienceTrack](#ambiencetrack)|List of ambience tracks to play.|
|SequenceSamplesPath|string|The subdirectory in the "Sounds" folder to look for the sound effects to play for the blinking blocks.|
|LowPass|Boolean|If true, music is put through low pass filter.|
|FAPFadeOutStart|Integer|Far Away Place fade out start. Unused.|
|FAPFadeOutLength|Integer|Far Away Place fade out length. Unused.|
|TrileSetName|String|A name of a Trile Set to use in this level.|
|Triles|[TrileInstance](#trileinstance)[]|A list of triles in this level.|
|Groups|[TrileGroup](#trilegroup)[]|A list of trile groups.|
|Volumes|[Volume](#volume)[]|A list of volumes in this level.|
|Scripts|[Script](#script)[]|A list of scripts in this level.|
|ArtObjects|[ArtObjectInstance](#artobjectinstance)[]|A list of art object instances in this level.|
|BackgroundPlanes|[BackgroundPlane](#backgroundplane)[]|A list of background planes in this level.|
|Paths|[MovementPath](#movementpath)[]|A list of paths in this level.|
|NonPlayerCharacters|[NpcInstance](#npcinstance)[]|A list of NPCs in this level.|

### Enum

All enums are stored as PascalCamelCase string parameters.

### LevelNodeType

[Enum](#enum) specifying how level should appear in the map. It can take one of three values:

- **Node**
- **Hub**
- **Lesser**

### Vector3

Geometry structure containing X, Y and Z coordinates. It's stored as an array of three floating point numbers, simirarly to how GeoJSON does it.

### TrileFace

Structure identifying location of a trile and facing direction. In FEZLVL data, it's used only to determine a default starting position.

|Property name|Type|Description|
|-|-|-|
|Id|[TrileEmplacement](#trileemplacement)|Location of the trile.|
|Face|[FaceOrientation](#faceorientation)|Facing orientation. For starting position, it can be only **Left**, **Right**, **Back** or **Front**|

### TrileEmplacement

Geometry structure containing X, Y, and Z coordinates of a trile in the map. It's stored as an array of three integer numbers.

### FaceOrientation

[Enum](#enum) specifying one of six possible trile face orientations - **Left**, **Down**, **Back**, **Right**, **Top** or **Front**.

### LiquidType

[Enum](#enum) specifying one possible water types used in levels - **None**, **Water**, **Blood**, **Lava**, **Sewer**, **Purple** or **Green**.

### AmbienceTrack

Structure specifying the name of ambience track to play and when it's played.

|Property name|Type|Description|
|-|-|-|
|Name|String|Name of an ambience track to play.|
|Day|Boolean|If true, ambience track will play during the day.|
|Dusk|Boolean|If true, ambience track will play during the dusk.|
|Night|Boolean|If true, ambience track will play during the nigty.|
|Dawn|Boolean|If true, ambience track will play during the dawn.|

### TrileInstance

Structure containing information about a single trile - a level tile in 3D space. Multiple triles may be present in the same position.

|Property name|Type|Description|
|-|-|-|
|Emplacement|[TrileEmplacement](#trileemplacement)|Location of the trile instance in 3D grid. Used as identifier.|
|Position|[Vector3](#vector3)|Real position of this trile instance in 3D space. Can be used to offset the block.|
|Phi|Byte|Rotation of this trile instance. Each increment is 90 degrees counter-clockwise.|
|Id|Integer|ID of a trile in Trile Set used by this level.|
|Settings|[TrileInstanceActorSettings](#trileinstanceactorsettings)|Additional parameters of this trile. Can be null.|

### TrileInstanceActorSettings

Structure containing additional information of a trile instance.

|Property name|Type|Description|
|-|-|-|
|ContainedTrile|int|Unused?|
|SignText|String|Language identifier of a text which appears when interacting with this trile.|
|Sequence|String|Behaviour currently unknown. Related to blinking blocks.|
|SequenceSampleName|String|Behaviour currently unknown. Same as above.|
|SequenceAlternateSampleName|String|Behaviour currently unknown. Same as above.|
|HostVolume|Integer|ID of host [Volume](#volume) into which this moveable crate will be accepted. As seen in the level ZU_4_SIDE.|

### TrileGroup

Structure containing a list of trile instances grouped together and parameters of this group.

|Property name|Type|Description|
|-|-|-|
|Triles|[TrileEmplacement](#trileemplacement)[]|List of coordinates used to determine which trile instances belong to this group.|
|Path|[MovementPath](#movementpath)|Path this group moves along|
|Heavy|Boolean|Behaviour currently unknown.|
|ActorType|[ActorType](#actortype)|Type of actor this group should be treated as.|
|GeyserOffset|Float|For the Geyser ActorType. The amount of seconds to wait before initially moving this group.|
|GeyserPauseFor|Float|For the Geyser ActorType. The amount of seconds this group will not be in the lifting state.|
|GeyserLiftFor|Float|For the Geyser ActorType. The amount of seconds this group will be in the lifting state.|
|GeyserApexHeight|Float|For the Geyser ActorType. The maximum height difference this group will reach.|
|SpinCenter|[Vector3](#vector3)|For the RotatingGroup ActorType. If it is not equal to `Vector3.Zero`, the group will rotate using this Vector3. Exact behaviour currently unknown.|
|SpinClockwise|Boolean|For the RotatingGroup ActorType. If true, will spin clockwise, otherwise will anticlockwise.|
|SpinFrequency|Float|For the RotatingGroup ActorType. The number of seconds this group waits between spins.|
|SpinNeedsTriggering|Boolean|Behaviour currently unknown.|
|Spin180Degrees|Boolean|For the RotatingGroup ActorType. If true, will spin 180 degrees, otherwise will spin 90 degrees.|
|FallOnRotate|Boolean|For the RotatingGroup ActorType. If true, Gomez will fall when the group spins, otherwise if he is holding onto the group, he will rotate with the group.|
|SpinOffset|Float|For the RotatingGroup ActorType. The amount of seconds to wait before initially spinning this group.|
|AssociatedSound|String|For the RotatingGroup ActorType. The name of the SoundEffect file in the `"Sounds/MiscActors/"` directory to play will this group spins.|

### MovementPath

Structure defining the path of movement and its properties. It's used by [Trile groups](#trilegroup) and occasionally by functions available through [Scripts](#script).

|Property name|Type|Description|
|-|-|-|
|Segments|[PathSegment](#pathsegment)[]|A list of path segments defining the path.|
|NeedsTrigger|Boolean|If true, the path needs to be triggered to function.|
|EndBehavior|[PathEndBehaviour](#pathendbehaviour)|Defines how path should behave when end is reached.|
|SoundName|String|A name of sound to use when path is in use.|
|IsSpline|Bool|If true, path uses spline interpolation.|
|OffsetSeconds|Float|Determines how long to wait until movement starts.|
|SaveTrigger|Boolean|Behaviour currently unknown.|

### PathSegment

Structure defining properties of a path segment.

```note
If both Acceleration and Deceleration are 0, the easing function is linear.
If only Acceleration is 0, the easing function is quadratic ease-out.
If both Acceleration and Deceleration are NOT 0, the easing function is sine ease-in-out.
If only Deceleration is 0, the easing function is quadratic ease-in.
```

|Property name|Type|Description|
|-|-|-|
|Destination|[Vector3](#vector3)|Destination of this path segment.|
|Duration|Float|Time it takes to traverse the segment, in seconds.|
|WaitTimeOnStart|Float|Time to wait on start of the segments, in seconds.|
|WaitTimeOnFinish|Float|Time to wait on end of the segment, in seconds.|
|Acceleration|Float|Acceleration factor. For exact behaviour, see note above.|
|Deceleration|Float|Deceleration factor. For exact behaviour, see note above.|
|JitterFactor|Float|The magnitude for how jittery/shaky this path is.|
|Orientation|[Quaternion](#quaternion)|Behaviour currently unknown.|
|CustomData|[CameraNodeData](#cameranodedata)|Contains additional camera data. Can be null.|

### Quaternion

Geometry structure containing X, Y, Z and W coordinates. It's stored as an array of four floating point numbers, simirarly to how GeoJSON does it.

### CameraNodeData

Structure containing custom information about camera movement along path.

|Property name|Type|Description|
|-|-|-|
|Perspective|Boolean|Behaviour currently unknown.|
|PixelsPerTrixel|Integer|Behaviour currently unknown.|
|SoundName|String|Behaviour currently unknown.|

### PathEndBehaviour

[Enum](#enum) specifying how path segment should end - **Bounce**, **Loop** or **Stop**.

### ActorType

[Enum](#enum) specifying a type of actor used by TrileGroup, Art Object or Background Plane. Depending on a type of actor, specified object can be treated differently. A list of all actor types along with their behaviours will be provided in the future.

### Volume

Structure defining a cuboid zone with custom properties. These zones can also be used by [Scripts](#script) for custom conditions or triggers.

|Property name|Type|Description|
|-|-|-|
|Orientations|[FaceOrientation](#faceorientation)|Orientations towards which perspective can be shifted for this Volume to work.|
|From|[Vector3](#vector3)|Coordinates of one of the corners of this volume zone.|
|To|[Vector3](#vector3)|Coordinates of another of the corners of this volume zone.|
|ActorSettings|[VolumeActorSettings](#volumeactorsettings)|Settings of this volume instance.|

### VolumeActorSettings

Structure defining settings for a volume instance.

|Property name|Type|Description|
|-|-|-|
|DotDialogue|[DotDialogueLine](#dotdialogueline)[]|List of Dot dialogues used by this volume.|
|CodePattern|[CodeInput](#codeinput)[]|Input combo used by this volume.|
|IsBlackHole|Boolean|If true, this volume is a black hole.|
|NeedsTrigger|Boolean|If true, this volume is disabled by default.|
|IsSecretPassage|Boolean|This is used for the secret shortcut doors. If true, this door will take the player to the first volume in the target level that has IsSecretPassage.|
|WaterLocked|Boolean|If the door could be underwater. Exact behaviour currently unknown.|
|IsPointOfInterest|Boolean|If true, this volume will be permanently disabled when the puzzle is completed or the chest is opened. Mainly used for Dot's tutorial text.|
|FarawayPlaneOffset|[Vector2](#vector2)|Behaviour currently unknown.|

### DotDialogueLine

Structure defining Dot dialogue.

|Property name|Type|Description|
|-|-|-|
|ResourceText|String|The key to get the localized text from the FEZDATA file.|
|Grouped|Boolean|Behaviour currently unknown.|

### CodeInput

[Enum](#enum) specifying in-game input - **None**, **Up**, **Down**, **Left**, **Right**, **SpinLeft**, **SpinRight** or **Jump**.

### Vector2

Geometry structure containing X and Y coordinates. It's stored as an array of two floating point numbers, simirarly to how GeoJSON does it.

### Script

Structure defining custom behaviour which can await certain triggers, react to specified conditions and execute defined actions with given parameters.

|Property name|Type|Description|
|-|-|-|
|Name|String|Name of the script. Presumably unused.|
|Timeout|Boolean|A time after which the script should be terminated, in seconds.|
|Triggers|[ScriptTrigger](#scripttrigger)[]|A list of triggers this script can react to.|
|Conditions|[ScriptCondition](#scriptcondition)[]|A list of conditions that has to be met for this script to be executed.|
|Actions|[ScriptAction](#scriptaction)[]|A list of actions this script will execute.|
|OneTime|Boolean|If set, this script will execute only once.|
|Trigerless|Boolean|Behaviour currently unknown.|
|IgnoreEndTriggers|Boolean|Behaviour currently unknown.|
|LevelWideOneTime|Boolean|Behaviour currently unknown.|
|Disabled|Boolean|If set, this script will be disabled until enabled by another script.|
|IsWinCondition|Boolean|If true, this script should be included in the [Conditions.ScriptIds\[\]](./fezmap#winconditions) for the appropriate [fezmap.MapNode](./fezmap#mapnode)|

### Script Operation

[ScriptTrigger](#scripttrigger), [ScriptCondition](#scriptcondition) and [ScriptAction](#scriptaction) are using string-encoded operations. Their syntax may vary, but they will always start with entity identifier followed by a dot. Entity identifier is simply its class name. If an entity is not static (like Level or Camera), it's followed by a square brackets [] operator containing an ID of an object (like Volume or ArtObject).

A full list of entities and their exposed triggers, properties and actions is available [at the "Scripting Reference" page](../../game/scripting).

### ScriptTrigger

[String-encoded operation](#script-operation) starting with entity identifier, followed by the name of the trigger, like so:

```js
[EntityIdentifier].[TriggerName]
```

As an example:

```js
Level.Start
```

### ScriptCondition

[String-encoded operation](#script-operation) starting with entity identifier, followed by the name of the property, one of the valid comparison operator (`==`, `>=`, `<=`, `>`, `<` or `!=`) and value literal, like so:

```js
[EntityIdentifier].[Property] [ComparisonOperator] [ValueLiteral]
```

As an example:

```js
Gomez.CollectedCubes >= 1
```

```js
Game.GetLevelState == INTRO_COMPLETE
```

### ScriptAction

[String-encoded operation](#script-operation) starting with entity identifier, followed by the name of the action and a list of parameters enclosed by parentheses and separated by commas. Additionally, operation string can be preceded by two control characters:

- `#` - blocks execution of following actions until this one is completed.
- `!` - terminates the entire script once the action is executed.

Script action has following syntax:

```js
[ControlCharacters][EntityIdentifier].[ActionName]([Property1], [Property2], ...)
```

As an example:

```js
Game.Wait(1)
```

```js
#Dot.Say(DOT_CUBES_GET_A, False, False)
```

### ArtObjectInstance

Structure defining art object instance, its location and settings.

|Property name|Type|Description|
|-|-|-|
|Name|String|Name of the art object used by this instance.|
|Position|Vector3|Position of this instance.|
|Rotation|Quaternion|Rotation of this instance.|
|Scale|Vector3|Scale of this instance.|
|Scale|Vector3|Scale of this instance.|
|ActorSettings|[ArtObjectActorSettings](#artobjectactorsettings)|Settings of this art object instance.|

### ArtObjectActorSettings

Structure defining settings for art object instance.

|Property name|Type|Description|
|-|-|-|
|Inactive|Boolean|If set, this Art Object will be inactive by default.|
|AttachedGroup|Integer|Identifier of a [Trile Group](#trilegroup) this art object belongs to. Can be null.|
|RotationCenter|Vector3|Rotation center of this art object.|
|SpinView|[Viewport](#viewpoint)|Behaviour currently unknown.|
|SpinEvery|Float|Behaviour currently unknown.|
|SpinOffset|Float|Behaviour currently unknown.|
|OffCenter|Boolean|Behaviour currently unknown.|
|VibrationPattern|[VibrationMotor](#vibrationmotor)[]|The vibration sequence to use for the tuning forks.|
|CodePattern|[CodeInput](#codeinput)[]|Unused?|
|Segment|[PathSegment](#pathsegment)|Behaviour currently unknown.|
|NextNode|Integer|Behaviour currently unknown. Can be null.|
|DestinationLevel|String|The name of the hub level this small warp panel will take the player. Note the target level must have a big warp gate.|
|TreasureMapName|String|The name of the treasure map this treasure contains.|
|InvisibleSides|[FaceOrientation](#faceorientation)[]|Behaviour currently unknown.|
|TimeswitchWindBackSpeed|Float|Behaviour currently unknown.|
|ContainedTrile|[ActorType](#actortype)|The ActorType to spawn when opening this treasure. Can be null.|

### VibrationMotor

[Enum](#enum) specifying controller vibration - **None**, **LeftLow** or **RightHigh**.

### Viewpoint

[Enum](#enum) specifying viewport - **None**, **Front**, **Right**, **Back**, **Left**, **Up**, **Down** or **Perspective**.

### BackgroundPlane

Structure defining background plane, its location and properties.

|Property name|Type|Description|
|-|-|-|
|Position|[Vector3](#vector3)|Position of a background plane.|
|Rotation|[Quaternion](#quaternion)|Rotation of a background plane.|
|Scale|[Vector3](#vector3)|Scale of a background plane.|
|Size|[Vector3](#vector3)|Width, height, and depth of plane.|
|TextureName|String|Name of a texture used by this background plane.|
|LightMap|Boolean|Behaviour currently unknown.|
|AllowOverbrightness|Boolean|Behaviour currently unknown.|
|Filter|[Color](#color)|Behaviour currently unknown.|
|Animated|Boolean|Behaviour currently unknown.|
|Doublesided|Boolean|If true, the texture is also rendered on the back of the mesh.|
|Opacity|Float|Behaviour currently unknown.|
|AttachedGroup|Integer|A [Trile Group](#trilegroup) this background plane belongs to. Can be null.|
|Billboard|Boolean|If true, this BackgroundPlane will always face the camera.|
|SyncWithSamples|Boolean|Behaviour currently unknown.|
|Crosshatch|Boolean|Behaviour currently unknown.|
|UnusedFlag|Boolean|Unused.|
|AlwaysOnTop|Boolean|Behaviour currently unknown.|
|Fullbright|Boolean|Behaviour currently unknown.|
|PixelatedLightmap|Boolean|Behaviour currently unknown.|
|XTextureRepeat|Boolean|Behaviour currently unknown.|
|YTextureRepeat|Boolean|Behaviour currently unknown.|
|ClampTexture|Boolean|Behaviour currently unknown.|
|ActorType|[ActorType](#actortype)|Behaviour currently unknown.|
|AttachedPlane|Integer|Behaviour currently unknown. Can be null.|
|ParallaxFactor|Float|Behaviour currently unknown.|

### Color

Structure containing information about R, G, B and A components of the color. It's stored in CSS/HTML-style eight-digit hexadecimal color syntax (`#rrggbbaa`) in a string.

### NpcInstance

Structure defining an instance of a non-playable character in the level.

|Property name|Type|Description|
|-|-|-|
|Name|String|Name of an NPC to use for this instance.|
|Position|[Vector3](#vector3)|Initial position of this NPC instance.|
|DestinationOffset|[Vector3](#vector3)|The position this NPC will move to say when talked to.|
|WalkSpeed|Float|How fast this NPC will move.|
|RandomizeSpeech|Boolean|If true, will pick a random line from this NpcInstance's `Speech` array when talked to, otherwise they will be sequential.|
|SayFirstSpeechLineOnce|Boolean|If true, this NpcInstance will only say the first entry in their `Speech` array a single time.|
|AvoidsGomez|Boolean|If true, this NPC will attempt to flee from Gomez.|
|ActorType|[ActorType](#actortype)|The ActorType of this NPC. Mainly used for owls, but also for rendering LightningGhosts.|
|Speech|[SpeechLine](#speechline)[]|The collection of SpeechLines this NpcInstance can say. Note this can be overrided by a Script with the action `NonPlayerCharacters[id].Say`|
|Actions|[NpcAction Dictionary](#npcaction-dictionary)|The NpcActions this NPC can take.|

### SpeechLine

Structure defining a speech line and its additional attributes.

|Property name|Type|Description|
|-|-|-|
|Text|String|Language identifier of a text which is used. See also: [fezdata's LanguageResource](./fezdata#languageresource).|
|OverrideContent|[NpcActionContent](#npcactioncontent)|Behaviour currently unknown.|

### NpcActionContent

|Property name|Type|Description|
|-|-|-|
|AnimationName|String|The name of the AnimatedTexture file in the `"Character Animations/" + Npc.Name + "/"` directory to use for this action.|
|SoundName|String|The name of the SoundEffect file in the `"Sounds/Npc/"` directory to use for this action.|

### NpcAction Dictionary

A dictionary of [NpcActionContents](#npcactioncontent) assigned to specific [NpcAction](#npcaction) as a key.

### NpcAction

[Enum](#enum) specifying NPC's action - **None**, **Idle**, **Idle2**, **Idle3**, **Walk**, **Turn**, **Talk**, **Burrow**, **Hide**, **ComeOut**, **TakeOff**, **Fly** or **Land**.
