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
|4|GoldenCube|Trile|When used, trile becomes a Golden Cube.|
|5|PickUp|Trile|Can be picked up by Gomez.|
|6|Bomb|Trile, BackgroundPlane|If trile, can be picked up by Gomez, after which it will explode after certain amount of time and respawn. If background plane and animated, it'll destroy itself once the animation is done (used to procedurally create explosion overlay).|
|7|Destructible|||
|8|DestructiblePermanent|||
|9|Vase|Trile|Can be picked up by Gomez. When thrown, it breaks on collision with ground.|
|10|Door|||
|11|Heart|||
|12|Watcher|||
|13|Crystal|||
|14|BlackHole|||
|15|Vine|||
|16|BigBomb|||
|17|TntBlock|||
|18|TntPickup|||
|19|MotorBlock|||
|20|Hurt|||
|21|Checkpoint|||
|22|TreasureChest|||
|23|CubeShard|||
|24|BigHeart|||
|25|SkeletonKey|||
|26|ExploSwitch|||
|27|PushSwitch|||
|28|EightBitDoor|ArtObject|Proximity door that opens when player has at least eight cubes collected.|
|29|PushSwitchSticky|||
|30|PushSwitchPermanent|||
|31|SuckBlock|||
|32|WarpGate|||
|33|OneBitDoor|ArtObject|Proximity door that opens when player has at least one cube collected.|
|34|SpinBlock|||
|35|PivotHandle|||
|36|FourBitDoor|ArtObject|Proximity door that opens when player has at least 4 cubes collected.|
|37|LightningPlatform|||
|38|LightningGhost|||
|39|Tombstone|||
|40|SplitUpCube|||
|41|UnlockedDoor|||
|42|Hole|||
|43|Couch|||
|44|Valve|||
|45|Rumbler|||
|46|Waterfall|||
|47|Trickle|||
|48|Drips|||
|49|Geyser|||
|50|ConnectiveRail|||
|51|BoltHandle|||
|52|BoltNutBottom|||
|53|BoltNutTop|||
|54|CodeMachine|ArtObject|Used for Code Machine puzzle. There can be only one in a level.|
|55|NumberCube|ArtObject, Trile|Used as an artifact. Once collected, appears in the inventory.|
|56|LetterCube|ArtObject, Trile|Used as an artifact. Once collected, appears in the inventory.|
|57|TriSkull|ArtObject, Trile|Used as an artifact. Once collected, appears in the inventory.|
|58|Tome|ArtObject, Trile|Used as an artifact. Once collected, appears in the inventory.|
|59|SecretCube|||
|60|LesserGate|||
|61|Crumbler|||
|62|LaserEmitter|||
|63|LaserBender|||
|64|LaserReceiver|||
|65|RebuildingHexahedron|||
|66|TreasureMap|||
|67|Timeswitch|||
|68|TimeswitchMovingPart|||
|69|Mail|||
|70|Mailbox|||
|71|Bookcase|||
|72|TwoBitDoor|ArtObject|Proximity door that opens when player has at least 2 cubes collected.|
|73|SixteenBitDoor|ArtObject|Proximity door that opens when player has at least 16 cubes collected.|
|74|ThirtyTwoBitDoor|ArtObject|Proximity door that opens when player has at least 32 cubes collected.|
|75|SixtyFourBitDoor|ArtObject|Proximity door that opens when player has at least 64 cubes collected.|
|76|Owl|||
|77|Bell|ArtObject|Uses bell puzzle logic on that art object. There can be only one in a level.|
|78|RotatingGroup|||
|79|BigWaterfall|||
|80|Telescope|||
|81|SinkPickup|||
|82|QrCode|||
|83|FpsPost|||
|84|PieceOfHeart|||
|85|SecretPassage|||
|86|Piston|||
