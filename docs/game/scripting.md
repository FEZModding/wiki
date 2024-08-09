# Scripting Reference

## Type Descriptors

[Events](#events) are ScriptTriggers<br />
[Properties](#properties) are for ScriptConditions (operators not included)<br />
[Operations](#operations) are ScriptActions

### Events

| EntityIdentifier | TriggerName | RestrictedToActorTypes | Description |
|---|
| ArtObject\[id\] | TreasureOpened |   |  |
| ArtObject\[id\] | Open | EightBitDoor | When it's opened |
| Camera | Rotated |   | When the viewpoint changed |
| ArtObject\[id\] | Activated | Rumbler, CodeMachine, QrCode | When the right pattern is input |
| Gomez | EnteredDoor |   |  |
| Gomez | Jumped |   |  |
| Gomez | ClimbedLadder |   |  |
| Gomez | ClimbedVine |   |  |
| Gomez | LookedAround |   |  |
| Gomez | LiftedObject |   |  |
| Gomez | ThrewObject |   |  |
| Gomez | OpenedMenuCube |   |  |
| Gomez | ReadSign |   |  |
| Gomez | GrabbedLedge |   |  |
| Gomez | DropObject |   |  |
| Gomez | DroppedLedge |   |  |
| Gomez | Hoisted |   |  |
| Gomez | ClimbedOverLadder |   |  |
| Gomez | DroppedFromLadder |   |  |
| Gomez | ReadMail |   |  |
| Gomez | CollectedSplitUpCube |   |  |
| Gomez | CollectedShard |   |  |
| Gomez | CollectedAnti |   |  |
| Gomez | CollectedGlobalAnti |   |  |
| Gomez | CollectedPieceOfHeart |   |  |
| Gomez | OpenedTreasure |   |  |
| Gomez | Landed |   |  |
| ArtObject\[id\] | Activate | LaserReceiver | When a receiver receives a laser |
| Level | Start |   | When the level starts |
| Owl | OwlCollected |   |  |
| Owl | OwlLanded |   |  |
| ArtObject\[id\] | RotatedRight | PivotHandle | When it's been rotated right |
| ArtObject\[id\] | RotatedLeft | PivotHandle | When it's been rotated left |
| Script\[id\] | Complete |   | When the script timeouts or terminates |
| Group\[id\] | Sucked | SuckBlock | When it's completely inside its host volume |
| Group\[id\] | Explode | PushSwitch, ExploSwitch, PushSwitchPermanent | When a bomb explodes near this switch |
| Group\[id\] | Push | PushSwitch, ExploSwitch, PushSwitchPermanent | When this switch is pushed completely |
| Group\[id\] | Lift | PushSwitch, ExploSwitch, PushSwitchPermanent | When this switch is lifted back up |
| ArtObject\[id\] | ScrewedOut | Timeswitch | When the screw minimally sticks out from the base (it's been screwed out) |
| ArtObject\[id\] | HitBase | Timeswitch | When it stop winding back in (hits the base) |
| Tombstone | MoreThanOneAligned |   | When more than one tombstones are aligned |
| ArtObject\[id\] | Screwed | Valve, BoltHandle | When it's unscrewed |
| ArtObject\[id\] | Unscrewed | Valve, BoltHandle | When it's screwed in |
| Volume\[id\] | Enter |   | When the player enters this volume |
| Volume\[id\] | Exit |   | When the player exits this volume |
| Volume\[id\] | GoHigher |   | When the player goes higher than the volume/height-marker |
| Volume\[id\] | GoLower |   | When the player goes lower than the volume/height-marker |
| Volume\[id\] | CodeAccepted |   | If the input code was accepted |

### Properties

| EntityIdentifier | PropertyName | Type | RestrictedToActorTypes | Description |
|---|
| Game | IsScrollOpen | bool |   | Is there an open scroll? |
| Game | GetGlobalState | String |   |  |
| Game | GetLevelState | String |   |  |
| Game | IsMapQrResolved | bool |   |  |
| Game | IsSewerQrResolved | bool |   |  |
| Game | IsZuQrResolved | bool |   |  |
| Gomez | CollectedCubes | int |   | The number of small golden cubes the player's collected |
| Gomez | Grounded | bool |   | Is he standing on solid ground? |
| Gomez | CanControl | bool |   | Is Gomez controllable by the player? |
| Gomez | Visible | bool |   | Is Gomez visible? |
| Gomez | IsOnLadder | bool |   |  |
| Gomez | Alive | bool |   |  |
| Gomez | CollectedSplits | int |   |  |
| Level | FirstVisit | bool |   |  |
| Owl | OwlsCollected | int |   | Number of owls collected up to now |
| ArtObject\[id\] | Turns | int | PivotHandle | Gets the number of turns it's relative to the original state |
| Group\[id\] | IsSucked | bool | SuckBlock |  |
| Time | Hour | int |   | The hour of day (0-23) |
| Tombstone | AlignedCount | int |   |  |
| Volume\[id\] | RegisterNeeded | bool |   |  |
| Volume\[id\] | GomezInside | bool |   | Tests if Gomez is inside a certain volume |
| Volume\[id\] | IsEnabled | bool |   | Tests if volume is enabled |

### Operations

| EntityIdentifier | ActionName | Parameters | RestrictedToActorTypes | Description |
|---|
| ArtObject\[id\] | SetRotation | float x, float y, float z |   | Replaces the rotation angles (in degrees) |
| ArtObject\[id\] | Rotate | float dX, float dY, float dZ |   | Rotates over time (in rotations per second) |
| ArtObject\[id\] | RotateIncrementally | float initPitch, float initYaw, float initRoll, float secondsUntilDouble |   | Rotates incrementally over time (in time before doubling) |
| ArtObject\[id\] | TiltOnVertex | float durationSeconds |   | Tilts the art object on its bottom vertex |
| ArtObject\[id\] | Move | float dX, float dY, float dZ, float easeInFor, float easeOutAfter, float easeOutFor |   | Moves incrementally over time (in units per second) |
| ArtObject\[id\] | HoverFloat | float height, float cyclesPerSecond |   | Makes the object hover vertically |
| ArtObject\[id\] | StartEldersSequence |  |   | Does the whole hex-room sequence |
| ArtObject\[id\] | MoveNutToEnd |  |   | Moves a nut&bolt to its end |
| ArtObject\[id\] | MoveNutToHeight | float height |   | Moves a nut&bolt to a certain height, and gradually |
| ArtObject\[id\] | GlitchOut | bool permanent, String spawnedActor |   | Glitches and removes art object (and associated group if any) |
| ArtObject\[id\] | BeamGomez |  |   | For the hexahedron |
| ArtObject\[id\] | Pulse | String textureName |   | For the glow blocks |
| ArtObject\[id\] | Say | String text, bool zuish |   | For the zuish speech |
| Plane\[id\] | Open |  | BigWaterfall |  |
| Camera | SetPixelsPerTrixel | int triles |   | Set the number of pixels per trixel (default is 4) |
| Camera | SetCanRotate | bool canRotate |   | Changes whether Gomez can rotate the camera |
| Camera | Rotate | int distance |   | Forces camera rotation, left (-1 to -3) or right (1 to 3) |
| Camera | RotateTo | String viewName |   | Rotates to any view orientation (Left, Right, Front, Back) |
| Camera | FadeTo | String colorName |   | Fades to the chosen color (Black, White, etc.) |
| Camera | FadeFrom | String colorName |   | Fades from the chosen color (Black, White, etc.) |
| Camera | Flash | String colorName |   | Flashes the chosen color once (Black, White, etc.) |
| Camera | Shake | float distance, float durationSeconds |   | Shakes the camera and vibrates controller |
| Camera | SetDescending | bool descending |   | Sets the camera offset as descending (true) or ascending (false) |
| Camera | Unconstrain |  |   | Remove the constraints (volume focus etc.) |
| Dot | Say | String line, bool nearGomez, bool hideAfter |   | Makes Dot say a custom text line |
| Dot | ComeBackAndHide | bool withCamera |   | Hides Dot in Gomez's hat |
| Dot | SpiralAround | bool withCamera, bool hideDot |   | Spiral around the level, yo |
| Game | EndTrial | bool forceRestart |   | Stops the trial EXPERIENCE and requires that the game is bought to continue |
| Game | Wait | float seconds |   | Pauses the script for some time |
| Game | GlitchUp |  |   | Glitch up |
| Game | Reboot | String toLevel |   | Reboots |
| Game | SetGravity | bool inverted, float factor |   | Changes gravity |
| Game | ShowScroll | String localizedString, float forSeconds, bool onTop, bool onVolume |   | Show scroll with localized string, for some time or indefinitely (0 or less), at the top or the bottom of the screen |
| Game | CloseScroll | String key |   | Hides the current scroll immediately |
| Game | SetGlobalState | String state |   | Sets a state string that is kept between levels |
| Game | SetLevelState | String state |   | Sets a state string that is local to that level |
| Game | AllowMapUsage |  |   |  |
| Game | Start32BitCutscene |  |   |  |
| Game | Start64BitCutscene |  |   |  |
| Game | Checkpoint |  |   |  |
| Game | ResolveMapQR |  |   |  |
| Game | ResolveSewerQR |  |   |  |
| Game | ResolveZuQR |  |   |  |
| Game | ShowCapsuleLetter |  |   |  |
| Gomez | SetCanControl | bool controllable |   | Sets whether Gomez can be controlled by the player |
| Gomez | SetAction | String actionName |   | Sets the current action (animation) for Gomez |
| Gomez | AllowEnterTunnel |  |   | Allows Gomez to enter that tunnel/passageway by pressing up |
| Gomez | SetFezVisible | bool visible |   | Shows/Hides gomez's fez |
| Gomez | SetGomezVisible | bool visible |   | Shows/Hides gomez |
| Group\[id\] | StartPath | bool backwards |   | Starts the group's moving path (must be set 'Needs Trigger') |
| Group\[id\] | RunPathOnce | bool backwards |   | Runs the group's moving path, but only once (must be set 'Needs Trigger') |
| Group\[id\] | RunSingleSegment | bool backwards |   | Runs a single segment of the group's moving path (must be set 'Needs Trigger') |
| Group\[id\] | Stop |  |   | Stops or pauses a moving group |
| Group\[id\] | Move | float dX, float dY, float dZ |   | Moves a group incrementally over time (units per second) |
| Group\[id\] | SetEnabled | bool enabled |   | Enables or disables all of a group's triles |
| Group\[id\] | MovePathToEnd |  |   | Moves a moving group to the end of its path |
| Group\[id\] | GlitchyDespawn | bool permanent |   | Moves a moving group to the end of its path |
| ArtObject\[id\] | SetEnabled | bool enabled | LaserEmitter | Starts or stops an emitter |
| Level | AllowPipeChangeLevel | String levelName |   | Changes the level MARIO-STYLE |
| Level | ChangeLevel | String levelName, bool asDoor, bool spin, bool trialEnding |   | Changes the level; if 'asDoor' is true, the level change occurs if gomez enters the door, else it's done immediately |
| Level | ReturnToLastLevel | bool asDoor, bool spin |   | Returns to the last accessed level; if 'asDoor' is true, the level change occurs if gomez enters the door, else it's done immediately |
| Level | ChangeToFarAwayLevel | String levelName, int toVolume, bool trialEnding |   | Changes the faraway level to a specific volume in the destination level; if 'asDoor' is true, the level change occurs if gomez enters the door, else it's done immediately |
| Level | ChangeLevelToVolume | String levelName, int toVolume, bool asDoor, bool spin, bool trialEnding |   | Changes the level to a specific volume in the destination level; if 'asDoor' is true, the level change occurs if gomez enters the door, else it's done immediately |
| Level | ExploChangeLevel | String levelName |   | Produces an epic explosion and changes level when it's done. |
| Level | SetWaterHeight | float height |   | Smoothly changes to a new water height |
| Level | RaiseWater | float unitsPerSecond, float stopAtHeight |   | Makes water rise to a certain threshold |
| Level | StopWater |  |   | Makes water stop raising immediately |
| Level | ResolvePuzzle |  |   | Marks a puzzle as solved, and plays the chime |
| Level | ResolvePuzzleSilent |  |   | Silently resolves a puzzle |
| Level | ResolvePuzzleSoundOnly |  |   |  |
| Npc\[id\] | Say | String line, String customSound, String customAnimation |   | Makes the NPC say a custom text line |
| Npc\[id\] | CarryGeezerLetter |  |   | CarryGeezerLetter |
| Path\[id\] | Start | bool inTransition, bool outTransition |   | Applies the whole path to the camera |
| ArtObject\[id\] | SetEnabled | bool enabled | PivotHandle | Enables or disables a pivot handle's rotatability |
| ArtObject\[id\] | RotateTo | int turns | PivotHandle | Enables or disables a pivot handle's rotatability |
| Plane\[id\] | FadeIn | float seconds |   |  |
| Plane\[id\] | FadeOut | float seconds |   |  |
| Plane\[id\] | Flicker | float factor |   |  |
| Group\[id\] | Rotate | bool clockwise, int turns | RotatingGroup |  |
| Group\[id\] | SetEnabled | bool enabled | RotatingGroup |  |
| Script\[id\] | SetEnabled | bool enabled |   | Enables or disables a script |
| Script\[id\] | Evaluate |  |   | Evaluates a script |
| Sound | Play | String soundName |   | Plays a sound by its filename |
| Sound | PlayNext | String soundPrefix |   | Plays a sound by its prefix and an auto-incremented index (starts at 1) |
| Sound | SetMusicVolume | float volume |   | Changes the volume of BGM |
| Sound | ResetIndices | String soundPrefix |   | Resets the indices for a sound |
| Sound | ChangeMusic | String newMusic |   | Changes the music track and plays it |
| Sound | UnmuteTrack | String trackName, float fadeDuration |   | Enables a track by its name |
| Sound | MuteTrack | String trackName, float fadeDuration |   | Disables a track by its name |
| Sound | UnmuteAmbience | String trackName, float fadeDuration |   |  |
| Sound | MuteAmbience | String trackName, float fadeDuration |   |  |
| Sound | FadeMusicOut | float overSeconds |   | Fades the music out |
| Sound | FadeMusicTo | float to, float overSeconds |   |  |
| Sound | ChangePhases | String trackName, bool dawn, bool day, bool dusk, bool night |   |  |
| ArtObject\[id\] | SetEnabled | bool enabled | SpinBlock | Enables or disables a spinblock (which ceases or resumes its spinning) |
| Group\[id\] | Activate |  | PushSwitch, ExploSwitch, PushSwitchPermanent | Activates this switch |
| Group\[id\] | ChangeTrile | int newTrileId | PushSwitch, ExploSwitch, PushSwitchPermanent | Changes the visual of this switch's triles |
| Time | SetHour | int hour, bool immediate |   | Changes the hour of day (0-23), gradually or immediately |
| Time | SetTimeFactor | int factor |   | Sets the speed of time passage (0 = paused) |
| Time | IncrementTimeFactor | float secondsUntilDouble |   | Increments the time factor (specifying how much time before it doubles up) |
| Tombstone | UpdateAlignCount | int count |   |  |
| ArtObject\[id\] | SetEnabled | bool enabled | Valve, BoltHandle | Enables or disables a valve's rotatability |
| Volume\[id\] | FocusCamera | int pixelsPerTrixel, bool immediate |   | Center the camera view on this volume; set a value <= 0 to pixelsPerTrixels if you don't want to alter it. Immediate doesn't wait for an end-trigger |
| Volume\[id\] | SetEnabled | bool enabled, bool permanent |   | Disables or enables this volume |
| Volume\[id\] | SlowFocusOn | float duration, float trixPerPix |   | Slowly focuses camera on a volume |
| Volume\[id\] | LoadHexahedronAt | String toLevel |   | Loads the hex in the middle of a specified volume, and warp to the specified level afterwards |
| Volume\[id\] | PlaySoundAt | String soundName, bool loop, float initialDelay, float perLoopDelay, bool directional, float pitchVariation |   | Plays a sound on the specified volume, looped or not, directional or not (follows volume's enabled directions) |
| Volume\[id\] | MoveDotWithCamera |  |   | Moves Dot and the camera to the specified volume's center |
| Volume\[id\] | FocusWithPan | int pixelsPerTrixel, float verticalPan, float horizontalPan |   | Focuses the camera with panning support |
| Volume\[id\] | SpawnTrileAt | String actorTypeName |   | Spawns a treasure trile at this volume's location |
| ArtObject\[id\] | SetEnabled | bool enabled | WarpGate |  |
