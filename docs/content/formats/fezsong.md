# FEZSONG format

## TODO

## Overview

`.feznpc` file contains song metadata stored in JSON format.

## Property definitions

### TrackedSong

|Property name|Type|Description|
|-|-|-|
|Loops|[Loop](#loop)[]|TODO|
|Name|String|The unique name of the song. Usually this is related to the file name.|
|Tempo|Integer|TODO|
|TimeSignature|Integer|TODO|
|Notes|[ShardNotes](#shardnotes)[]|The pitch of the musical tones to play when collecting a cube bit.|
|AssembleChord|[AssembleChords](#assemblechords)|The pitch of the collect jingle to play when collecting a treasure that's not in a treasure chest.|
|RandomOrdering|Boolean|TODO|
|CustomOrdering|Integer[]|TODO|

### Loop

|Property name|Type|Description|
|-|-|-|
|Duration|Integer|TODO|
|LoopTimesFrom|Integer|TODO|
|LoopTimesTo|Integer|TODO|
|Name|String|The name of this loop. Should be distinct from other loop names in this song.|
|TriggerFrom|Integer|TODO|
|TriggerTo|Integer|TODO|
|Delay|Integer|TODO|
|Night|Boolean|If this loop plays during night|
|Day|Boolean|If this loop plays during day|
|Dusk|Boolean|If this loop plays during dusk|
|Dawn|Boolean|If this loop plays during dawn|
|FractionalTime|Boolean|TODO|
|OneAtATime|Boolean|TODO|
|CutOffTail|Boolean|TODO|

### Enum

All enums are stored as PascalCamelCase string parameters.

### shardnotes

[Enum](#enum) specifying cube bit pickup sounds. It can take one of these values:

C2,
Csharp2,
D2,
Dsharp2,
E2,
F2,
Fsharp2,
G2,
Gsharp2,
A2,
Asharp2,
B2,
C3,
Csharp3,
D3,
Dsharp3,
E3,
F3,
Fsharp3,
G3,
Gsharp3,
A3,
Asharp3,
B3,
C4

### assemblechords

[Enum](#enum) specifying treasure get sound (not treasure chests). It can take one of these values:

C_maj,
Csharp_maj,
D_maj,
Dsharp_maj,
E_maj,
F_maj,
Fsharp_maj,
G_maj,
Gsharp_maj,
A_maj,
Asharp_maj,
B_maj

