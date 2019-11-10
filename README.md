# Wolf Trans
## A translation tool for Wolf RPG Editor games
![](http://i.imgur.com/fzuJjsU.png)

## Summary
Wolf Trans is a set of tools to aid in the translation of games made using
[Wolf RPG Editor](http://www.silversecond.com/WolfRPGEditor/). The syntax and functionality is inspired primarily by the [RPG Maker Trans](http://rpgmakertrans.bitbucket.org/) project.

## Installation
Download all source code zip file and uncompress in a folder.
If you are using Windows, you will need to have Ruby installed first. You can download it from [here](http://rubyinstaller.org/downloads/).

## Example
The source code for the translation patch file used in the sample image above is the following:

    > BEGIN STRING
    ウルファール
    「ようこそ、\\r[WOLF,ウルフ] RPGエディターの世界へ！
    　私は案内人のウルファールと申します。
    > CONTEXT MPS:TitleMap/events/0/pages/1/65/Message
    Wolfarl
    "Welcome to the world of WOLF RPG Editor!
     I am Wolfarl, your guide."
    > END STRING

All of the translatable game text is first extracted by Wolf Trans into plaintext files, which can then be edited by a translator. Refer to RPG Maker Trans's documentation for now for a more thorough explanation, as the two share very similar designs.

## Usage
First, make a folder as `work_dir`, and copy unpackaged game data files `Data\BasicData\` and `Data\MapData\` folders to 'work_dir'. e.g.

    xcopy "D:\gamename\Data\BasicData" "D:\transwork\Data\BasicData" /I
    xcopy "D:\gamename\Data\MapData" "D:\transwork\Data\MapData" /I
    
Make sure you have already installed ruby. Run **bin\wolftrans** using **ruby**. For exsample:
    
    ruby d:\wolftrans\bin\wolftrans 
    
Currently, Wolf Trans can be invoked with the command line:

    wolftrans work_dir patch_dir out_dir [localecode]

If `patch_dir` does not exist, it will be automatically generated with the text contained in the data files of the game in `work_dir`. `out_dir` will contain the patched game.

**WARNING: OUT_DIR WILL BE *DELETED* IF IT EXISTS. USE CAUTION.**

localecode: default(not set) for English  
Set Encoding CodePage for other languages. eg. GBK for Simplified Chinese, CP950 for Traditional Chinese, CP949 for Korean...
About Encoding CodePage, See this https://docs.ruby-lang.org/ja/latest/class/Encoding.html e.g.

When destination translated language is English:

    ruby d:\wolftrans\bin\wolftrans "D:\transwork" "D:\transwork\patch" "D:\transwork\output"
    
When destination translated language is Simplified Chines:

    ruby d:\wolftrans\bin\wolftrans "D:\transwork" "D:\transwork\patch" "D:\transwork\output" "GBK"

## Disclaimer

This project is still in a very early state, and probably won't work with all games. Make sure to backup your translation work frequently in case of errors until this project is stable. I am not personally responsible for anything done by this tool.
