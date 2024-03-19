# FEZDATA format

## JSON Data

`.fezdata.json` files contain FEZ language text localization data stored in a JSON format. This documentation presents a structure and purpose to each property in this file format. Descriptions are incomplete in some cases, and they might be incorrect due to lack of proper testing in the game itself, but that'll improve over time.

## Property definitions

### FezData

Top-level object stored in `.fezdata.json` JSON file.

```note
LanguageResources and LanguageResource are names used solely to better convey the structure of the FezData file, and are never refered to as such in the game code, instead just being a single `Dictionary<string, Dictionary<string, string>>`.
```

```note
The game will default to the entry with the key of `""` if an entry for the current game language was not found, or if the language was found but did not contain the desired entry.
```

|Property name|Type|Description|
|-|-|-|
|LanguageResources|[LanguageResource](#languageresource)|Dictionary of definitions for each language, with keys being [ISO 639-1 two-letter  Code \(external link\)](https://www.loc.gov/standards/iso639-2/php/code_list.php) |

### LanguageResource

|Property name|Type|Description|
|-|-|-|
|TextLine|String|Dictionary with definitions for each line of text in the containing language, with keys being identifiers used by the level/game. |
