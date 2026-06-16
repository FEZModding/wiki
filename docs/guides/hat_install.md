# HAT installation

To install and update HAT, there is an installer that takes care of most of the patching work.

## Requirements

Before patching, you need to:

1. Obtain a copy of FEZ (preferably the PC 1.12 version, which is available on Steam or GOG).
2. Download [the stable release](https://github.com/FEZModding/HAT/releases) of the HAT installer.
3. On Linux and macOS, install the Mono package.

## Patching

![](/wiki/assets/images/hat/hat_installer_cli.png)

Run the installer. It searches for the `FEZ` executable in this order:

1. The path passed with `--path` or `-p`.
2. The current working directory.
3. The Steam library.
4. The GOG library.

If the installer cannot find the game executable, either move the installer into the FEZ game directory and run it there, or pass the game directory explicitly:

```powershell
.\HATinstaller.exe --path "C:\Program Files (x86)\Steam\steamapps\common\FEZ"
```

## Launching

After installation, the installer produces a patched version of the original `FEZ` executable. It is called `HAT.exe` on Windows and `HAT` on Linux and macOS. To use the vanilla version, start the original `FEZ` executable instead.

![](/wiki/assets/images/hat/hat_mod_loader.png)

## Updating

To update HAT, download the newer installer and run it against the same FEZ directory.

## Modding

Start the game through `HAT` once. It will create the `Mods` directory.

To install a mod, place the mod's folder or `.zip` archive inside `Mods`. A valid HAT mod has a `Metadata.xml` file at the root of the folder or archive.

For more details about valid mod layouts, see [HAT mod structure](/wiki/guides/hat_mod_structure).

## Troubleshooting

### Mod is not loading

If a mod fails to load, check the latest log file in the `Debug Logs` directory inside game's data folder:

| OS      | Default FEZ application data directory         |
| ------- | ---------------------------------------------- |
| Windows | `%APPDATA%/FEZ/`                               |
| Linux   | `$XDG_DATA_HOME/FEZ/` or `~/.local/share/FEZ/` |
| macOS   | `~/Library/Application Support/FEZ/`           |
