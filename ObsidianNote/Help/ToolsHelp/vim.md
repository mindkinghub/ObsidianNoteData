
[如何在 VS Code 中优雅的使用 Vim - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/512935904)

[Learn-Vim(the Smart Way) 中文翻译](https://wsdjeg.net/wiki/learn-vim/)
### 模态编辑

Vim 的设计基于这样一个想法，即花费大量程序员的时间 读取、导航和进行小编辑，而不是编写长流 的文本。因此，Vim 有多种操作模式。

- **Normal**：用于在文件中移动和进行编辑
- **Insert**：用于插入文本
- **Replace**：用于替换文本
- **可视**（普通、行或块）（**Visual**）：用于选择文本块
- **命令行（Command-line）**：用于运行命令

击键在不同的操作模式下具有不同的含义。例如 Insert 模式下的字母只会插入一个文本字符 'x'，但在 Normal 模式下，它会删除光标下的字符，而在 Visual 模式下， 它将删除选择。`x`

在默认配置中，Vim 在左下角显示当前模式。 初始/默认模式为 Normal 模式。您通常会花费大部分 Normal 模式和 Insert 模式之间的时间。

您可以通过按 （Esc 键） 从任何模式切换模式 返回 Normal 模式。从“正常”模式中，进入插入模式，使用“替换”模式 带 、 可视模式 带 、 可视线条模式 带 、 可视块模式 （Ctrl-V，有时也写作）和命令行模式。`<ESC> i R v V <C-v> ^V :`

# 基本

## 插入文本（**Inserting text**）

From Normal mode, press to enter Insert mode. Now, Vim behaves like any other text editor, until you press to return to Normal mode. This, along with the basics explained above, are all you need to start editing files using Vim (though not particularly efficiently, if you’re spending all your time editing from Insert mode).`i<ESC>`

## **缓冲区、选项卡和窗口**

Vim 维护一组打开的文件，称为 “缓冲区”。Vim 会话有一个数字 的选项卡，每个选项卡都有多个窗口（拆分窗格）。每个窗口显示 单个缓冲区。与您熟悉的其他程序（如 Web）不同 浏览器，缓冲区和窗口之间没有 1 对 1 的对应关系; 窗口只是视图。给定的缓冲区可以在_多个_窗口中打开， 甚至在同一个选项卡中。这可能非常方便，例如，查看两个 同时文件的不同部分。

默认情况下，Vim 打开时只有一个选项卡，其中包含一个窗口。

## **命令行**

可以通过在 Normal 模式下键入来进入命令模式。您的光标将跳动 按屏幕底部的命令行。此模式 具有许多功能，包括打开、保存和关闭文件，以及退出Vim。`: :`

- `:q`
    
    退出 （关闭窗口）
    
- `:w`
    
    save （“写入”）
    
- `:wq`
    
    保存并退出
    
- `:e {name of file}`
    
    打开文件进行编辑
    
- `:ls`
    
    显示打开缓冲区
    
- `:help {topic}`
    
    打开帮助
    
    - `:help :w`
        
        打开命令的 help`:w`
        
    - `:help w`
        
        打开移动的帮助`w`
        

## Vim的接口时一种编程语言

Vim 中最重要的思想是 Vim 的接口本身就是一个编程 语言。击键（带有助记词名称）是命令，这些命令_组成_。这样可以实现高效的移动和编辑，尤其是在 命令变成了肌肉记忆。

## **（运动）Movement**

You should spend most of your time in Normal mode, using movement commands to navigate the buffer. Movements in Vim are also called “nouns”, because they refer to chunks of text.

- Basic movement: (left, down, up, right)`hjkl`
- Words: (next word), (beginning of word), (end of word)`w b e`
- Lines: (beginning of line), (first non-blank character), (end of line)`0 ^ $`
- Screen: (top of screen), (middle of screen), (bottom of screen)`H M L`
- Scroll: (up), (down)`Ctrl-u Ctrl-d`
- File: (beginning of file), (end of file)`gg G`
- Line numbers: or (line {number})`:{number}<CR> {number}G`
- Misc: (corresponding item)`%`
- Find: , , , `f{character} t{character} F{character} T{character}`
    - find/to forward/backward {character} on the current line
    - `,` / `;`for navigating matches
- Search: , / for navigating matches`/{regex} n N`

您应该将大部分时间花在正常模式下，使用移动命令 导航缓冲区。Vim 中的动作也被称为 “名词”，因为它们 请参阅 Chunks of Text。

- 基本移动：（左、下、上、右）`hjkl`
    
- 单词：（下一个单词）、（单词开头）、（单词结尾）`wbe`
    
- 行：（行首）、（第一个非空白字符）、（行尾）`0^$`
    
- 屏幕：（屏幕顶部）、（屏幕中间）、（屏幕底部）`HML`
    
- 滚动：（向上）、（向下滚动）`Ctrl-uCtrl-d`
    
- 文件：（文件开头）、（文件结尾）`ggG`
    
- 行号：或 （line {number}）`:{number}<CR>{number}G`
    
- 其他：（对应项目）`%`
    
- 找到：`f{character}t{character}F{character}T{character}`
    
    - 查找/向前/向后 {character} 在当前行
        
    - `,` / `;`
        
        用于导航匹配项
        
- 搜索： ， / 用于导航匹配项`/{regex}nN`
    

## 选择

视觉模式：

- 视觉：`v`
- 可视线：`V`
- 视觉块：`Ctrl-v`

可以使用移动键进行选择。

## **编辑**

您过去使用鼠标完成的所有操作，现在都使用键盘完成 使用编辑命令，这些命令与 Movement 命令组合。这是 Vim 的 interface 开始看起来像一门编程语言。Vim 的编辑命令 也称为 “动词”，因为动词作用于名词。

- `i`
    
    进入插入模式
    
    - 但是对于操作/删除文本，使用 退格键
- `o` / `O`
    
    在下方/上方插入行
    
- `d{motion}`
    
    删除 {motion}
    
    - 例如 is delete word， is delete to end of line， is delete to beginning of line`dw d$ d0`
- `c{motion}`
    
    更改 {motion}
    
    - 例如 是 change word`cw`
    - like followed by `d{motion} i`
- `x`
    
    删除字符（equal do `dl`)
    
