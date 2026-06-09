---
sort: 12
---

# Localization

**Po** creates and edits localization files (`.feztxt.json`) used to translate the game's text:

![](/wiki/assets/images/editor/po.png)

The game supports the following languages:

- English (default)
- French
- Italian
- German
- Spanish
- Portuguese
- Japanese
- Korean
- Chinese

The localization files are stored in the `Resources/` folder:

- `GameText`: Dialogue and gameplay text
- `StaticText`: Menus, prompts, and interface text
- `CreditsText`: Credits text

```note
The game represents text internally using UTF-16, while `.feztxt.json` files store text as UTF-8-encoded JSON. See the [FEZTXT format reference](/wiki/content/formats/feztxt) for the structure of localization data.
```

## Layout

The toolbar has the following buttons, from left to right:

- **Language Selector**: Selects a language for translation.
- **Add New Entry**: Adds a new entry to the localization data.

The editor displays text strings in a table:

| Column           | Description                                     |
| ---------------- | ----------------------------------------------- |
| ID               | Stable identifier referenced by game content.   |
| Source text      | English text used as the translation source.    |
| Translation text | Text for the language selected above the table. |

Each text row has a unique ID. Levels, scripts, NPC speech lines, and game services refer to these IDs to display text.

## Editing Text

Click a table cell to open its menu, then choose `Edit This Cell`.

![](/wiki/assets/images/editor/po_edit.png)

Editing behavior depends on the selected column:

- **ID**: Renames that ID in every language.
- **Source text**: Changes the English entry.
- **Translation text**: Changes the entry for the selected language.

Text can contain multiple lines. Accept the edit dialog to apply the change.

```warning
Renaming an ID does not update other assets that may refer to it. Update those references separately.
```

## Adding and Removing Entries

Use `Add New Entry` above the table or from a cell's menu to create a text ID. The ID must be non-empty and must not already exist in the English language entries.

Choose `Delete This Entry` from a cell's menu to remove the ID from every language after confirmation.

## Font Files

To edit the fonts used for localized text in the game, see the [Sprite Fonts](/wiki/editor/sprite_fonts) page.
