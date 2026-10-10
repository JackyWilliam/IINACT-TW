# DACT 台服 IINACT 依赖

本仓库是 [DalamudActCompat-TW](https://github.com/JackyWilliam/DalamudActCompat-TW) 的独立台服依赖源码库，基于 [PlusoneChiang/IINACT](https://github.com/PlusoneChiang/IINACT) 的 `tc/api13_net9`（`0788c177c5df622c9e20c4f00027b873732b5606`）合入 DACT 嵌入式 ACT、OverlayPlugin 和 Host 兼容层。目标为台服 API 13 / .NET 9。

构建及完整回归由主仓库的 [Taiwan Build](https://github.com/JackyWilliam/DalamudActCompat-TW/actions/workflows/build.yml) 执行。请递归克隆主仓库并运行 `tools/build-taiwan.ps1`，依赖由 gitlink 与哈希锁文件固定。本仓库不发布独立 IINACT 安装包，继承的独立插件发布工作流未启用。

DACT 台服问题请提交到 [DalamudActCompat-TW Issues](https://github.com/JackyWilliam/DalamudActCompat-TW/issues)。原作者版权、GPL-3.0 及第三方许可保持，以下原上游说明保留用于溯源，其中安装与构建入口不适用于 DACT 台服包。

---

![icon](https://github.com/marzent/IINACT/blob/main/images/icon.ico?raw=true)

# IINACT

A [Dalamud](https://github.com/goatcorp/Dalamud) plugin to run the [FFXIV_ACT_Plugin](https://github.com/ravahn/FFXIV_ACT_Plugin) in an [ACT](https://advancedcombattracker.com/)-like enviroment with a heavily modified port of [Overlay Plugin](https://github.com/OverlayPlugin/OverlayPlugin) for modern .NET.

The data source here is only based on [Unscrambler](https://github.com/perchbirdd/Unscrambler) and does not require any extra injection with [Deucalion](https://github.com/ff14wed/deucalion) or network capture with elevated privileges.

This will **not** render overlays by itself, use something like [Browsingway](https://github.com/Styr1x/Browsingway), [Next UI](https://github.com/kaminaris/Next-UI), [hudkit](https://github.com/valarnin/hudkit) (Linux only) or [Bunny HUD](https://github.com/marzent/Bunny-HUD) (macOS only) to display Overlays.


## Why

- ACT is too inconvenient IMHO for just wanting to have the game data parsed and served via a WebSocket server
- Drastically more efficent than ACT, in part to .NET 7.0, in part to a more sane log line processing (disk I/O is not blocking LogLineEvents and happening on a separate lower priority thread)
- Due to the above and running fully inside the game process CPU usage will be orders of magnitude (not exaggerating here) lower when running under Wine compared to network-based capture
- Uses an ultra fast and low latency WebSocket server based on [NetCoreServer](https://github.com/chronoxor/NetCoreServer)
- Doesn't use legacy technology that hurts Linux and macOS users
- Follows the Unix philosophy of just doing one thing and doing it well   

## Installing 

> **Warning**  
> No support will be provided on any Dalamud official support channel. Please use the [Issues](https://github.com/marzent/IINACT/issues) page or [Discord](https://discord.gg/pcexJC8YPG) for any support requests. Do NOT ask for support on the [XIVLauncher & Dalamud Discord](https://discord.gg/holdshift), as support for 3rd-party plugins is not provided there. 

Install instructions can be found [here](https://www.iinact.com/installation/), but are indentical to any other 3rd-party plugin repository.

## How to build

Just run 
```
git clone --recurse-submodules https://github.com/marzent/IINACT.git
cd IINACT
dotnet build
``` 
on a Linux, macOS or Windows machine with the [.NET 7 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/7.0). 

You will need to be able to reference Dalamud as well, meaning having an install of [XL](https://github.com/goatcorp/FFXIVQuickLauncher) or [XOM](https://github.com/marzent/XIV-on-Mac) on Windows and macOS respectively. On Linux `DALAMUD_HOME` needs to be correctly set (for example `$HOME/.xlcore/dalamud/Hooks/dev`).

## FAQ

**Where are my logs?**

- In your Documents folder. For Windows users, `C:\Users\[user]\Documents\IINACT`. For Mac/Linux users, same thing, but relative to your wine prefix.

**Are these logs compatible with FFLogs? Can I use the FFLogs Uploader?**

- Yes! 100% compatible.
