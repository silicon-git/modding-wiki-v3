Modding Danganronpa V3: Killing Harmony requires familiarity with the game's file formats.

TODO: Maybe make individual pages for each format. Maybe also make full lists of files in each format and their locations, for putting on these individual pages
TODO: AWB, ACB, maybe others/less understood formats (PPP, post processing file format)

## Terminology
**Archives** combine multiple files together into one file, which may be smaller, easier to distribute, and/or harder for a user to change on accident. Most games have files in archive formats which need to be unpacked to be viewed.
**Unpacking** TODO: Definition
**Repacking** TODO: Definition
**Extracting** TODO: Definition
TODO: Definitions for Textures? Models? Strings?

## .CPK
.CPK files are the first archive used to store DRV3's files. They stem from DRV3's usage of CRIWARE. DRV3's files are stored in .CPK archives by default. 
The unpacked files from .CPK archives can be placed in the `win` folder and used without repacking. However, files in .CPK archives will be prioritized when running the game, so move all .CPKs out of the `win` folder when trying to test unpacked files.
When developing or [distributing mods](Distributing%20Mods), data read from .CPK file archives can be added to or replaced through [CRI FileSystem V2 Hook](https://github.com/Sewer56/CriFs.V2.Hook.ReloadedII) for [Reloaded-II](https://github.com/Reloaded-Project/Reloaded-II). This makes it easy for users to play a mod without actually changing the files in their install of DRV3. 

## .DAT
TODO: .DAT files are cursed abominations
There are .DAT files that store data that can be unpacked into a .CSV spreadsheet by Harmony-Tools, and then there are the *other* .DAT files (nonstop debate data, minigame data(?), monopad map data)

## .SFL
.SFL is the format used for image transformations and animations. These files specify how CGs and other 2D image assets should display and animate in-game.
.SFL is very obtuse, and still being researched. No editing tools for it currently exist.

## .SPC
.SPC is the archive format used by DRV3 for most files within the initial .CPK. The format is well understood and can be unpacked and repacked with [[DRV3-Sharp]] or [[Harmony-Tools]].
Unlike .CPKs, .SPCs cannot be recognized by the game if they are left unpacked. Be sure to repack after making modifications to data in .SPC files.

## .SRD
.SRD, .SRDI, and .SRDV are the file formats used to store image textures and 3D model data. A .SRD file will usually have a corresponding .SRDI or .SRDV file.
TODO: can't remember whether SRD or SRDI/SRDV contains the actual model/texture data. one of them is just the filenames/identifiers
.SRD files can be matched to their .SRDI/.SRDV counterparts and have their texture data extracted using [[DRV3-Sharp]] or [[Harmony-Tools]]. 
DRV3-Sharp is needed to extract 3D model data. Harmony-Tools is needed to (imperfectly) repack 2D texture data.
No solutions currently exist for modifying 3D models or their associated textures.

## .STX
.STX files are used to store player-facing text. They can be unpacked and repacked using [[DRV3-Sharp]] or [[Harmony-Tools]].
In the `wrd_script` folder, .SPCs containing .STX files have at least one corresponding .SPC which contains .WRD files. DRV3-Sharp's .WRD unpacking implementation is able to match these .SPCs to each other and unpack/repack their contents in tandem for easy editing.
Harmony-Tools is designed to unpack and repack .STX files in a manner useful to fan translators, who will need to modify text more than event script. Since .WRD files contain the data specifying which character is speaking for a given line of dialogue, Harmony-Tools can match .WRD files to .STX files and extract them into a .JSON document containing dialogue with speaker data.

## .WRD
.WRD files are used to store the event scripting of the game. They can be unpacked and repacked using [[DRV3-Sharp]].
In the `wrd_script` folder, .SPCs containing .WRD files have at least one corresponding .SPC which contains .STX files. DRV3-Sharp's .WRD unpacking implementation is able to match these .SPCs to each other and unpack/repack their contents in tandem for easy editing.
.WRD files are written in a unique [syntax](WRD%20Syntax.md). Mastering this syntax allows modders to transform the flow and events of DRV3's gameplay.