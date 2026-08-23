# Cursor 完整汉化工具：一键把界面变成中文

> 本工具面向日常使用 Cursor 的用户，在**不修改 Cursor 核心程序**的前提下，将界面中的英文菜单、按钮、提示和说明替换为中文，降低阅读和操作成本。已实现**编辑器模式（Editor）**和**智能体模式（Agent）**两种界面的全面汉化。


## 工具介绍

Cursor 官方目前尚未提供中文界面或汉化包。常见做法是安装 VS Code 汉化扩展，菜单、通用设置等会变成中文，但智能体侧栏、Cursor 设置、插件市场等 **Cursor 专有界面** 往往仍是英文，给习惯中文界面的用户增加了学习和使用成本。

**Cursor 完整汉化工具** 通过向工作台注入带词典的运行时脚本，把 **Cursor 专有界面** 替换成中文，让日常使用的界面尽量一眼能读懂。**不要求**安装 Chinese (Simplified) Language Pack。

### 覆盖区域

- **设置页**：账户、模型、规则、工具与 MCP、隐私等选项
- **智能体窗口**：对话、命令面板、模式切换（计划 / 询问 / 调试 / 多任务）等
- **插件市场**：插件名称、简介、获取按钮及市场相关文案
- **其它界面**：欢迎页、Git 变更面板、部分通知与推广弹窗等

### 主要特点

- **无需官方语言包**：默认不安装、不依赖 Chinese (Simplified) Language Pack；仅通过注入脚本完成汉化。
- **注入汉化，覆盖 Cursor 专有界面**：通过注入脚本 + 本地词典，翻译智能体侧栏、Cursor 设置（账户 / 模型 / 规则 / MCP）、插件市场、欢迎页、Git 面板及部分通知弹窗等。
- **不改动核心程序，可一键还原**：只修改工作台相关文件（如 `workbench.html`），需要英文时运行「取消汉化」脚本即可恢复。
- **维护成本低**：Cursor 小版本更新后若有个别位置变回英文，再运行一次启动脚本即可，一般无需重装软件。
- **其它说明**：日常点得到的界面大多已是中文；个别菜单、动态文案或新版本新增词条可能仍为英文，可在词典中补充后重新注入。Agent 对话与模型生成内容不属于界面汉化范围。若仍希望使用官方语言包覆盖标准菜单，可自行安装或运行 `python Cursor_Localization_Tool.py --install-langpack`（可选，非必需）。Markdown 编辑器标签旁的 **Preview** 预览按钮保持英文，不翻译。

## 界面截图

<img width="2002" height="1360" alt="Cursor exe_20260604_000934" src="https://github.com/user-attachments/assets/b043419d-3ab1-4d26-a36a-9618694df310" />

<img width="2000" height="1360" alt="Cursor exe_20260604_000214" src="https://github.com/user-attachments/assets/3cd64d40-3d3b-435e-8a46-7bfa17c06434" />

<img width="2000" height="1360" alt="Cursor exe_20260604_001901" src="https://github.com/user-attachments/assets/d06f3f34-6896-470a-a75d-192cbdf268b5" />


## 如何使用

### 环境要求

汉化工具依赖 **Python 3.8+**（Windows 通过 `启动汉化_Win.bat` 调用，Mac/Linux 通过 shell 脚本调用）。

1. 下载并解压汉化工具（内含 `启动汉化_Win.bat` / `启动汉化_Mac.sh` 等）。
2. **Windows**：双击 `启动汉化_Win.bat`。**Mac / Linux**：在终端执行 `启动汉化_Mac.sh`。
3. 脚本会注入汉化（**不要求**安装官方简体中文语言包），按提示可选打开 Cursor。
4. **完全退出并重启** Cursor（不要只重载窗口）。

**Mac在终端中运行汉化脚本：**
1. 打开**终端**：按 `Cmd + 空格`，输入「终端」后回车。
2. 在终端输入 `bash`加空格，再把 `启动汉化_Mac.sh` 拖入窗口补全路径后回车，输入`Y`进行汉化。

本工具**不要求**安装 **Chinese (Simplified) Language Pack**。若你自行安装了该扩展并希望切换显示语言，可在命令面板运行 `Configure Display Language` 选择 **中文(简体)**（`zh-cn`）后完全重启；此步骤与本工具无关，纯属可选。

## 恢复英文

