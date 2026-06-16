---
sort: 8
---

# NPC Metadata

NPC instances edited in [Eddy](/wiki/editor/levels) have properties that apply only within a single level. Properties shared by every instance of a particular NPC are instead stored in a separate metadata file (`.feznpc.json`), avoiding duplication across levels.

**Mu** is a small, specialized editor for modifying an NPC's shared behavior properties:

![](/wiki/assets/images/editor/mu.png)

NPC metadata is usually stored beside the character's animations:

```text
Character Animations/<Character Name>/Metadata.feznpc.json
```

Metadata does not store NPC positions, dialogue, or actions. Its properties override the corresponding properties of NPC instances within levels.

## Properties

You can edit the following properties:

- **Walk Speed**: Controls how quickly the NPC moves while walking.

<video width="100%" controls>
  <source src="/wiki/assets/images/editor/mu_damn_he_is_fast.mp4" type="video/mp4">
</video>

- **Avoids Gomez**: Makes the NPC attempt to move away when Gomez gets too close.

<video width="100%" controls>
  <source src="/wiki/assets/images/editor/mu_there_is_no_escape_old_man.mp4" type="video/mp4">
</video>

- **Sound Path**: Defines a shared NPC sound relative to the `Sounds/` directory. For example:

<video width="100%" controls>
  <source src="/wiki/assets/images/editor/mu_possessed_by_dot.mp4" type="video/mp4">
</video>

This example uses this line:

```text
Dot/Talk
```

- **Sound Actions**: Lists the actions, such as `Walk` or `Talk`, that use **Sound Path**. An action-specific sound overrides the shared sound.

## Reference

A more detailed description of the properties is available in the [FEZNPC format reference](/wiki/content/formats/feznpc).
