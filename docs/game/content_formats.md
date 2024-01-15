# FEZ Content Specification

FEZ is a game built on Microsoft XNA Game Studio, which distributes all its content as a binary data stored in a proprietary XNB format. This format is then packed into a simple containers with `.pak` extension. This specification defines the format of these containers and XNB files with attention to details specific to FEZ.

```tip
Keep in mind that underlying knowledge of these formats is **not** required for modding purposes, as our current modding environment takes advantage of content conversion to more user-friendly formats. For more information, visit [Content Conversion](/wiki/content/content_conversion) page.
```

```note
Both XNB and PAK binary files are compatible with C#'s `BinaryReader` and `BinaryWriter`, meaning all of the fields are little-endian, and string fields are prefixed with 7-bit encoded integer. Additionally, the following documentation will use C#'s data types for describing fields.
```

## PAK packages

FEZ stores its assets in four package files that are buffered into a memory on game launch. Three packages, `Essentials.pak`, `Updates.pak` and `Other.pak` (loaded in this order), contain all game assets except music, each in a binary XNB content format. Fourth package, `Music.pak`, is loaded separately and contains all music in an OGG format.

### PAK package format

The file starts with a small header, containing an integer indicating a number of files in this archive, followed by an array of files.

|Field Type|Description|
|-|-|
|`uint`|File count defining the size of following array.|
|File Array|Array of variable-sized files, placed one after another.|

Every file in the array is represented as follows:

|Field Type|Description|
|-|-|
|`string`|Path and name of the file without its extension.|
|`uint`|Size of the file data in bytes.|
|`byte[]`|File data.|

Types of files stored in the archive can vary. Because file extensions are not included in their paths, the only indication of a file type is its own header and path/name. FEZ packages contain three types of files:

- **XNB** - Microsoft XNA Game Studio 4.0 compiled content containers. Stores textures, sound effects, triles, levels, scripts and other miscellaneous data.
- **OGG** - digital multimedia container. Stores music.
- **FXC** - files that can be located in the `effects` directory. They're compiled XNA effect files.

Path of the file can be mixed case. However, FEZ expects them to be lowercase when loading assets.

It is possible for package to contain multiple files with the same path - for instance, in `effects` directory of `Updates.pak` there are multiple effect files which are stored as both FXC files and XNB `Effect` assets. The game seem to ignore duplicates within single package and across multiple ones, leaving only the first one cached in memory.

## XNB files

Most of assets in the package files are stored in compressed XNB content format, produced by XNA Game Studio.

### XNB file format

```note
This is a rough description of the format, with attention to FEZ-specific details. For full format specification, consult the [XNB Content Format documentation](https://github.com/SimonDarksideJ/XNAGameStudio/wiki/Compiled-(XNB)-Content-Format)
```

Header of each XNB file has following structure:

|Field Type|Description|
|-|-|
|`char[3]`|Format identifier. Should be equal to `['X', 'N', 'B']`.|
|`char`|Target platform. Possible values are `w`, `m` and `x` for MS Windows, Windows Phone 7 and Xbox 360 respectively.|
|`byte`|XNB format version. FEZ uses `5` - XNA Game Studio 4.0.|
|`byte`|Flag bits. See below for details.|
|`uint`|Compressed file size, including header.|

Flag bits can contain following flags:

- `0x01` - content is for HiDef profile (used for FEZ assets),
- `0x40` - data is compressed (LZ4, unused for FEZ),
- `0x80` - data is compressed (LZX, used for all original FEZ assets).

If compression flag is set, the rest of the file is compressed and prefixed with `uint` representing the size of this data after decompression. In case of FEZ, slightly modified LZX algorithm is used for compression. For details, visit [XNB reader code from open source implementation of MonoGame](https://github.com/labnation/MonoGame/blob/d270be3e800a3955886e817cdd06133743a7e043/MonoGame.Framework/Content/ContentManager.cs#L405).

Uncompressed data (or non-compressed file content after header) should look like this:

|Field Type|Description|
|-|-|
|`7BitEncodedInt`|Type reader count, defining the number of elements in following array.|
|Type Reader Info Array| An array of type reader information blocks.|
|`7BitEncodedInt`|Shared resource count, defining the number of additional resources in array later on. Always 0 in FEZ.|
|Object| The primary resource of the XNB file.|
|Object Array| Shared resources array. In FEZ, none of the original XNB files contain additional resources.

Each `Type Reader Info Array` entry stores information about the `ContentTypeReader<T>` subclass that was used to read the informations within this file:

|Field Type|Description|
|-|-|
|`string`|Type reader name - .NET assembly qualified name of a subclass.|
|`int`|Version number, usually zero.|

In original XNB files, type reader name includes assembly name specification (which contains assembly identifier, version, culture and public key token). In most cases, they're not required by the game to read the asset file.
However, sometimes it is necessary to include it, especially for readers and types in FezEngine namespace. For instance, the way it's done in FEZ Repacker is by including simplified assembly name specification to every data structure that can be stored in XNB files.

Each Object is a reference to a type reader, followed by a raw data, like so:

|Field Type|Description|
|-|-|
|`7BitEncodedInt`|Object type. If non-zero, then `(type - 1)`th entry of Type Reader Info Array is used.|
|`byte[]`|Raw object data. Empty if object type is zero.|

XNB reader uses the object type to determine what reader should be used to read the raw object data. Readers can use other readers to read underlying properties of the object, in which the same rule of reading object applies (a 7-bit encoded object identifier and a raw data is expected, then read by a corresponding content type reader). For primitive types like `int`, `float`, `bool`, etc., the data is written directly into a binary format.

Even though the structures of these objects are static, the correct type identifiers are still required by the game, and error will be thrown if mismatch of types is detected.

Additionally, binary data of an object may not ideally reflect its structure, and it's up to the corresponding content type reader to interpret it correctly.

### Content types

Based on primary reader type of every XNB file contained within FEZ's packages, we can distinguish 13 unique data types.

|XNB content type name|Main purpose|
|-|-|
|Texture2D|Sprites and textures|
|AnimatedTexture|Animated textures|
|ArtObject|3D models of art objects|
|TrileSet|Texture and models of level blocks (triles)|
|Dictionary[String,Dictionary[String,String]]|Language texts|
|SpriteFont|Bitmap font|
|Level|Level data|
|MapTree|World map data|
|NpcMetadata|NPC behaviour information|
|Sky|Skybox structure|
|TrackedSong|Song information|
|Effect|Binary XNA effect file container|
|SoundEffect|WAV sound effect container|

For now, for the exact method of storing each of these data types, refer to the implementation of `ContentTypeReader` for each type in FEZ decompilation.
