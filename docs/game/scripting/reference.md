# Scripting Reference

## Type Descriptors

[Events](#Events) are ScriptTriggers
[Properties](#Properties) are for ScriptConditions (operators not included)
[Operations](#Operations) are ScriptActions

### Events

| EntityIdentifier | TriggerName | RestrictedToActorTypes | Description |
|---|
| ArtObjects\[id\] | TreasureOpened |   |  |
| ArtObjects\[id\] | Open | EightBitDoor | When it's opened |
| Camera | Rotated |   | When the viewpoint changed |
| ArtObjects\[id\] | Activated | Rumbler, CodeMachine, QrCode | When the right pattern is input |
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
| ArtObjects\[id\] | Activate | LaserReceiver | When a receiver receives a laser |
| Level | Start |   | When the level starts |
| Owl | OwlCollected |   |  |
| Owl | OwlLanded |   |  |
| ArtObjects\[id\] | RotatedRight | PivotHandle | When it's been rotated right |
| ArtObjects\[id\] | RotatedLeft | PivotHandle | When it's been rotated left |
| Scripts\[id\] | Complete |   | When the script timeouts or terminates |
| Groups\[id\] | Sucked | SuckBlock | When it's completely inside its host volume |
| Groups\[id\] | Explode | PushSwitch, ExploSwitch, PushSwitchPermanent | When a bomb explodes near this switch |
| Groups\[id\] | Push | PushSwitch, ExploSwitch, PushSwitchPermanent | When this switch is pushed completely |
| Groups\[id\] | Lift | PushSwitch, ExploSwitch, PushSwitchPermanent | When this switch is lifted back up |
| ArtObjects\[id\] | ScrewedOut | Timeswitch | When the screw minimally sticks out from the base (it's been screwed out) |
| ArtObjects\[id\] | HitBase | Timeswitch | When it stop winding back in (hits the base) |
| Tombstone | MoreThanOneAligned |   | When more than one tombstones are aligned |
| ArtObjects\[id\] | Screwed | Valve, BoltHandle | When it's unscrewed |
| ArtObjects\[id\] | Unscrewed | Valve, BoltHandle | When it's screwed in |
| Volumes\[id\] | Enter |   | When the player enters this volume |
| Volumes\[id\] | Exit |   | When the player exits this volume |
| Volumes\[id\] | GoHigher |   | When the player goes higher than the volume/height-marker |
| Volumes\[id\] | GoLower |   | When the player goes lower than the volume/height-marker |
| Volumes\[id\] | CodeAccepted |   | If the input code was accepted |

### Properties

| EntityIdentifier | Type | PropertyName | RestrictedToActorTypes | Description |
|---|
| Game | bool | IsScrollOpen |   | Is there an open scroll? |
| Game | String | GetGlobalState |   |  |
| Game | String | GetLevelState |   |  |
| Game | bool | IsMapQrResolved |   |  |
| Game | bool | IsSewerQrResolved |   |  |
| Game | bool | IsZuQrResolved |   |  |
| Gomez | int | CollectedCubes |   | The number of small golden cubes the player's collected |
| Gomez | bool | Grounded |   | Is he standing on solid ground? |
| Gomez | bool | CanControl |   | Is Gomez controllable by the player? |
| Gomez | bool | Visible |   | Is Gomez visible? |
| Gomez | bool | IsOnLadder |   |  |
| Gomez | bool | Alive |   |  |
| Gomez | int | CollectedSplits |   |  |
| Level | bool | FirstVisit |   |  |
| Owl | int | OwlsCollected |   | Number of owls collected up to now |
| ArtObjects | int | Turns | PivotHandle | Gets the number of turns it's relative to the original state |
| Groups | bool | IsSucked | SuckBlock |  |
| Time | int | Hour |   | The hour of day (0-23) |
| Tombstone | int | AlignedCount |   |  |
| Volumes | bool | RegisterNeeded |   |  |
| Volumes | bool | GomezInside |   | Tests if Gomez is inside a certain volume |
| Volumes | bool | IsEnabled |   | Tests if volume is enabled |

### Operations

| EntityIdentifier | Parameters | ActionName | RestrictedToActorTypes | Description |
|---|
| ArtObjects | float x, float y, float z | SetRotation |   | Replaces the rotation angles (in degrees) |
| ArtObjects | float dX, float dY, float dZ | Rotate |   | Rotates over time (in rotations per second) |
| ArtObjects | float initPitch, float initYaw, float initRoll, float secondsUntilDouble | RotateIncrementally |   | Rotates incrementally over time (in time before doubling) |
| ArtObjects | float durationSeconds | TiltOnVertex |   | Tilts the art object on its bottom vertex |
| ArtObjects | float dX, float dY, float dZ, float easeInFor, float easeOutAfter, float easeOutFor | Move |   | Moves incrementally over time (in units per second) |
| ArtObjects | float height, float cyclesPerSecond | HoverFloat |   | Makes the object hover vertically |
| ArtObjects |  | StartEldersSequence |   | Does the whole hex-room sequence |
| ArtObjects |  | MoveNutToEnd |   | Moves a nut&bolt to its end |
| ArtObjects | float height | MoveNutToHeight |   | Moves a nut&bolt to a certain height, and gradually |
| ArtObjects | bool permanent, String spawnedActor | GlitchOut |   | Glitches and removes art object (and associated group if any) |
| ArtObjects |  | BeamGomez |   | For the hexahedron |
| ArtObjects | String textureName | Pulse |   | For the glow blocks |
| ArtObjects | String text, bool zuish | Say |   | For the zuish speech |
| BackgroundPlanes |  | Open | BigWaterfall |  |
| Camera | int triles | SetPixelsPerTrixel |   | Set the number of pixels per trixel (default is 4) |
| Camera | bool canRotate | SetCanRotate |   | Changes whether Gomez can rotate the camera |
| Camera | int distance | Rotate |   | Forces camera rotation, left (-1 to -3) or right (1 to 3) |
| Camera | String viewName | RotateTo |   | Rotates to any view orientation (Left, Right, Front, Back) |
| Camera | String colorName | FadeTo |   | Fades to the chosen color (Black, White, etc.) |
| Camera | String colorName | FadeFrom |   | Fades from the chosen color (Black, White, etc.) |
| Camera | String colorName | Flash |   | Flashes the chosen color once (Black, White, etc.) |
| Camera | float distance, float durationSeconds | Shake |   | Shakes the camera and vibrates controller |
| Camera | bool descending | SetDescending |   | Sets the camera offset as descending (true) or ascending (false) |
| Camera |  | Unconstrain |   | Remove the constraints (volume focus etc.) |
| Dot | String line, bool nearGomez, bool hideAfter | Say |   | Makes Dot say a custom text line |
| Dot | bool withCamera | ComeBackAndHide |   | Hides Dot in Gomez's hat |
| Dot | bool withCamera, bool hideDot | SpiralAround |   | Spiral around the level, yo |
| Game | bool forceRestart | EndTrial |   | Stops the trial EXPERIENCE and requires that the game is bought to continue |
| Game | float seconds | Wait |   | Pauses the script for some time |
| Game |  | GlitchUp |   | Glitch up |
| Game | String toLevel | Reboot |   | Reboots |
| Game | bool inverted, float factor | SetGravity |   | Changes gravity |
| Game | String localizedString, float forSeconds, bool onTop, bool onVolume | ShowScroll |   | Show scroll with localized string, for some time or indefinitely (0 or less), at the top or the bottom of the screen |
| Game | String key | CloseScroll |   | Hides the current scroll immediately |
| Game | String state | SetGlobalState |   | Sets a state string that is kept between levels |
| Game | String state | SetLevelState |   | Sets a state string that is local to that level |
| Game |  | AllowMapUsage |   |  |
| Game |  | Start32BitCutscene |   |  |
| Game |  | Start64BitCutscene |   |  |
| Game |  | Checkpoint |   |  |
| Game |  | ResolveMapQR |   |  |
| Game |  | ResolveSewerQR |   |  |
| Game |  | ResolveZuQR |   |  |
| Game |  | ShowCapsuleLetter |   |  |
| Gomez | bool controllable | SetCanControl |   | Sets whether Gomez can be controlled by the player |
| Gomez | String actionName | SetAction |   | Sets the current action (animation) for Gomez |
| Gomez |  | AllowEnterTunnel |   | Allows Gomez to enter that tunnel/passageway by pressing up |
| Gomez | bool visible | SetFezVisible |   | Shows/Hides gomez's fez |
| Gomez | bool visible | SetGomezVisible |   | Shows/Hides gomez |
| Groups | bool backwards | StartPath |   | Starts the group's moving path (must be set 'Needs Trigger') |
| Groups | bool backwards | RunPathOnce |   | Runs the group's moving path, but only once (must be set 'Needs Trigger') |
| Groups | bool backwards | RunSingleSegment |   | Runs a single segment of the group's moving path (must be set 'Needs Trigger') |
| Groups |  | Stop |   | Stops or pauses a moving group |
| Groups | float dX, float dY, float dZ | Move |   | Moves a group incrementally over time (units per second) |
| Groups | bool enabled | SetEnabled |   | Enables or disables all of a group's triles |
| Groups |  | MovePathToEnd |   | Moves a moving group to the end of its path |
| Groups | bool permanent | GlitchyDespawn |   | Moves a moving group to the end of its path |
| ArtObjects | bool enabled | SetEnabled | LaserEmitter | Starts or stops an emitter |
| Level | String levelName | AllowPipeChangeLevel |   | Changes the level MARIO-STYLE |
| Level | String levelName, bool asDoor, bool spin, bool trialEnding | ChangeLevel |   | Changes the level; if 'asDoor' is true, the level change occurs if gomez enters the door, else it's done immediately |
| Level | bool asDoor, bool spin | ReturnToLastLevel |   | Returns to the last accessed level; if 'asDoor' is true, the level change occurs if gomez enters the door, else it's done immediately |
| Level | String levelName, int toVolume, bool trialEnding | ChangeToFarAwayLevel |   | Changes the faraway level to a specific volume in the destination level; if 'asDoor' is true, the level change occurs if gomez enters the door, else it's done immediately |
| Level | String levelName, int toVolume, bool asDoor, bool spin, bool trialEnding | ChangeLevelToVolume |   | Changes the level to a specific volume in the destination level; if 'asDoor' is true, the level change occurs if gomez enters the door, else it's done immediately |
| Level | String levelName | ExploChangeLevel |   | Produces an epic explosion and changes level when it's done. |
| Level | float height | SetWaterHeight |   | Smoothly changes to a new water height |
| Level | float unitsPerSecond, float stopAtHeight | RaiseWater |   | Makes water rise to a certain threshold |
| Level |  | StopWater |   | Makes water stop raising immediately |
| Level |  | ResolvePuzzle |   | Marks a puzzle as solved, and plays the chime |
| Level |  | ResolvePuzzleSilent |   | Silently resolves a puzzle |
| Level |  | ResolvePuzzleSoundOnly |   |  |
| NonPlayerCharacters | String line, String customSound, String customAnimation | Say |   | Makes the NPC say a custom text line |
| NonPlayerCharacters |  | CarryGeezerLetter |   | CarryGeezerLetter |
| Paths | bool inTransition, bool outTransition | Start |   | Applies the whole path to the camera |
| ArtObjects | bool enabled | SetEnabled | PivotHandle | Enables or disables a pivot handle's rotatability |
| ArtObjects | int turns | RotateTo | PivotHandle | Enables or disables a pivot handle's rotatability |
| BackgroundPlanes | float seconds | FadeIn |   |  |
| BackgroundPlanes | float seconds | FadeOut |   |  |
| BackgroundPlanes | float factor | Flicker |   |  |
| Groups | bool clockwise, int turns | Rotate | RotatingGroup |  |
| Groups | bool enabled | SetEnabled | RotatingGroup |  |
| Scripts | bool enabled | SetEnabled |   | Enables or disables a script |
| Scripts |  | Evaluate |   | Evaluates a script |
| Sound | String soundName | Play |   | Plays a sound by its filename |
| Sound | String soundPrefix | PlayNext |   | Plays a sound by its prefix and an auto-incremented index (starts at 1) |
| Sound | float volume | SetMusicVolume |   | Changes the volume of BGM |
| Sound | String soundPrefix | ResetIndices |   | Resets the indices for a sound |
| Sound | String newMusic | ChangeMusic |   | Changes the music track and plays it |
| Sound | String trackName, float fadeDuration | UnmuteTrack |   | Enables a track by its name |
| Sound | String trackName, float fadeDuration | MuteTrack |   | Disables a track by its name |
| Sound | String trackName, float fadeDuration | UnmuteAmbience |   |  |
| Sound | String trackName, float fadeDuration | MuteAmbience |   |  |
| Sound | float overSeconds | FadeMusicOut |   | Fades the music out |
| Sound | float to, float overSeconds | FadeMusicTo |   |  |
| Sound | String trackName, bool dawn, bool day, bool dusk, bool night | ChangePhases |   |  |
| ArtObjects | bool enabled | SetEnabled | SpinBlock | Enables or disables a spinblock (which ceases or resumes its spinning) |
| Groups |  | Activate | PushSwitch, ExploSwitch, PushSwitchPermanent | Activates this switch |
| Groups | int newTrileId | ChangeTrile | PushSwitch, ExploSwitch, PushSwitchPermanent | Changes the visual of this switch's triles |
| Time | int hour, bool immediate | SetHour |   | Changes the hour of day (0-23), gradually or immediately |
| Time | int factor | SetTimeFactor |   | Sets the speed of time passage (0 = paused) |
| Time | float secondsUntilDouble | IncrementTimeFactor |   | Increments the time factor (specifying how much time before it doubles up) |
| Tombstone | int count | UpdateAlignCount |   |  |
| ArtObjects | bool enabled | SetEnabled | Valve, BoltHandle | Enables or disables a valve's rotatability |
| Volumes | int pixelsPerTrixel, bool immediate | FocusCamera |   | Center the camera view on this volume; set a value <= 0 to pixelsPerTrixels if you don't want to alter it. Immediate doesn't wait for an end-trigger |
| Volumes | bool enabled, bool permanent | SetEnabled |   | Disables or enables this volume |
| Volumes | float duration, float trixPerPix | SlowFocusOn |   | Slowly focuses camera on a volume |
| Volumes | String toLevel | LoadHexahedronAt |   | Loads the hex in the middle of a specified volume, and warp to the specified level afterwards |
| Volumes | String soundName, bool loop, float initialDelay, float perLoopDelay, bool directional, float pitchVariation | PlaySoundAt |   | Plays a sound on the specified volume, looped or not, directional or not (follows volume's enabled directions) |
| Volumes |  | MoveDotWithCamera |   | Moves Dot and the camera to the specified volume's center |
| Volumes | int pixelsPerTrixel, float verticalPan, float horizontalPan | FocusWithPan |   | Focuses the camera with panning support |
| Volumes | String actorTypeName | SpawnTrileAt |   | Spawns a treasure trile at this volume's location |
| ArtObjects | bool enabled | SetEnabled | WarpGate |  |

