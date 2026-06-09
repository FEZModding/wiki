---
sort: 11
---

# Tracked Songs

Instead of prerecorded, offline-sequenced music files, the game uses a tracked music system that:

- Uses smaller `.ogg` loop files.
- Allows dynamic, indefinitely playing, track-based songs.
- Allows scripts to mute or unmute tracks in response to level or player events.
- Works with the time-of-day cycle.

**Diez** edits these song metadata files:

![](/wiki/assets/images/editor/diez.png)

Tracked songs are stored in the `Music/` folder. Each song has a `.fezsong.json` file and a same-named folder alongside it containing the song's `.ogg` loop files:

```text
├── Zuins
│   ├── Zuins_01.ogg
│   ├── Zuins_02.ogg
│   ├── Zuins_03.ogg
│   └── Zuins_04.ogg
└── Zuins.fezsong.json
```

## Layout

The editor is split into three sections:

- **Tracked Song Properties**: Global song settings, shard notes, assemble chord, and ordering.
- **Overlay Loops**: The list of loops used by the song.
- **Selected Loop Properties**: Timing and playback settings for the selected loop.

## Song Properties

The left section edits global song data.

- **Song Name**: Unique song name.
- **Tempo**: Tempo used for bar-based loop timing.
- **Time Signature /4**: Number of beats per bar.
- **Assemble Chord**: Golden or Anti cube collect chord used by this song.
- **Note #1-#8**: Cube shards pickup notes.
- **Preview the Assemble Chord**: Plays the selected assemble chord.
- **Random One-At-a-Time Ordering**: Enables random ordering for one-at-a-time loops.
- **Custom Ordering**: Custom loop ordering data.

You can preview an assemble chord by clicking the `Play` button. Diez loads the corresponding sound from the `Sounds/Collects/SplitUpCube/` folder.

## Overlay Loops

The middle section lists the song's overlay loops.

The toolbar has the following buttons, from left to right:

- **Down** / **Up**: Reorders the selected loop.
- **Add**: Chooses a loop file from the current song folder.
- **Remove**: Deletes the selected loop from the metadata.

To edit a loop's properties, double-click it in the list.

Loop names use the tracked song naming convention:

```text
SongName ^ LoopName
```

For example:

```text
CMYKave ^ rhythm
```

## Loop Properties

The right section edits the selected loop properties.

- **Filename**: Referenced loop name.
- **Trigger From / Trigger To**: Range of bars to wait before triggering the loop again.
- **Fractional Time**: Allows non-integer trigger timing within the trigger range.
- **Loop Times From / Loop Times To**: Range for how many times the loop repeats.
- **Duration**: Loop length in bars.
- **Delay**: Bars to wait before the first trigger.
- **One-at-a-time**: Marks the loop for one-at-a-time playback behavior.
- **Cut off tail**: Cuts the loop tail when stopping.
- **Day / Night / Dawn / Dusk**: Time-of-day filters for when the loop can play.

Most loop timing is bar-based, so changes depend on the song tempo and time signature.

## Example Song

The following example shows the metadata for Disasterpeace's **Puzzle**, also known as the puzzle-solving music. Its tracked song is named `Cycle` and uses the following global settings:

| Property                      | Value                                          |
| ----------------------------- | ---------------------------------------------- |
| Tempo                         | 140 BPM                                        |
| Time Signature                | 4/4                                            |
| Assemble Chord                | E major                                        |
| Shard Notes                   | `D2`, `E2`, `A2`, `B2`, `D3`, `E3`, `A3`, `B3` |
| Random One-At-a-Time Ordering | Disabled                                       |
| Custom Ordering               | None                                           |

The following table summarizes the timing pattern used by the recurring parts. Individual loops may use different values:

| Track       | Initial Delay | Duration | Interplay Delay |
| ----------- | ------------- | -------- | --------------- |
| Main Arp    | None          | 8 bars   | [0, 16] bars    |
| Counter Arp | 4 bars        | 8 bars   | [0, 16] bars    |
| Ostinato    | 8 bars        | 4 bars   | [0, 16] bars    |
| Bass        | 8 bars        | 4 bars   | [0, 24] bars    |
| Antecedent  | 16 bars       | 3 bars   | [0, 16] bars    |
| Triplets    | 16 bars       | 9 bars   | [0, 16] bars    |
| Consequent  | 20 bars       | 3 bars   | [0, 16] bars    |

The arrangement changes with the time of day:

| Time of Day | Loop Family | Active Loops |
| ----------- | ----------- | ------------ |
| Day         | Locrian     | 7            |
| Dawn        | Dorian      | 7            |
| Dusk        | Aeolian     | 6            |
| Night       | Aeolian     | 3            |

Most loops play once per trigger. The bass loops may repeat once or twice and use a trigger range of 0 to 24 bars. The nighttime-only loop uses a trigger range of 0 to 8 bars, while most other loops use a range of 0 to 16 bars. All `Cycle` loops disable fractional timing, one-at-a-time playback, and tail cutoff.

The `Cycle.fezsong.json` song uses the following loops:

```text
├── Cycle
│   ├── Aeolian_Antecedent_3Bars
│   ├── Aeolian_Bass_4Bars
│   ├── Aeolian_Consequent_3Bars
│   ├── Aeolian_CounterArp_8Bars
│   ├── Aeolian_MainArp_8Bars
│   ├── Aeolian_Nighttime_13Bars
│   ├── Aeolian_Triplets_9Bars
│   ├── Dorian_Antecedent_3bars
│   ├── Dorian_Bass_4bars
│   ├── Dorian_Consequent_3bars
│   ├── Dorian_CounterArp_8bars
│   ├── Dorian_MainArp_8bars
│   ├── Dorian_Ostinato_2bars
│   ├── Dorian_Triplets_9bars
│   ├── Locrian_Antecedent_3bars
│   ├── Locrian_Bass_4bars
│   ├── Locrian_Consequent_3bars
│   ├── Locrian_CounterArp_8bars
│   ├── Locrian_MainArp_8bars
│   ├── Locrian_Ostinato_4bars
│   └── Locrian_Triplets_9bars
```

Here is the song during daytime:

![](/wiki/assets/images/editor/diez_cycle_day.mp3)

Here is the song during nighttime:

![](/wiki/assets/images/editor/diez_cycle_night.mp3)

The nighttime arrangement is less dense and has a distinctly different sound.

## Reference

A more detailed description of the properties is available in the [FEZSONG format reference](/wiki/content/formats/fezsong).

For information about the song scripting API with `Sound` static entity, see the [Scripting Reference](/wiki/game/scripting).
