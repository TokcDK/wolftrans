# Wolf Trans
(English description is *Below*, please pull down)

* 以下为Wolf Trans软件自身说明。Wolf RPG游戏汉化翻译全流程说明请看这里[READMEfullcourse](READMEfullcourse.md)

Wolf Trans是一个Wolf RPG游戏的辅助翻译工具，用于减少汉化/本地化Wolf RPG游戏的难度和工作量。它将游戏数据文件(.dat, .project, .mps)中所有可翻译的文字内容抽出为txt文本文件，翻译者翻译编辑txt文件后，它再将翻译后的文字整合进数据文件重新输出(.dat, .project, .mps)。

WolfTrans抽出的txt是由一个个类似这样的翻译段组成的：

    > BEGIN STRING
    【はじめから】
    > CONTEXT MPS:Map000/events/0/pages/1/36/Picture < UNTRANSLATED
    > END STRING
翻译者只需要将翻译后的内容填入最后一个> CONTEXT 和> END STRING之间即可

    > BEGIN STRING
    【はじめから】
    > CONTEXT MPS:Map000/events/0/pages/1/36/Picture < UNTRANSLATED
    【从头开始】
    > END STRING
## 安装
下载所有源代码后解压到一个文件夹即可

另外本工具使用ruby编写，你需要安装ruby，这里下载http://rubyinstaller.org/downloads/

## 使用
首先，建立一个文件夹`work_dir`，将已经解包的游戏数据文件的`Data\BasicData\`和`Data\MapData\` 文件夹复制到`work_dir`。例如：

    xcopy "D:\gamename\Data\BasicData" "D:\transwork\Data\BasicData" /I
    xcopy "D:\gamename\Data\MapData" "D:\transwork\Data\MapData" /I
    
确认你已经安装好了ruby. 用ruby运行Wolf Trans安装文件夹里的**bin\wolftrans**，例如:
    
    ruby d:\wolftrans\bin\wolftrans 
    
wolftrans的用法和参数如下:

    wolftrans work_dir patch_dir out_dir [localecode]

如果`patch_dir`不存在，它将自动建立并将抽出的可翻译文本生成txt文件存于此文件夹。`out_dir`将用于存放整合了翻译文本后重新输出的数据文件。

**警告：软件每次运行都会先清空`out_dir`的所有内容，请小心**

`localecode`: 此参数用于设置翻译语言的编码代码页，默认（不设置此参数）为英文。例如GBK为简体中文, CP950为繁体中文, CP949为韩文...更多请参考https://docs.ruby-lang.org/ja/latest/class/Encoding.html 示例：

当目标翻译语言为英文时：

    ruby d:\wolftrans\bin\wolftrans "D:\transwork" "D:\transwork\patch" "D:\transwork\output"
    
当目标翻译语言为简体中文时：

    ruby d:\wolftrans\bin\wolftrans "D:\transwork" "D:\transwork\patch" "D:\transwork\output" "GBK"

## 提示

本软件会将相同的文字内容抽出为同一个翻译段，并将它放在首次出现的地方对应的txt文件中。比如游戏数据中多个地方都有“はい”这句话，抽出的翻译段如下，存于`patch_dir`\Patch\dump\mps\Map000.txt 中

    > BEGIN STRING
    はい
    > CONTEXT MPS:Map001/events/0/pages/1/23/Choices
    > CONTEXT MPS:Map002_A_1/events/0/pages/1/23/Choices
    > CONTEXT MPS:Map002_A_3/events/4/pages/7/3/Choices
    > CONTEXT MPS:Map002_A_3/events/9/pages/2/21/Choices
    > CONTEXT MPS:Map003/events/5/pages/1/3/Choices
    > CONTEXT MPS:Map003/events/24/pages/2/4/Choices
    > CONTEXT MPS:Map003/events/32/pages/2/4/Choices
    > CONTEXT MPS:Map003/events/34/pages/2/5/Choices
    > CONTEXT MPS:Map004/events/5/pages/2/4/Choices
    > CONTEXT MPS:Map004/events/9/pages/2/12/Choices
    > CONTEXT MPS:Map004/events/20/pages/2/6/Choices
    是
    > END STRING

这样只需要在map000.txt中翻译一次，其他的地方也都会自动生成翻译后的数据文件(.dat, .project, .mps)。但这也带来一个问题，“はい”在不同的语境上下文中可能有不同的意思，比如表示“知道了”、“好”等等，统一翻译成“是”比较生硬。此时可以自己在相应的地方写一个翻译段，比如在map004.txt里，

    > BEGIN STRING
    はい
    > CONTEXT MPS:Map004/events/5/pages/2/4/Choices
    好
    > END STRING
就能实现同一原文不同译文。



## 声明
作者对使用此软件造成的任何损失概不负责。为了避免意外，防止翻译成果付之东流，请经常备份`patch_dir`里的内容。

----------------------------------------------------------------------------------------------------
# Wolf Trans
## A translation tool for Wolf RPG Editor games
![](http://i.imgur.com/fzuJjsU.png)

## Summary
Wolf Trans is a set of tools to aid in the translation of games made using
[Wolf RPG Editor](http://www.silversecond.com/WolfRPGEditor/). The syntax and functionality is inspired primarily by the [RPG Maker Trans](http://rpgmakertrans.bitbucket.org/) project.

## Installation
Download all source code zip file and uncompress to a folder.
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
First, make a folder as `work_dir`, and copy unpackaged game data files `Data\BasicData\` and `Data\MapData\` folders to `work_dir`. e.g.

    xcopy "D:\gamename\Data\BasicData" "D:\transwork\Data\BasicData" /I
    xcopy "D:\gamename\Data\MapData" "D:\transwork\Data\MapData" /I
    
Make sure you have already installed ruby. Run **bin\wolftrans** in Wolf Trans installed folder using **ruby**. For exsample:
    
    ruby d:\wolftrans\bin\wolftrans 
    
Currently, Wolf Trans can be invoked with the command line:

    wolftrans work_dir patch_dir out_dir [localecode]

If `patch_dir` does not exist, it will be automatically generated with the text contained in the data files of the game in `work_dir`. `out_dir` will contain the patched game.

**WARNING: OUT_DIR WILL BE *DELETED* IF IT EXISTS. USE CAUTION.**

`localecode`: Set Encoding CodePage for other languages, default(not set) for English. eg. GBK for Simplified Chinese, CP950 for Traditional Chinese, CP949 for Korean... About Encoding CodePage, See this https://docs.ruby-lang.org/ja/latest/class/Encoding.html e.g.

When destination translated language is English:

    ruby d:\wolftrans\bin\wolftrans "D:\transwork" "D:\transwork\patch" "D:\transwork\output"
    
When destination translated language is Simplified Chinese:

    ruby d:\wolftrans\bin\wolftrans "D:\transwork" "D:\transwork\patch" "D:\transwork\output" "GBK"

## Disclaimer

This project is still in a very early state, and probably won't work with all games. Make sure to backup your translation work frequently in case of errors until this project is stable. I am not personally responsible for anything done by this tool.
