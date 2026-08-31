# Cursor 汉化

参考：[VibePM Cursor 汉化](https://www.vibepm.net/cursor/)

## 推荐

1. 先安装 **Chinese (Simplified) (简体中文) Language Pack `1.105.0`** 
2. 完全退出 Cursor（含托盘）
3. 运行 `启动汉化_Win.bat` 

## 实现

相对安装根目录（默认 `D:\cursor`）

- **改** `resources\app\out\vs\code\electron-sandbox\workbench\workbench.html` — 注入脚本标签
- **加** 同目录 `Cursor_Localization.js` — 运行时汉化
- **改** `resources\app\product.json` — 更新 checksums（避免「安装已损坏」）
- **首次备份** 对应 `.bak` 文件

## 脚本

| 脚本 | 作用 |
|------|------|
| `启动汉化_Win.bat` | 注入 / 更新汉化 |
| `取消汉化_Win.bat` | 还原备份，去掉注入 |
| `修复校验_Win.bat` | 只修 `product.json` 校验（提示「安装已损坏」时用） |

## 注意

- 不生效或升级后失效 → 完全退出后重跑 `启动汉化_Win.bat`
- 安装目录不是 `D:\cursor` → 设置环境变量 `CURSOR_INSTALL_DIR`
- 需要 Python 3.8+

## 许可

[MIT License](LICENSE)
