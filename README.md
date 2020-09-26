# io_import_vmf

A Valve Map Format (.vmf) and Valve Material Type (.vmt) importer for Blender.

Also includes helpful wrappers for importing [HLAE .agr files](https://www.advancedfx.org/) and .qc/.mdl models with materials using the included material importer.

### Requires Blender 2.82 or newer.

### [Blender Source Tools](https://steamreview.org/BlenderSourceTools/) must be installed for importing models!

### Ships bundled with [Crowbar-Command-Line](https://github.com/UltraTechX/Crowbar-Command-Line) for automatic model decompilation.

## Installation
- Get the latest release from the [releases](https://github.com/lasa01/io_import_vmf/releases) tab.
- Go to Preferences > Addons > Install.
- Select the .zip file you downloaded.

### Latest from source
- Install Python.
- Clone the repository.
- Run `install.sh` or `install.ps1` depending on your OS.
- Follow the installation instructions above for the newly created .zip file.

## Usage

The importer can automatically extract the required files from the game files.
Materials and props, for example, require external game files for the import to succeed.
You can specify a game file cache path in the preferences to reuse some previously processed data for slightly faster reimports.

You need to go to the addon preferences to add game definitions which are used for loading these files.
Click the + button to add a new game definition. Press the "Detect from a game directory" button and select the game directory.
For CSGO that is installed in the default directory, you need to select `C:\Program Files (x86)\Steam\steamapps\common\Counter-Strike Global Offensive\csgo`.
The addon attempts to automatically detect the game name and relevant VPK files and directories inside the selected directory.
If your game includes content inside other directories, you can use the auto-detection on them too.
In case the addon fails to detect some VPK archives or you would like to add a directory without detecting the VPKs inside it,
you can use the + buttons to add them manually.

Blender may appear frozen when importing complex maps. To see the import progress and any errors in realtime, you can open the Blender console.
Unsupported material parameter warnings are normal, although they could mean that the importer can not recreate fully accurate materials.

### Maps
`File -> Import -> Valve Map Format (.vmf)`

Source maps that ship with the game are in a compiled `.bsp` file format.
This addon can only import them in the original `.vmf` format.
You can use [BSPSource](https://github.com/ata4/bspsrc) to decompile the map files into the `.vmf` format supported by this addon.

You can select what to import from the file dialog.
The more things you select, the slower the import progress will be, so you should select only the things you need.

Brushes, lights and overlays are fast to import, they should take less than a minute.
Importing materials can take a little longer. Importing props is extremely slow, it usually takes over 30 minutes for a full-sized map.

There is an option to optimize the imported props, which removes unneeded armatures from static props.
It is enabled by default, but you can disable it if you encounter issues with it.

Importing the sky converts the original cubemap into a Blender-compatible equirectangular format, so quality might suffer.
You can select a larger sky resolution to increase the quality, but this will also increase import time.

Importing the 3D sky origin allows you to select the 3D sky after importing and automatically transforming it to the correct position and scale.
After the import has finished, you need to manually select every object that belongs to the 3D sky.
Ensure you have the 3D sky origin (sky_camera) also selected and as the active object, and press `Object -> Transform VMF 3D sky` to transform the objects.

### Materials
`File -> Import -> Valve Material Type (.vmt)`

By default, the materials try to mimic the original appearance as much as possible.
They are however approximations and may appear different than ingame.

You can also import simpler versions of materials.
You should check it if you plan to export the materials outside Blender, since exporters are usually unable to read the more complicated material setups.

There are also options to select the texture interpolation type
and whether to allow backface culling in materials that don't disable it.

### **The following features are only supported on Windows:**

### QC / MDL (requires [Blender Source Tools](https://steamreview.org/BlenderSourceTools/) or [SourceIO](https://github.com/REDxEYE/SourceIO))
`File -> Import -> Source Engine Model (enhanced) (.qc/.mdl)`

### AGR (requires [afx-blender-scripts](https://github.com/advancedfx/afx-blender-scripts))
`File -> Import -> HLAE afxGameRecord (enhanced) (.agr)`

## Credits
- Me for the addon, [VMF and VMT parser](https://github.com/lasa01/vmfpy) and [VTFLib wrapper](https://github.com/lasa01/pyvtflib).
- ValvePython for [VPK](https://github.com/ValvePython/vpk) and [Valve KeyValues](https://github.com/ValvePython/vdf) parser.
- Nemesis for [VTFLib](http://nemesis.thewavelength.net/index.php?p=40).
- Artfunkel for [Blender Source Tools](http://steamreview.org/BlenderSourceTools/).
- ZeqMacaw and UltraTechX for [Crowbar](https://steamcommunity.com/groups/CrowbarTool) and [Crowbar-Command-Line](https://github.com/UltraTechX/Crowbar-Command-Line).
- REDxEYE for [SourceIO](https://github.com/REDxEYE/SourceIO).
- Devostated for testing and bug reporting.
- Alex Flint and Pete Florence for [bilinear interpolation code](https://stackoverflow.com/a/12729229).
- adamb70 for [Python-Spherical-Projection](https://github.com/adamb70/Python-Spherical-Projection).

## License
This project is licensed under the MIT license. See LICENSE for more information.
