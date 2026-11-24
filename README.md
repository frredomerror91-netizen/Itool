# Itool

Itool 是面向 I wanna 玩家和制图者的 Windows 桌面工具，支持 GM8、GMS 和 I Wanna Maker（IWM）地图求解、地图转换和逐帧 TAS。

[下载最新正式版](https://github.com/frredomerror91-netizen/Itool/releases/latest) · [更新记录](CHANGELOG.md) · [SHA-256 校验](SHA256SUMS.txt)

## 主要功能

- **地图编辑与转换**　编辑物件、角色参数和房间边界，在 .jmap、.map 与 .itmap 格式间转换，并排检查和编辑源图与转换结果。
- **路线求解**　普通求解和含ya求解可从出生点寻找不同过法，按帧数和操作次数排序。支持窄口、连续起跳、平台、水域和藤蔓，也可从录像中的指定帧接着求解。
- **路线比较与回放**　在解列表比较跳法和多键取消次数，在 Input 中查看逐帧输入。路线支持回放、导出和继续改短。
- **XA 与 YA 分析**　查看正式起跳时的位置、固定后程与其他过法的可行 YA 范围，分析一段跳、二段跳和连续松键。
- **完整游戏 TAS**　为兼容的 GM8 游戏录制键鼠输入，逐帧编辑、读档、续录并比较分支。完整游戏 TAS 需要自行准备游戏文件。

## 运行环境与许可

适用于 Windows 10 / 11 x64，提供便携版及内置更新。GM8 录制使用 OpenGMK，其许可随包提供。[软件许可](LICENSE.txt) · [OpenGMK 项目与源码](https://github.com/OpenGMK/OpenGMK)