Windows 双击 `取消汉化_Win.bat`；Mac / Linux 运行 `取消汉化_Mac.sh`。

同样要**完全退出并重启**。取消汉化只撤销注入并恢复备份文件，不会卸载你自行安装的任何扩展。

## 路径配置

默认自动检测 Cursor 安装位置，一般无需修改。

**Windows**：Cursor 装在非默认路径时，用记事本打开 `启动汉化_Win.bat`（取消汉化时改 `取消汉化_Win.bat`），在 `cd /d "%~dp0"` 后面增加一行：

```bat
set CURSOR_INSTALL_DIR=D:\Program Files\cursor
```

路径需指向**含 `Cursor.exe` 的安装文件夹**。若用户数据目录也不在默认位置，可额外设置（一般不用改）：

```bat
set CURSOR_USER_DATA_DIR=C:\Users\你的用户名\AppData\Roaming\Cursor
```

**macOS / Linux**：在 `启动汉化_Mac.sh`（或 `取消汉化_Mac.sh`）开头增加：

```bash
export CURSOR_INSTALL_DIR="/Applications/Cursor.app"
```

也可在运行前临时指定：`export CURSOR_INSTALL_DIR="/Applications/Cursor.app"` 后再执行脚本。用户数据目录可选：

```bash
export CURSOR_USER_DATA_DIR="$HOME/Library/Application Support/Cursor"
```

保存后重新运行启动脚本。

也可通过环境变量 `CURSOR_INSTALL_DIR`、`CURSOR_USER_DATA_DIR` 覆盖（见下表），由 `Cursor_Localization_Tool.py` 优先读取：

| 变量 | 含义 |
| --- | --- |
| `CURSOR_INSTALL_DIR` | 安装根目录（含 `Cursor.exe` 或 `Cursor.app`） |
| `CURSOR_USER_DATA_DIR` | 用户数据目录（默认 `%APPDATA%\Cursor` 或 macOS `~/Library/Application Support/Cursor`） |

## 文件说明

| 文件 | 说明 |
| --- | --- |
| `Cursor_Localization_Tool.py` | 主程序（组装并注入汉化脚本；可选 `--install-langpack`） |
| `localization/runtime/` | 注入用 JS 运行时（`bootstrap.js` / `engine.js` / `market.js` / `init.js` / `helpers.js` / `keywords.js`） |
| `localization/Core_Dictionary.json` | 通用界面主词典（设置、Agent、菜单等） |
| `localization/Partial_Fragments.json` | 设置页长句部分匹配（`TiHuan_BuFen_WenBen`） |
| `localization/Dropdown_Fragments.json` | 下拉/快速选择文本片段（`FanYi_XiaLa_WenBen`） |
| `localization/Cursor_Settings_Fragments.json` | Cursor 设置页 MCP/域名片段（`Cursor_SheZhi_*_SuiPian`） |
| `localization/runtime/helpers.js` | 通用 DOM 补丁辅助（`FanYi_Scope_*`、`FanYi_SheZhiGen_*`、`FanYi_Cursor_SheZhi_*`、`FanYi_ZiShu_QuYu`） |
| `localization/runtime/keywords.js` | 合并后的 `QuanJu_BaoHan_GuanJianCi` 关键词表（按补丁标签引用） |
| `localization/Pattern_Dictionary.json` | 动态文本正则替换规则 |
| `localization/Ad_Popup_Dictionary.json` | 左下角推广 / 通知弹窗词典 |
| `localization/Plugin_Marketplace_Dictionary.json` | 插件市场专用词典（注入后首次进入市场页才加载到内存） |
| `VSCode-language-pack-zh-hans.vsix` | 可选：官方简体中文语言包（仅 `--install-langpack` 时使用；非必需） |
| `启动汉化_Win.bat` / `取消汉化_Win.bat` | Windows 快捷脚本 |
| `启动汉化_Mac.sh` / `取消汉化_Mac.sh` | macOS / Linux 快捷脚本 |
| `Cursor_Setting_Lookup.js` | 辅助查找设置页英文原文 |

## 维护翻译

修改对应文件后，运行 `python Cursor_Localization_Tool.py` 并重启 Cursor。

