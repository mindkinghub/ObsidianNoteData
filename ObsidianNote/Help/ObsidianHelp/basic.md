
# website
- [Obsidian 中文论坛 - Obsidian 知识管理 笔记](https://forum-zh.obsidian.md/)
- [PKMer_Obsidian](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian/)
- [Home - Obsidian Help](https://help.obsidian.md/)
- [Obsidian文档咖啡豆版 | obsidian文档咖啡豆版](https://obsidian.vip/zh/)
- 

# Tabs
当要打开新笔记时, 如果不想覆盖现有笔记标签页, 按住ctrl打开即可, 而如果想覆盖那就不按。
## shortcuts
### Common actions 

| Action                          | Shortcut                         |
| ------------------------------- | -------------------------------- |
| Copy                            | `Ctrl+C`                         |
| Cut                             | `Ctrl+X`                         |
| Paste                           | `Ctrl+V`                         |
| Paste without formatting        | `Ctrl+Shift+V`                   |
| Undo                            | `Ctrl+Z`                         |
| Redo                            | `Ctrl+Shift+Z` or `Ctrl+Y`       |
| Copy paragraph                  | `Ctrl+C` (with no selected text) |
| Cut paragraph                   | `Ctrl+X` (with no selected text) |
| Open file browser               | `Ctrl+O`                         |
| Search current notes            | `Ctrl+F`                         |
| Add current document properties | `Ctrl+;`                         |
| Toggle view                     | `Ctrl+E`                         |
| Open a new tab                  | `Ctrl+T`                         |
|                                 |                                  |

### Text editing 

| Action                        | Shortcut                               |
| ----------------------------- | -------------------------------------- |
| Insert new line               | `Enter`                                |
| Delete the previous character | `Backspace`                            |
| Delete the next character     | `Delete`                               |
| Delete the previous word      | `Ctrl+Backspace`                       |
| Delete the next word          | `Ctrl+Delete`                          |
| Delete the current line       | `Ctrl+Shift+K` (with no selected text) |

### Text navigation 

|Action|Shortcut|
|---|---|
|Move the cursor one character|`Left/right arrow`|
|Move the cursor to the beginning of the previous word|`Ctrl+Left arrow`|
|Move the cursor to the end of the next word|`Ctrl+Right arrow`|
|Move the cursor to the beginning of the current line|`Home`|
|Move the cursor to the end of the current line|`End`|
|Move the cursor to the previous line|`Up arrow`|
|Move the cursor to the next line|`Down arrow`|
|Move the cursor to the beginning of the note|`Ctrl+Home`|
|Move the cursor to the end of the note|`Ctrl+End`|
|Move the cursor up one page|`Page up`|
|Move the cursor down one page|`Page down`|

### Text selection 

|Action|Shortcut|
|---|---|
|Simplify selection|`Escape`|
|Select all|`Ctrl+A`|
|Extend selection one character|`Shift+Left/right arrow`|
|Extend selection to the beginning of the previous word|`Ctrl+Shift+Left arrow`|
|Extend selection to the end of the next word|`Ctrl+Shift+Right arrow`|
|Extend selection to the beginning of the current line|`Shift+Home`|
|Extend selection to the end of the current line|`Shift+End`|
|Extend selection to the beginning of the note|`Ctrl+Shift+Home`|
|Extend selection to the end of the note|`Ctrl+Shift+End`|
|Extend selection one page up|`Shift+Page up`|
|Extend selection one page down|`Shift+Page down`|

### 切换到不同的标签页 
选中该标签页以点击即可。或者，可以使用键盘快捷键：

| Action        | Shortcut         |
| ------------- | ---------------- |
| **下一个标签页**    | `Ctrl+Tab`       |
| **上一个标签页**    | `Ctrl+Shift+Tab` |
| **最左边的标签页**   | `Ctrl+1`         |
| **第2到第8个标签页** | `Ctrl+2..8`      |
| **最右边的标签页**   | `Ctrl+9`         |
| **最近关闭的标签页**  | `Ctrl+Shift+t`   |
### 自定义

| Action               | Shortcut       |
| -------------------- | -------------- |
| Toggle left sidebar  | `Ctrl+shift+←` |
| Toggle right sidebar | `Ctrl+shift+→` |

## obsidian同步不同库配置

采用软连接
```
mklink /D .obsidian软连接 实际.obsidian路径
mklink /D E:\newstore\.obsidian E:\oldstore\.obsidian
```