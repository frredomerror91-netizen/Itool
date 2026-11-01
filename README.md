# Itool 与 I wanna物理规律与机制

这里提供 Itool Windows 软件，以及按引擎独立编写的物理规律与机制资料。

## 下载

打开 [当前下载页：Itool 1.6.2 与资料库](https://github.com/frredomerror91-netizen/Itool/releases/tag/v1.6.2)，在 Assets 中选择：

| 文件 | 用途 |
| --- | --- |
| Itool-v1.6.2-win64.zip | Windows 64 位便携软件，当前为检查版 |
| I wanna物理规律与机制.zip | 五引擎资料，解压后从 README.md 开始阅读 |
| 对应的 .sha256 文件 | 核对下载完整性 |

## 使用软件

解压整个软件包，运行 `Itool/Itool.exe`，保留同目录的 `_internal` 文件夹。无需安装 Python。

软件提供地图编辑、内置模型试玩、路线回放与 YA 工具。地图页 F5 开始或暂停、F1 单帧、R 回起点、Esc 返回编辑；F9/F10 保存和恢复当前地图内的练习点。完整说明位于软件包内。

1.6.2 修正 Windows NumLock 置物与原生下拉框焦点问题，试玩在 Itool 画布内运行。当前仍是检查版：离线模型不等于原游戏实机验证，求解性能、任意地图覆盖及三份训练游戏全通目标尚未完成；人类求解暂未实现。已有算法和物理的范围限制继续保留。

## 阅读资料

解压资料包，打开 `I wanna物理规律与机制/README.md`。Markdown 可以用支持本地图片与链接的阅读器打开。

| 书册 | 适用对象 |
| --- | --- |
| GM8 | Yuuutu 2.17 |
| GMS | YoYoYo 1.51 |
| IWM | 已分析的固定 Windows 构建 |
| Jtool | 本地 1.3.6、Patrick 1.3.5 源码与 Tuhka 5.2 说明 |
| Cloud | 已分析的核心类与网格实现 |

各册包含教程版、专业版、连续全册、对应分章和附录；配套插图、地图、CSV 保留相对链接。版本身份、来源、社区署名、验证范围与未闭合环节随各册附录保留。资料的机制研究范围不因打包而升级为完整游戏认证。

## 校验与许可

Windows PowerShell 可运行 `Get-FileHash -LiteralPath '下载文件.zip' -Algorithm SHA256`，与对应 `.sha256` 或本仓库的 [SHA256SUMS.txt](SHA256SUMS.txt) 对比。两个 ZIP 内也提供逐文件校验清单。

软件许可与第三方组件条款见 [LICENSE.txt](LICENSE.txt) 及软件包内的许可文件。资料中的来源与社区署名见各册附录；本次整理没有授予额外的再分发许可。

## 本次整理

2026-11-01 更新当前下载内容与阅读入口，清理旧版 Release。旧标签与 Git 提交历史保留。