| 维护对象 | 编辑文件 | 格式 |
| --- | --- | --- |
| 通用界面 | `localization/Core_Dictionary.json` | `sections[].entries`: `[英文, 中文]` |
| 动态文案（含数字等） | `localization/Pattern_Dictionary.json` | `patterns`: `{regex, flags, replacement}` |
| 插件市场 | `localization/Plugin_Marketplace_Dictionary.json` | `pluginNames`、`descriptionFragments` 等字段 |
| 广告弹窗 | `localization/Ad_Popup_Dictionary.json` | `entries`: `[英文, 中文]` |

若词典仍放在项目根目录（旧版路径），程序也会自动识别；新路径优先。

校验词典（可选）：

```bash
python localization/tools/validate_dictionary.py
```

**注意**：中文译文中不要使用全角引号 `""`，以免生成的 JS 报错。

### 市场页可选开关（开发者工具控制台）

```javascript
localStorage.setItem('Cursor_Localization_Market_Translate', '0')  // 关闭市场中文描述
localStorage.setItem('Cursor_Localization_Market_Online_Translate', '1')  // 开启在线翻译兜底
```

修改后重启 Cursor。

## 工作原理（简述）

汉化由**注入脚本**完成（不依赖官方语言包）：

| 层级 | 机制 | 覆盖范围 |
| --- | --- | --- |
| 注入脚本（默认） | `Cursor_Localization.js` 运行时替换 | Cursor 专有界面及词典覆盖的文案 |
| 官方语言包（可选） | `--install-langpack` 安装 VSIX | VS Code 标准菜单等（非必需） |

执行步骤：

1. （可选）仅在传入 `--install-langpack` 时安装官方语言包
2. 若本机已有 zh-cn 语言包，桥接 Cursor 私有扩展翻译；否则跳过
3. 备份 `workbench.html`、`product.json`
4. 生成 `Cursor_Localization.js` 并注入到 `workbench.html`
5. 同步更新 `product.json` 中的文件校验值（避免「安装损坏」提示）

取消汉化（`--restore`）会恢复备份文件。

## 常见问题

- **更新 Cursor 后汉化失效了**：重新再运行一次汉化脚本即可。
- **已经执行汉化但是没有生效**：确认已完全重启了 Cursor。
- **标准菜单仍是英文**：本工具默认不安装官方语言包；若需要 VS Code 标准菜单也中文化，可自行安装 Language Pack，或运行 `python Cursor_Localization_Tool.py --install-langpack`（可选）。
- **执行脚本找不到 Cursor**：一般是因为 Cursor 未装在默认目录中。用记事本打开 `启动汉化_Win.bat`（取消汉化时改 `取消汉化_Win.bat`），在 `cd /d "%~dp0"` 后面增加一行，指定 Cursor 安装目录，保存后重新运行启动脚本。

```bat
set CURSOR_INSTALL_DIR=D:\Program Files\cursor
```

Mac / Linux 可在 `启动汉化_Mac.sh` 开头增加 `export CURSOR_INSTALL_DIR="/Applications/Cursor.app"`，详见上文「路径配置」。

- **执行脚本时仍然出错**：直接将汉化脚本拖入 Cursor 对话框，发送以下提示词：

```
我需要安装这个汉化工具，汉化时出现了报错，帮我检查并重新执行脚本，我安装目录是：XXX
```

### 其它情况

| 现象 | 处理 |
| --- | --- |
| 运行脚本报错 / 弹出 Microsoft Store / 汉化无输出 | 多半是 **未安装真正的 Python**，仅有 Windows「应用执行别名」占位程序。运行 `where python`，若路径为 `...\Microsoft\WindowsApps\python.exe` 即属此情况。从 [python.org](https://www.python.org/downloads/) 安装 Python 3（勾选 **Add python.exe to PATH**），或 `winget install Python.Python.3.12`；安装后重开终端，用 `python --version` 验证。可选：在 **设置 → 应用 → 高级应用设置 → 应用执行别名** 关闭 `python.exe` / `python3.exe` 商店快捷方式 |
| 提示 installation appears to be corrupt / 安装已损坏 | 先运行 `修复校验_Win.bat` 或 `python Cursor_Localization_Tool.py --fix-checksum`；若提示权限不足，Windows 请**以管理员身份运行**启动/修复脚本；完成后完全重启 Cursor |
| 部分英文未翻译 | 在对应词典中补充条目后重新注入 |
| 需要恢复原版 | `取消汉化_Win.bat` 或 `--restore` |