- `s`
    
    substitute 字符（equal to `cl`)
    
- 可视模式 + 操作
    
    - 选择文本，以删除或更改它`d c`
- `u` 撤消、重做`<C-r>`
    
- `y` 复制 / “拉扯”（其他一些命令，如 Also Copy）`d`
    
- `p`粘贴
    
- 还有很多东西需要学习：例如 翻转字符的大小写`~`
    

## **计数**

您可以将名词和动词与 count 组合在一起，这将执行给定的操作 好几次。

- `3w`
    
    向前移动 3 个单词
    
- `5j`
    
    向下移动 5 行
    
- `7dw`
    
    删除 7 个单词
    

## **修饰 符**

您可以使用修饰符来更改名词的含义。一些修饰符是 ， 意思是“内部”或“内部”，以及 ，意思是“周围”。`i a`

- `ci(`
    
    更改当前括号对内的内容
    
- `ci[`
    
    更改当前方括号对内的内容
    
- `da'`
    
    删除单引号字符串，包括周围的单引号
    

## 自定义Vim

Vim is customized through a plain-text configuration file in (containing Vimscript commands). There are probably lots of basic settings that you want to turn on.`~/.vimrc`

We are providing a well-documented basic config that you can use as a starting point. We recommend using this because it fixes some of Vim’s quirky default behavior. **Download our config [here](https://missing.csail.mit.edu/2020/files/vimrc) and save it to `~/.vimrc`.**

Vim is heavily customizable, and it’s worth spending time exploring customization options. You can look at people’s dotfiles on GitHub for inspiration, for example, your instructors’ Vim configs ([Anish](https://github.com/anishathalye/dotfiles/blob/master/vimrc), [Jon](https://github.com/jonhoo/configs/blob/master/editor/.config/nvim/init.lua) (uses [neovim](https://neovim.io/)), [Jose](https://github.com/JJGO/dotfiles/blob/master/vim/.vimrc)). There are lots of good blog posts on this topic too. Try not to copy-and-paste people’s full configuration, but read it, understand it, and take what you need.

## 拓展Vim

有大量的插件可以扩展 Vim。与过时的建议相反， 您可能会在互联网上找到，您_不需要_使用 plugin manager for Vim （自 Vim 8.0 起）.相反，您可以使用内置的包管理 系统。只需创建目录 ，然后将 插件中（例如 via ）。`~/.vim/pack/vendor/start/ git clone`

以下是我们最喜欢的一些插件：

- [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim)： 模糊文件查找器
- [ack.vim](https://github.com/mileszs/ack.vim)：代码搜索
- [Nerdtree](https://github.com/scrooloose/nerdtree)：文件资源管理器
- [vim-easymotion](https://github.com/easymotion/vim-easymotion)：魔术动作

我们尽量避免在这里给出一个冗长的插件列表。你 可以查看讲师的 Dot 文件 （[Anish](https://github.com/anishathalye/dotfiles)， [Jon](https://github.com/jonhoo/configs)， [Jose](https://github.com/JJGO/dotfiles)） 查看我们使用的其他插件。 查看 [Vim Awesome](https://vimawesome.com/) 以获取更多很棒的 Vim 插件。 关于这个话题也有很多博客文章：只需搜索“best Vim” 插件”。

## 其他程序中的Vim-mode

Many tools support Vim emulation. The quality varies from good to great; depending on the tool, it may not support the fancier Vim features, but most cover the basics pretty well.

## **Shell**

If you’re a Bash user, use . If you use Zsh, . For Fish, . Additionally, no matter what shell you use, you can . This is the environment variable used to decide which editor is launched when a program wants to start an editor. For example, will use this editor for commit messages.`set -o vibindkey -vfish_vi_key_bindingsexport EDITOR=vimgit`

## **Readline**

Many programs use the [GNU Readline](https://tiswww.case.edu/php/chet/readline/rltop.html) library for their command-line interface. Readline supports (basic) Vim emulation too, which can be enabled by adding the following line to the file:`~/.inputrc`

`set editing-mode vi`

With this setting, for example, the Python REPL will support Vim bindings.

## **Others**

There are even vim keybinding extensions for web [browsers](http://vim.wikia.com/wiki/Vim_key_bindings_for_web_browsers) - some popular ones are [Vimium](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb?hl=en) for Google Chrome and [Tridactyl](https://github.com/tridactyl/tridactyl) for Firefox. You can even get Vim bindings in [Jupyter notebooks](https://github.com/jupyterlab-contrib/jupyterlab-vim). Here is a [long list](https://reversed.top/2016-08-13/big-list-of-vim-like-software) of software with vim-like keybindings.

# 高级Vim

Here are a few examples to show you the power of the editor. We can’t teach you all of these kinds of things, but you’ll learn them as you go. A good heuristic: whenever you’re using your editor and you think “there must be a better way of doing this”, there probably is: look it up online.

## **Search and replace**

`:s` (substitute) command ([documentation](http://vim.wikia.com/wiki/Search_and_replace)).

- `%s/foo/bar/g`
    - replace foo with bar globally in file
- `%s/\\[.*\\](\\(.*\\))/\\1/g`
    - replace named Markdown links with plain URLs

## **Multiple windows**

- `:sp` / `:vsp`
    
    to split windows
    
- Can have multiple views of the same buffer.
    

## **Macros**

- `q{character}{character}`
    
    to start recording a macro in register
    
- `q`
    
    to stop recording
    
- `@{character}`
    
    replays the macro
    
- Macro execution stops on error
    
- `{number}@{character}`
    
    executes a macro {number} times
    
- Macros can be recursive
    
    - first clear the macro with `q{character}q`
    - record the macro, with to invoke the macro recursively (will be a no-op until recording is complete)`@{character}`
- Example: convert xml to json ([file](https://missing.csail.mit.edu/2020/files/example-data.xml))
    
    - Array of objects with keys “name” / “email”
    - Use a Python program?
    - Use sed / regexes
        - `g/people/d`
        - `%s/<person>/{/g`
        - `%s/<name>\\(.*\\)<\\/name>/"name": "\\1",/g`
        - …
    - Vim commands / macros
        - `Gddggdd`
            
            , delete first and last lines
            
        - Macro to format a single element (register `e`)
            
            - Go to line with `<name>`
            - `qe^r"f>s": "<ESC>f<C"<ESC>q`
        - Macro to format a person
            
            - Go to line with `<person>`
            - `qpS{<ESC>j@eA,<ESC>j@ejS},<ESC>q`
        - Macro to format a person and go to the next person
            
            - Go to line with `<person>`
            - `qq@pjq`
        - Execute macro until end of file
            
            - `999@q`
        - Manually remove last and add and delimiters`,[]`
            

# **资源**

- `vimtutor`
    
    是随 Vim 一起安装的教程 - 如果安装了 Vim，您应该能够从 shell 运行
    
- [Vim Adventures](https://vim-adventures.com/) 是一款学习 Vim 的游戏
    
- [Vim 小贴士 Wiki](http://vim.wikia.com/wiki/Vim_Tips_Wiki)
    
- [Vim Advent Calendar](https://vimways.org/2019/) 有各种 Vim 提示
    
- [Vim Golf](http://www.vimgolf.com/) 是 [code golf](https://en.wikipedia.org/wiki/Code_golf)，但编程语言是 Vim 的 UI
    
- [Vi/Vim 堆栈交换](https://vi.stackexchange.com/)
    
- [Vim 截屏视频](http://vimcasts.org/)
    
- [Practical Vim](https://pragprog.com/titles/dnvim2/) （书籍）