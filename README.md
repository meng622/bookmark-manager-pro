# 书签管理器 Pro

> 一个单文件、零依赖的 Chrome 书签整理工具。<br><img width="1343" height="883" alt="屏幕截图 2026-10-15 200904" src="https://github.com/user-attachments/assets/fc08b841-adc4-49b5-bcb8-88eff28d0405" />

> 导入 → 可视化整理 → 导出，再导回 Chrome。

![version](https://img.shields.io/badge/version-1.9.1-blue)
![license](https://img.shields.io/badge/license-MIT-green)
![platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)
![single file](https://img.shields.io/badge/single--file-HTML-orange)

---

## 目录

- [简介](#简介)
- [快速开始](#快速开始)
- [功能特性](#功能特性)
- [批量改名详解](#批量改名详解)
- [快捷键](#快捷键)
- [常见问题](#常见问题)
- [更新日志](#更新日志)
- [许可](#许可)

---

## 简介

Chrome 原生书签管理器功能太少、管理麻烦。这个工具用**一个 `.html` 文件**解决它：

- 不需要安装任何东西
- 不需要联网
- 不需要后端
- 双击用 Chrome 打开就能用
- 数据全程在本地内存，不上传任何服务器

导出的 `bookmarks.html` 完全符合 Netscape Bookmark File Format 标准，可以直接导入回 Chrome。

---

## 快速开始

### 1. 下载
把 `bookmark-manager-pro.html` 下载到本地任意位置。

### 2. 打开
双击文件，用 **Chrome / Edge / Brave** 等 Chromium 内核浏览器打开。

### 3. 导入
点击左上角 **📂 导入书签**，选择 Chrome 导出的 `bookmarks.html`（或者直接把文件拖进窗口）。

> 如何导出 Chrome 书签：Chrome → 书签 → 书签管理器 → ⋮ → 导出书签。

### 4. 整理
- 左侧树状栏：浏览 / 拖动文件夹
- 右侧列表：浏览 / 拖动书签
- 工具栏：搜索、批量改名、查找重复、检测失效

### 5. 导出
点击 **💾 导出书签**，得到新的 `bookmarks_YYYY-MM-DD.html`。

### 6. 导回 Chrome
Chrome → 书签 → 书签管理器 → ⋮ → 导入书签 → 选择刚导出的文件。

---

## 功能特性

### 📂 导入 / 导出
- 完整解析 Netscape Bookmark 格式（Chrome / Edge / Firefox 通用）
- 导出格式兼容 Chrome，可原样导回
- 支持 **导出选中项**（保留原始层级结构，只导出你勾选的部分）
- 再次导入时可选择「**替换现有**」或「**合并到根**」

### 🌳 树状栏
- 单击文件夹 = 高亮 + 切换右侧 + 展开（若收起）
- 单击箭头 ▼/▶ = 只展开 / 收起
- 全部折叠 / 展开按钮
- 拖动调整侧边栏宽度（磁吸 280px，双击恢复默认）
- 拖动文件夹到另一个文件夹 = 移动
- 拖到文件夹上下边缘 = 同级插入

### 📋 列表栏（仿 Windows 资源管理器）
- 列宽可拖，双击列分隔线自动适配内容宽度
- 横向滚动（列宽总和超出容器时出现）
- 点击列头切换升 / 降序排序
- 行高亮只覆盖到列尾，**右侧空白区**按住左键拖动 = 框选
- 支持 Ctrl / Shift 多选
- 多选拖拽：一次拖动整组书签到其他文件夹

### ✏️ 批量改名（核心功能）
仿「拖把更名器」，Tab 式 6 种规则，可叠加、可实时预览、可逐条勾选。

详见[下一节](#批量改名详解)。

### 🔍 查找重复
- 扫描当前文件夹及其子级，找出 URL 相同的书签
- **先报告、后确认**：弹出日志列出所有重复项，你点「确定删除 N 项」才真正删
- 日志可下载为 `.log` 文件

### 🔗 检测失效
- 对当前视图的书签做批量可达性检测
- 并发 8 个请求，标注「可用 / 失效」
- ⚠️ 受浏览器 CORS 限制，只能判断"能否连上"，无法读到 HTTP 状态码，结果仅供参考

### 🔖 新增书签 / 新建文件夹
- 工具栏按钮，或右键菜单
- 支持标题 / URL 双输入

### ⌨️ 内联重命名（F2）
- 选中一项按 F2，直接就地编辑
- 回车提交 / Esc 取消
- 不再弹 prompt 对话框

---

## 批量改名详解

点工具栏 **✏️ 批量改名** 打开。

### 各 Tab 说明

| Tab | 参数 | 示例 |
|---|---|---|
| **裁剪** | 开头词 + 第N个 / 结尾词 + 第N个 / ☐区分大小写 / ☐找不到时删空 | 开头 `Download`、结尾 `IMAX` → 保留中间部分 |
| **替换** | 查找 / 替换为（留空=删）/ 第几个（空=全部）/ ☐区分大小写 | 查找 `Download`、替换留空 → 删除所有 Download |
| **删除** | 方向（头/尾）/ 从第 N 个字符 / 删 M 个字符 | 从头、第 1 个、删 5 个 |
| **序号** | 模板（`#`=序号，`<SELF>`=原标题）/ 起始 / 步长 / 位数 | 模板 `#. <SELF>`、位数 2 → `01. 标题` |
| **前后缀** | 前缀 / 后缀 / 从第 N 个字符插入 | 前缀 `[收藏] ` → `[收藏] 标题` |
| **正则** | 作用范围 / 正则模式 / 替换为（`$1` `$2` 捕获组） | 模式 `^(.+?) \|.*$` 替换 `$1` |

### 规则叠加
多个 Tab 可同时启用，应用时**按 Tab 从左到右顺序**依次作用。

### 实时预览
- 改任意输入框，预览表立即刷新
- 预览表列出所有将处理的项，逐条勾选控制是否应用
- 文件夹行带 📁 前缀，书签行不带

### 独立计数
- 文件夹序号：1, 2, 3…
- 书签序号：1, 2, 3…
- 各自独立，不混算

---

## 快捷键

| 快捷键 | 功能 |
|---|---|
| `F2` | 重命名当前选中项（内联编辑） |
| `Delete` | 删除选中项；无选中时删除当前文件夹 |
| `Ctrl + A` | 全选当前列表 |
| `Esc` | 关闭弹窗 / 关闭右键菜单 |
| `Ctrl + 单击` | 追加选择 |
| `Shift + 单击` | 范围选择 |

---

## 常见问题

**Q：会把我数据传到网上吗？**
A：不会。整个工具完全在浏览器本地运行，不发起除"检测失效"外的任何网络请求。检测失效也只发起一次 HEAD/GET 探测。

**Q：我的书签里有中文 / emoji，能正常处理吗？**
A：可以。解析和导出都用 UTF-8。

**Q：导出的文件 Chrome 能识别吗？**
A：能。导出格式严格遵循 Netscape Bookmark File Format，Chrome / Edge / Firefox 都能导入。

**Q：为什么"检测失效"有些明明能打开的网站也显示失效？**
A：浏览器 CORS 限制导致无法读到真实的 HTTP 状态码，只能判断"能否建立连接"。某些网站会拦截跨域请求。建议只把它当作粗略参考。

**Q：我整理到一半，关了浏览器，数据还在吗？**
A：不在。数据只存在内存里，刷新页面即清空。整理到一半记得先导出备份。

**Q：能在手机上用吗？**
A：理论可以（Chrome 移动版能打开 HTML），但界面是为桌面设计的，触屏体验不佳。

---

## 更新日志

### v1.7.1
- 修复批量改名弹窗 Tab 无法点击、预览区空白（重排初始化顺序、DOM 引用提前获取）

### v1.7.0
- 侧边栏可拖（磁吸 280px，双击恢复默认）
- 树状栏单击展开 + 切换右侧
- 主列表横向滚动
- 批量改名弹窗 16:9 可拉伸、应用到文件夹/书签开关
- 预览表列宽可拖
- 示例文字抽象化（隐私考虑）

### v1.6.0
- 批量改名（Tab 式 6 种规则可叠加、逐条勾选、实时预览）
- 行高亮只到列尾、右侧空白可框选

### v1.5.0
- 预设清理标题（11 条规则可勾选 + 实时预览）

### v1.4.0
- 重写列宽逻辑（固定列 + 末列 flex 填满、splitter 钳制防崩坏）
- 缩短行 padding
- 批量编辑简化为纯正则

### v1.3.1
- splitter 拖拽钳制防崩坏
- Delete 可删树文件夹
- F2 内联重命名
- 去掉时间列

### v1.3.0
- 全部折叠 / 展开
- 列表拖入文件夹
- drop 标记防弹回
- 导出选中
- 查找重复（先报告后确认删除）
- 列表栏排序、框选选择、去重日志

### v1.2.1
- 修复拖拽失效（dragstart 不再重渲 DOM）
- 树同级改为行内三分区

### v1.2.0
- 列宽 splitter、多选拖拽、树同级插入、drop 阈值优化

### v1.1.0
- 列表栏排序、框选选择、去重日志
- 修复搜索全选

### v1.0.0
- 导入 / 导出、搜索、拖拽整理、批量编辑、去重、排序、失效检测

---

## 致谢

本项目的全部代码由 **DeepSeek** 协助完成。

从最初的构想到一路打磨到 v1.7.1，界面设计、交互逻辑、功能取舍、bug 修复、重构建议，几乎每一次迭代都是与 DeepSeek 共同讨论的结果。作为一个不会写代码的使用者，我提出需求、反馈问题、指出不顺手的细节；DeepSeek 负责理解、拆解、给出方案并落地成可运行的代码。

如果没有 DeepSeek，这个工具不会存在。感谢。
<img width="555" height="552" alt="1000197380" src="https://github.com/user-attachments/assets/de3a8dbd-4206-4a7f-b636-43e2d8047fcf" />

---

## 许可

MIT License. 随便用，随便改。

---

<br>

---

# Bookmark Manager Pro

> A single-file, zero-dependency Chrome bookmark organizer.<br>
> Import → visually tidy up → export → import back into Chrome.

![version](https://img.shields.io/badge/version-1.7.1-blue)
![license](https://img.shields.io/badge/license-MIT-green)
![platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)
![single file](https://img.shields.io/badge/single--file-HTML-orange)

---

## Table of Contents

- [Introduction](#introduction)
- [Quick Start](#quick-start)
- [Features](#features)
- [Batch Rename in Detail](#batch-rename-in-detail)
- [Keyboard Shortcuts](#keyboard-shortcuts)
- [FAQ](#faq)
- [Changelog](#changelog)
- [License](#license)

---

## Introduction

Chrome's built-in bookmark manager is too basic and painful to use. This tool solves that with **a single `.html` file**:

- No installation needed
- No internet required
- No backend
- Just double-click to open in Chrome
- Everything stays in local memory — nothing is uploaded to any server

Exported `bookmarks.html` files strictly follow the Netscape Bookmark File Format, so they import cleanly back into Chrome.

---

## Quick Start

### 1. Download
Save `bookmark-manager-pro.html` anywhere on your machine.

### 2. Open
Double-click it and open with **Chrome / Edge / Brave** or any Chromium-based browser.

### 3. Import
Click **📂 导入书签** (Import) at the top left, and pick your Chrome-exported `bookmarks.html`. Or just drag the file into the window.

> To export from Chrome: Bookmarks → Bookmark manager → ⋮ → Export bookmarks.

### 4. Organize
- Left tree: browse / drag folders
- Right list: browse / drag bookmarks
- Toolbar: search, batch rename, find duplicates, check dead links

### 5. Export
Click **💾 导出书签** (Export). You get a fresh `bookmarks_YYYY-MM-DD.html`.

### 6. Import back into Chrome
Chrome → Bookmarks → Bookmark manager → ⋮ → Import bookmarks → pick the exported file.

---

## Features

### 📂 Import / Export
- Full support for the Netscape Bookmark format (Chrome / Edge / Firefox compatible)
- Exported files import cleanly into Chrome
- **Export selection**: preserves the original folder hierarchy, exports only what you checked
- On re-import, choose "**Replace existing**" or "**Merge into root**"

### 🌳 Tree Panel
- Click a folder = highlight + switch right panel + expand if collapsed
- Click the ▼ / ▶ arrow = expand / collapse only
- Collapse-all / Expand-all buttons
- Drag the sidebar edge to resize (snaps to 280px, double-click to reset)
- Drag a folder onto another folder = move inside
- Drag to a folder's top/bottom edge = insert at sibling level

### 📋 List Panel (Windows Explorer-style)
- Drag column borders to resize; double-click a splitter to auto-fit content
- Horizontal scroll when total column width exceeds the viewport
- Click column headers to toggle sort order
- Row highlight stops at the last column — the blank area to the right is **click-drag = marquee select**
- Ctrl / Shift multi-select
- Multi-drag: drag an entire selection at once

### ✏️ Batch Rename (core feature)
Inspired by the classic **拖把更名器 (TuoBa Renamer)**. Tab-based, 6 rule types, composable, live preview, per-row checkboxes.

See [the next section](#batch-rename-in-detail).

### 🔍 Find Duplicates
- Scans the current folder and its children for bookmarks with identical URLs
- **Report first, then confirm**: shows a full log of duplicates; nothing is deleted until you click "Confirm delete N items"
- Download the log as `.log`

### 🔗 Check Dead Links
- Batch-checks bookmark reachability for the current view
- 8 concurrent requests, marks "OK / Dead"
- ⚠️ Due to browser CORS limits, it can only tell whether a connection succeeds — HTTP status codes are not visible. Results are indicative only.

### 🔖 New Bookmark / New Folder
- Toolbar buttons or right-click menu
- Title + URL input

### ⌨️ Inline Rename (F2)
- Select an item and press F2 to edit in place
- Enter to commit / Esc to cancel
- No more prompt dialogs

---

## Batch Rename in Detail

Click **✏️ 批量改名** on the toolbar to open.

### Tabs

| Tab | Parameters | Example |
|---|---|---|
| **Trim** | Start word + nth / End word + nth / ☐Case-sensitive / ☐Empty if not found | start `Download`, end `IMAX` → keep the middle |
| **Replace** | Find / Replace with (empty = delete) / nth (empty = all) / ☐Case-sensitive | find `Download`, replace empty → delete all "Download" |
| **Delete** | Direction (head/tail) / from Nth char / delete M chars | head, from 1, delete 5 |
| **Number** | Template (`#`=number, `<SELF>`=title) / Start / Step / Pad | template `#. <SELF>`, pad 2 → `01. Title` |
| **Affix** | Prefix / Suffix / Insert at Nth char | prefix `[fav] ` → `[fav] Title` |
| **Regex** | Target / Pattern / Replacement (`$1`, `$2`) | `^(.+?) \|.*$` → `$1` |

### Composability
Multiple tabs can be enabled at once. When you click **Apply**, rules run **left-to-right across the tab bar**.

### Live Preview
- Editing any input refreshes the preview table instantly
- Table lists every item that would be renamed; per-row checkboxes control what actually applies
- Folder rows get a 📁 prefix; bookmark rows don't

### Independent Numbering
- Folders: 1, 2, 3…
- Bookmarks: 1, 2, 3…
- Counted separately

---

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `F2` | Rename selected item (inline) |
| `Delete` | Delete selection; or delete current folder if nothing selected |
| `Ctrl + A` | Select all in current list |
| `Esc` | Close modal / hide context menu |
| `Ctrl + click` | Add to selection |
| `Shift + click` | Range select |

---

## FAQ

**Q: Does it send my data anywhere?**
A: No. The tool runs entirely in your browser. The only network requests it makes are for the "check dead links" feature.

**Q: Does it handle Chinese / emoji in titles?**
A: Yes. Parsing and export both use UTF-8.

**Q: Will Chrome accept the exported file?**
A: Yes. The export format strictly follows Netscape Bookmark File Format, compatible with Chrome / Edge / Firefox.

**Q: Why does "check dead links" mark sites that clearly work as dead?**
A: Browser CORS restrictions prevent reading real HTTP status codes — only connection success is detected. Some sites block cross-origin probes. Treat the results as rough guidance.

**Q: If I close the browser mid-session, is my work saved?**
A: No. Data lives only in memory. Refresh wipes it. Export early and often.

**Q: Does it work on mobile?**
A: Theoretically, yes (mobile Chrome can open the file), but the UI is designed for desktop and touch interaction is poor.

---

## Changelog

### v1.7.1
- Fixed batch rename modal tabs unclickable and empty preview (reordered init, hoisted DOM refs)

### v1.7.0
- Sidebar resizable (snaps to 280px, double-click to reset)
- Tree: click to expand + switch right panel
- Main list horizontal scroll
- Batch rename modal 16:9, resizable; apply-to-folders / apply-to-bookmarks toggles
- Preview table columns resizable
- Abstracted example text (privacy)

### v1.6.0
- Batch rename (tabbed, 6 composable rule types, per-row checkboxes, live preview)
- Row highlight stops at last column; blank area supports marquee select

### v1.5.0
- Preset title cleanup (11 rules to toggle + live preview)

### v1.4.0
- Rewrote column-width logic (fixed columns + flex last column; clamped splitters)
- Shorter row padding
- Batch edit reduced to pure regex

### v1.3.1
- Clamped splitter drag to prevent layout breakage
- Delete can remove tree folders
- F2 inline rename
- Removed date column

### v1.3.0
- Collapse-all / Expand-all
- Drag list items into folders
- Drop-marker to prevent drag-bounce
- Export selection
- Find duplicates (report first, then confirm)
- List sorting, marquee select, dedup log

### v1.2.1
- Fixed drag not working (no re-render during dragstart)
- Tree sibling drop now uses 3-zone inline logic

### v1.2.0
- Column splitters, multi-drag, tree sibling insert, drop-threshold tweaks

### v1.1.0
- Column-header sorting, marquee select, dedup log
- Fixed select-all in search

### v1.0.0
- Import/export, search, drag-to-organize, batch edit, dedup, sort, dead-link check

---

## Acknowledgements

The entire codebase of this project was built with the assistance of **DeepSeek**.

From the initial idea all the way to v1.7.1 — UI design, interaction logic, feature decisions, bug fixes, and refactoring suggestions — nearly every iteration was shaped through conversations with DeepSeek. As a user who doesn't write code, I described what I wanted, reported what broke, and pointed out what felt awkward. DeepSeek interpreted, broke things down, proposed solutions, and turned them into working code.

Without DeepSeek, this tool would not exist. Thank you.
<img width="555" height="552" alt="1000197380" src="https://github.com/user-attachments/assets/a72601af-4692-4aa7-946f-db7e750bd646" />

---

## License

MIT License. Do whatever you want with it.
