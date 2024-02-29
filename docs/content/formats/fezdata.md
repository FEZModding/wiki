# FEZDATA format

## TODO

## JSON Data

`.fezdata.json` files contain FEZ language text localization data stored in a JSON format. This documentation presents a structure and purpose to each property in this file format. Descriptions are incomplete in some cases, and they might be incorrect due to lack of proper testing in the game itself, but that'll improve over time.

## Property definitions

### FezData

Top-level object stored in `.fezdata.json` JSON file.

|Property name|Type|Description|
|-|-|-|
|LanguageResources|[LanguageResource](#LanguageResource)|Dictionary of definitions for each language, with keys being [ISO 639-1 two-letter  Code \(external link\)](https://www.loc.gov/standards/iso639-2/php/code_list.php) |

### LanguageResource

|Property name|Type|Description|
|-|-|-|
|TextLine|String|Dictionary with definitions for each line of text in the containing language, with keys being identifiers used by the level/game. |
