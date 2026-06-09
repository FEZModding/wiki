# FEZTXT Format

FEZTXT files contain localized game text. FEZRepacker stores them as UTF-8-encoded JSON files with the `.feztxt.json` extension.

## JSON Structure

The root object maps language codes to language resources. Each language resource maps text IDs to strings:

```text
Dictionary<string, Dictionary<string, string>>
```

```json
{
  "": {
    "ExampleGreeting": "HELLO!",
    "ExampleStatus": "CUBES: {0}"
  },
  "fr": {
    "ExampleGreeting": "BONJOUR !",
    "ExampleStatus": "CUBES : {0}"
  }
}
```

The empty language code (`""`) contains the default English text. When the selected language or requested text ID is unavailable, the game falls back to the corresponding entry in this default language resource.

## Language Codes

The resource files contain the following language keys:

| Key  | Language   |
| ---- | ---------- |
| `""` | English    |
| `fr` | French     |
| `it` | Italian    |
| `de` | German     |
| `es` | Spanish    |
| `pt` | Portuguese |
| `ja` | Japanese   |
| `ko` | Korean     |
| `zh` | Chinese    |

Non-default language resources may omit entries.

## Text Entries

Each entry consists of a text ID and its displayed string:

| Part    | Type   | Description                                           |
| ------- | ------ | ----------------------------------------------------- |
| Text ID | String | Text identifier (ID)                                  |
| Text    | String | Text displayed for that ID in the containing language |

Text IDs should match across language resources so each translation corresponds to the same game text. Preserve IDs exactly when editing them because references in other assets are not updated automatically.

Text strings may contain:

- Escaped line breaks such as `\r\n`.
- Composite-format placeholders such as `{0}`.

Translations must preserve any placeholders expected by the game.
