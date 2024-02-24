# FEZMAP format

## Overview

`.fezmap` file contain map tree structure stored in JSON format. It's mostly similar to in-game's `MapTree` structure; however, in order to improve data readability, it was slightly changed: instead of directly storing children nodes in node connections, they're stored in parallel as a directory, with unique integer as an identifier for each node.

## Property definitions

### Root object

The root object of `.fezmap` JSON file is a `Directory<int, MapNode>`. MapNode with index 0 is expected to be a root node in the map tree. Map tree cannot create a loop and some connection may be ignored if that happens.

### MapNode

|Property name|Type|Description|
|-|-|-|
|LevelName|String|Name of a level this node represents. Used to determine a thumbnail.|
|NodeType|[LevelNodeType](#levelnodetype)|Type of the node.|
|Conditions|[WinConditions](#winconditions)|List of values determining what is required to turn this node as completed.|
|HasLesserGate|Boolean|If true, displays lesser gate icon next to this node.|
|HasWarpGate|Boolean|If true, displays warp gate icon next to this node.|
|Connections|[MapNodeConnection](#mapnodeconnection)[]|List of connections this node branch to.|

### WinConditions

|Property name|Type|Description|
|-|-|-|
|ChestCount|Integer|Number of chests required to be opened in this level.|
|LockedDoorCount|Integer|Number of key doors required to be opened in this level.|
|UnlockedDoorCount|Integer|Number of normal doors required to be opened in this level.|
|ScriptIds|Integer[]|List of integers representing IDs of level's scripts required to be marked as completed.|
|CubeShardCount|Integer|Behaviour currently not known.|
|OtherCollectibleCount|Integer|Behaviour currently not known.|
|SplitUpCount|Integer|Behaviour currently not known.|
|SecretCount|Integer|Behaviour currently not known.|

### MapNodeConnection

|Property name|Type|Description|
|-|-|-|
|Face|[FaceOrientation](#faceorientation)|The direction which given connection is branching towards.|
|Node|Integer|ID of a node this connection links to.|
|BranchOversize|Float|Behaviour currently not known.|

### Enum

All enums are stored as PascalCamelCase string parameters.

### LevelNodeType

[Enum](#enum) specifying how level should appear in the map. It can take one of three values:

- **Node**
- **Hub**
- **Lesser**

### FaceOrientation

[Enum](#enum) specifying one of six possible trile face orientations - **Left**, **Down**, **Back**, **Right**, **Top** or **Front**.
