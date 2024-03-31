# ActorType Enum

For multiple object types in the game (trile groups, background planes, NPC instances, art objects and triles), you can assign one of the types defined in a shared enum named `ActorType`. This specification documents all of the types, their designated object type and their usage in the game.

```note
This page is still WIP!
```

|Index|Name|Used by|Description|
|-|-|-|-|
|0|None|All|This object has no special properties.|
|1|Ladder|Trile|Gomez can climb it.|
|2|Bouncer|Trile|Gomez can bounce on it.|
|3|Sign|Trile|Can be interacted with to display text stored in [TrileInstance](/wiki/content/formats/fezlvl#trileinstanceactorsettings)'s `SignText` property.|
|4|GoldenCube|Trile|When used, trile becomes a Golden Cube (commonly called cube bits).|
|5|PickUp|Trile|Can be picked up by Gomez.|
|6|Bomb|Trile, BackgroundPlane|If trile, can be picked up by Gomez, after which it will explode after certain amount of time and respawn. If background plane and animated, it'll destroy itself once the animation is done (used to procedurally create explosion overlay).|
|7|Destructible|Trile|Can be destroyed by bombs.|
|8|DestructiblePermanent|Trile|Can be permanently destroyed by bombs. (destruction state persists through saves)|
|9|Vase|Trile|Can be picked up by Gomez. When thrown, it breaks on collision with ground.|
|10|Door|Trile|It's a locked door. Can be opened with a key.|
|11|Heart||Unused|
|12|Watcher|Trile|Those block characters that try to squish Gomez.|
|13|Crystal|Trile|The blocks that blink to the beat.|
|14|BlackHole||Unused. See ActorType `Hole` instead.|
|15|Vine|Trile|Gomez can climb it.|
|16|BigBomb|||
|17|TntBlock|||
|18|TntPickup|||
|19|MotorBlock||Unused|
|20|Hurt|Trile|Gomez gets hurt when touching this trile.|
|21|Checkpoint|||
|22|TreasureChest|ArtObject|It's a treasure chest. What it contains is determined by ActorSettings.ContainedTrile and if it's a TreasureMap ActorSettings.TreasureMapName|
|23|CubeShard||The big golden cubes|
|24|BigHeart||Unused|
|25|SkeletonKey||Key used for unlocking locked doors.|
|26|ExploSwitch|||
|27|PushSwitch|Group|A switch that activates when a heavy enough item is places atop it, and can become unactivated if that item is removed.|
|28|EightBitDoor|ArtObject|Proximity door that opens when player has at least eight cubes collected.|
|29|PushSwitchSticky|Group|A switch that activates when a heavy enough item is places atop it, and stays active until the level is reloaded.|
|30|PushSwitchPermanent|Group|A switch that permanently activates when a heavy enough item is places atop it. (activation state persists through saves)|
|31|SuckBlock|Trile|Can be picked up by Gomez. Will get sucked into ActorSettings.HostVolume if it's close enough, and if it's this SuckBlock's HostVolume, an event is fired.|
|32|WarpGate|ArtObject|Those big warp gate things in some of the hub levels.|
|33|OneBitDoor|ArtObject|Proximity door that opens when player has at least one cube collected.|
|34|SpinBlock|ArtObject|These objects spin around a set point around a set axis every `ActorSettings.SpinEvery` seconds, and will throwing Gomez off if he is holding onto the side.|
|35|PivotHandle|ArtObject|Gomez can push this from the front to cause it to rotate, which triggers events.|
|36|FourBitDoor|ArtObject|Proximity door that opens when player has at least 4 cubes collected.|
|37|LightningPlatform|Trile|Invisible platforms that flash visible when lightning strikes|
|38|LightningGhost|Npc|The spooky ghosts you can talk to in the graveyard area.|
|39|Tombstone|ArtObject|Gomez can grab ahold of it and spin it around, causing events to be fired depending on how many are aligned.|
|40|SplitUpCube||Unused? Likely was for an old version of cube bits.|
|41|UnlockedDoor|Trile|It's a door that does not require any unlocking.|
|42|Hole|Trile|This trile is a blackhole. See also `VolumeActorSettings.IsBlackHole`|
|43|Couch|||
|44|Valve|ArtObject|Gomez can spin them around, which triggers events.|
|45|Rumbler|ArtObject|Used for tuning forks. See ActorSettings.VibrationPattern for the code pattern.|
|46|Waterfall|BackgroundPlane|Spawns water particle effects.|
|47|Trickle|BackgroundPlane|Spawns water particle effects.|
|48|Drips|BackgroundPlane|Spawns water particle effects.|
|49|Geyser|Group|Causes the group to move up and down at regular intervals and to set heights.|
|50|ConnectiveRail|ArtObject|Used for those tracks that certain moving platforms follow.|
|51|BoltHandle|ArtObject|Gomez can spin these aroung to move the platform up or down.|
|52|BoltNutBottom|ArtObject|Deternimes the lower limit of the colliding bolt platform.|
|53|BoltNutTop|ArtObject|Deternimes the upper limit of the colliding bolt platform.|
|54|CodeMachine|ArtObject|Used for Code Machine puzzle. There can be only one in a level.|
|55|NumberCube|ArtObject, Trile|Used as an artifact. Once collected, appears in the inventory.|
|56|LetterCube|ArtObject, Trile|Used as an artifact. Once collected, appears in the inventory.|
|57|TriSkull|ArtObject, Trile|Used as an artifact. Once collected, appears in the inventory.|
|58|Tome|ArtObject, Trile|Used as an artifact. Once collected, appears in the inventory.|
|59|SecretCube||Anti cubes|
|60|LesserGate|ArtObject|Those one-way warp panel things that take you back to the hub level's WarpGate|
|61|Crumbler|Trile|This trile crumbles when stepped on.|
|62|LaserEmitter|ArtObject|Has an unused `SetEnabled` ScriptAction|
|63|LaserBender|ArtObject|Unused|
|64|LaserReceiver|ArtObject|Has an unused `Activate` ScriptTrigger|
|65|RebuildingHexahedron|ArtObject|Unused|
|66|TreasureMap||It's a treasure map. See ActorSettings.TreasureMapName for the name of the map.|
|67|Timeswitch|ArtObject|Those things that you can screw out that move stuff and then move back when the time is up.|
|68|TimeswitchMovingPart|||
|69|Mail|||
|70|Mailbox|ArtObject||
|71|Bookcase|ArtObject|A bookcase secret door that Gomez can push from the front to open.|
|72|TwoBitDoor|ArtObject|Proximity door that opens when player has at least 2 cubes collected.|
|73|SixteenBitDoor|ArtObject|Proximity door that opens when player has at least 16 cubes collected.|
|74|ThirtyTwoBitDoor|ArtObject|Proximity door that opens when player has at least 32 cubes collected.|
|75|SixtyFourBitDoor|ArtObject|Proximity door that opens when player has at least 64 cubes collected.|
|76|Owl|Npc|Those owls that often spit out lore and the game keeps track of how many you've talked to.|
|77|Bell|ArtObject|Uses bell puzzle logic on that art object. There can be only one in a level.|
|78|RotatingGroup|Group|This group spins around a set point around a set axis every `Group.SpinFrequency` seconds, moving Gomez with the group.|
|79|BigWaterfall|BackgroundPlane||
|80|Telescope|ArtObject|When interacted with, will show stars depending on the camera's viewpoint.|
|81|SinkPickup||Used internally for SuckBlock.|
|82|QrCode|ArtObject|Almost functionally equivalent to the `Rumbler` ActorType, but there's no vibrations, and if one if this code is solved, the first ArtObject in `SEWER_QR` will be marked as inactivate, the second (Note: these are only set if the levels are visited)|
|83|FpsPost|ArtObject|Unused|
|84|PieceOfHeart||The red/heart cubes|
|85|SecretPassage|ArtObject|Secret shortcut door that require visiting both levels before they are enabled.|
|86|Piston|Group|Plays the piston sound effect when this group moves.|
