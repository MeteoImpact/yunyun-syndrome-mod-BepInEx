# Yunyun Denpa Syndrome Translation Mod (BepInEx)

[![Discord](https://img.shields.io/discord/1497391770118393967)](https://discord.gg/jYjTd5qpKv)
[![Release](https://github.com/YYDS-EN-Fanslation/yunyun-syndrome-mod/actions/workflows/release.yaml/badge.svg)](https://github.com/YYDS-EN-Fanslation/yunyun-syndrome-mod/releases)
[![Releases](https://img.shields.io/github/v/release/YYDS-EN-Fanslation/yunyun-syndrome-mod?label=Latest%20Version)](https://github.com/YYDS-EN-Fanslation/yunyun-syndrome-mod/releases)

This is a mod for [Yunyun Syndrome!? Rhythm Psychosis](https://store.steampowered.com/app/2914150/Yunyun_Syndrome_Rhythm_Psychosis/)
from the [YYDS EN Fanslation Project](https://github.com/YYDS-EN-Fanslation). It loads and applies patches which can modify in-game text and images in order
to tweak, change and fix the game's localization. The BepInEx port of the mod is maintained by MeteoImpact, whose most recent translation is currently included in the release.

Looking for something else?
- [Yunyun Denpa Syndrome Translation Mod (MelonLoader)](https://github.com/YYDS-EN-Fanslation/yunyun-syndrome-mod) - Original MelonLoader version of the mod
- [Yunyun Syndrome Patch](https://github.com/YYDS-EN-Fanslation/yunyun-syndrome-patch) - Alternative patcher with simple installer
- [Yunyun Syndrome Translation](https://github.com/YYDS-EN-Fanslation/yunyun-syndrome-translation) - Main project's translation repository
- [YYDS EN Fanslation Project](https://github.com/YYDS-EN-Fanslation) - More information about YYDS EN Fanslation Project
- [YYDS EN Fanslation Discord](https://discord.com/invite/Pd3CWA8BfD) - Our Discord

## How to Install

1. Download [BepInEx](https://github.com/BepInEx/BepInEx/releases/) and extract to your root Yunyun Denpa Syndrome folder (by default C:\Steam\steamapps\common\Yunyun_Syndrome).

2. Download the mod archive from the [Releases page](https://github.com/MeteoImpact/yunyun-syndrome-mod-BepInEx/releases/) and extract to your root Yunyun Denpa Syndrome folder.

3. **(optional)** Add/remove locale patches in `Yunyun_Syndrome\UserData\LocalePatches` directory. For example:
    - [Radish](https://github.com/Radish-sys)'s MTL: [JP -> EN](https://raw.githubusercontent.com/YYDS-EN-Fanslation/yunyun-syndrome-translation/refs/heads/master/YYDS%20EN%20Fanslation%20-%20MTL%20Patch.csv)
    - Google Translate MTL: [JP -> EN](https://raw.githubusercontent.com/funmaker/YunyunLocalePatcher/refs/heads/master/examples/20-english-mtl.csv) (no dialogues)
    - [Moshi Moshi](https://github.com/lIllIIlI)'s: [JP -> EN](https://raw.githubusercontent.com/funmaker/YunyunLocalePatcher/refs/heads/master/examples/20-faithful-english.csv) ([#2](https://github.com/funmaker/YunyunLocalePatcher/pull/2)) (no dialogues)

## How to make patches?

- (optional) Once you have the mod installed, you can run the game with the `--localepatcher.dumpstrings` launch option to create a `00-base.csv`
  file in `Yunyun_Syndrome\UserData\LocalePatches` which will contain all the translation related strings.
- **Make sure to remove `--localepatcher.dumpstrings` flag from launch options and delete/move `00-base.csv` file!** YunyunLocalePatcher will
  not load any patches if that flag is present in launch options!
- You can import `00-base.csv` into this [spreadsheet](https://docs.google.com/spreadsheets/d/1nKseRzV7VLbYQeV79oiWpTRxfSj_n8xqap94Bf6t2I4/edit?gid=0#gid=0&fvid=826278446)
  to make it editing easier.
    - Make sure to select `A1` cell(contains "TableName"), `Replace data at selected cell` in `Import location`, `Comma` in `Separator type` 
      and uncheck `Convert text to numbers, dates and formulas`
- Make your changes by editing `New Text` column in `Editor` tab. All your changes should be reflected in `Patch Export` tab. In order to create
  a patch, go to `Patch Export` tab and save it as `Comma-Separated Values (CSV)`.
- Technical note: YunyunLocalePatcher expects patches to be in CSV format([RFC 4180](https://www.rfc-editor.org/rfc/rfc4180.html)).
  It should contain exactly 3 columns(TableName, Key, Text), just like the `00-base.csv` file generated in first step.

## How does it work?

This mod simply hooks into Unity Localization using ITablePostprocessor interface and modifies StringTables as they are loaded.
The patches loaded from `Yunyun_Syndrome\UserData\LocalePatches\*.csv` are applied in alphabetical order, so you can use names
like `10-initial.csv`, `50-common.csv`, `90-extra.csv`, etc to control the order in which patches are applied.

For more details about patch format, [read this](https://github.com/YYDS-EN-Fanslation/yunyun-syndrome-translation#format).
