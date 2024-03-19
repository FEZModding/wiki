# FEZSONG format

## Overview

`.feznpc` file contains song metadata stored in JSON format. This documentation presents a structure and purpose to each property in this file format. Descriptions are incomplete in some cases, and they might be incorrect due to lack of proper testing in the game itself, but that'll improve over time.

## Property definitions

### TrackedSong

|Property name|Type|Description|
|-|-|-|
|Loops|[Loop](#loop)[]|Behaviour currently unknown.|
|Name|String|The unique name of the song. Usually this is related to the file name.|
|Tempo|Integer|Behaviour currently unknown.|
|TimeSignature|Integer|Behaviour currently unknown.|
|Notes|[ShardNotes](#shardnotes)[]|The pitch of the musical tones to play when collecting a cube bit.|
|AssembleChord|[AssembleChords](#assemblechords)|The pitch of the collect jingle to play when collecting a treasure that's not in a treasure chest.|
|RandomOrdering|Boolean|Behaviour currently unknown.|
|CustomOrdering|Integer[]|Behaviour currently unknown.|

### Loop

```note
The pairs of LoopTimesFrom to LoopTimesTo, and TriggerFrom to TriggerTo define bounds for random values 
```

|Property name|Type|Description|
|-|-|-|
|Duration|Integer|The number of musical bars in this loop.|
|LoopTimesFrom|Integer|The minimum number times to repeat the loop before playing again.|
|LoopTimesTo|Integer|The maximum number times to repeat the loop before playing again.|
|Name|String|The name of this loop. Should be distinct from other loop names in this song.|
|TriggerFrom|Integer|The minimum number of musical bars to wait before playing again.|
|TriggerTo|Integer|The maximum number of musical bars to wait before playing again.|
|Delay|Integer|The number of musical bars to wait before playing for the first time.|
|Night|Boolean|If this loop plays during night|
|Day|Boolean|If this loop plays during day|
|Dusk|Boolean|If this loop plays during dusk|
|Dawn|Boolean|If this loop plays during dawn|
|FractionalTime|Boolean|If false, the random value determined by the range TriggerFrom to TriggerTo will be an integer, otherwise it will be a floating point value.|
|OneAtATime|Boolean|Behaviour currently unknown.|
|CutOffTail|Boolean|Behaviour currently unknown.|

### Enum

All enums are stored as PascalCamelCase string parameters.

### ShardNotes

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

### AssembleChords

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

