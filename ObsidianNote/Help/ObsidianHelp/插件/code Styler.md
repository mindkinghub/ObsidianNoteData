---
date: 2025-09-26
tags:
  - help
---

# 介绍
在阅读视图和编辑视图中对代码块和内联代码进行样式设置。

# 主题
可以在主题中设置的不同组件颜色包括：
- 代码块背景颜色【Codeblock background colour】
- 代码块文本颜色【Codeblock text colour】
- 行号栏背景颜色【Line number gutter background colour】
- 行号栏文本颜色【Line number text colour】
- 代码块行号当前行指示器【Codeblock line number current line indicator】
- 代码块标题栏背景颜色【Codeblock header background colour】
- 代码块标题栏标题文本颜色【Codeblock header title text colour】
- 代码块标题栏分隔线颜色【Codeblock header separator colour】
- 代码块标题栏语言标签背景颜色【Codeblock header language tag background colour 】
- 代码块标题栏语言标签文本颜色【Codeblock header language tag text colour】
- 编辑器活动行高亮颜色【Editor active line highlight colour】
- 代码块活动行高亮颜色【Codeblock active line highlight colour】
- 默认高亮颜色【Default highlight colour】
- 其他高亮颜色【Alternative highlight colours】
- 按钮颜色【Button colour】
- 按钮活动颜色【Button active colour】
# 代码块参数
代码块参数被添加到语言后的代码块的第一行。它们可以以任何顺序添加。如果没有设置语言，则在代码块分隔符 ` ``` ` 后应留出一个空格，以表示第一个参数不是代码块的语言。
示例：

- ` ```cpp fold title:example_title `
- ` ```cpp title:example_title fold `（与上一行效果相同）
- ` ``` fold title:example_title `（如果没有设置语言）
## 行号
行号可以在主题的设置中启用/禁用。除此之外，是否应用行号还可以在代码块本身中使用` ln `参数进行额外指定。
设置 `ln:true `将始终显示行号，`ln:false` 将永远不显示行号，而 `ln:NUMBER`（例如 `ln:27`）将始终显示从指定数字开始的行号（因此偏移量为该数字减一）。
## 标题
要为代码块显示一个标题，在代码块的第一行指定 `title:`，然后跟上标题。如果标题包含空格，可以使用 `""` 或 `''` 将其指定在其中，例如：`title:"long filename.cpp"`。
示例：
- ` ```cpp title:test.cpp`
- ` ```cpp title:“long filename.cpp”`
## 折叠
要在打开文档时指定初始折叠状态，请使用 `fold` 参数。如果在代码块中设置了` fold`，那么在打开文档时，代码块将自动折叠，只显示标题。您可以通过点击标题来展开代码块。
点击任何标题都会切换该代码块的折叠状态。
当没有设置` title` 参数时，折叠的代码块将具有默认的折叠占位符标题。可以在设置中更改此设置，或者可以通过在折叠参数后设置字符串来更改特定参数，例如 `fold:Folded` 或 `fold:"Collapsed Codeblock"`。
## 高亮显示
要高亮显示行，请在代码块的第一行中指定 `hl:`，后面跟着行号、纯文本或正则表达式。
您可以使用逗号（不带空格）分隔的以下任何高亮类型，例如：`hl:1,3-4,foo,'bar baz',"bar and baz",/#\w{6}/。`
单个数字：`hl:1 `将高亮显示第一行
数字范围：`hl:1-3 `将高亮显示从第 1 行到第 3 行
纯文本：`hl:foo` 将高亮显示包含单词 foo 的行
用引号括起来的纯文本：`hl:'bar baz' `或 `hl:"bar baz" `将高亮显示包含单词 bar baz 的行
正则表达式：`hl:/#\w{6}/` 将高亮显示与该正则表达式匹配的行（通过` regex.test(line)` 进行测试）- 对于此示例，任何包含十六进制颜色的行都会被高亮显示
这些组合将高亮显示所有相关行。
## 外貌
代码块可以在设置中更改代码块的曲率，使其显示更圆或更直。
如果在设置中启用，代码块的左边框可以根据语言进行着色（颜色与语言图标相匹配）。还可以更改此边框的宽度。
在以下情况下会显示头部：
- 您指定了`title:`
- 您指定了 `fold `如果您指定了` fold` 但没有指定` title:` 或 `fold:`，则默认文本将显示在头部（默认为“折叠代码”）
- 您通过` ```language` 定义了代码块语言，并在主题设置中将 `Display Header Language Tags` 设置为 `Always` 或将 `Display Header Language Icons` 设置为 `Always`

如果显示了头部，则折叠也会起作用。如果将 `Display Header Language Tags`设置为 `Always`，则头部将始终显示代码块语言，如果将其设置为 `If Header Shown`，则仅在显示头部时显示（即设置了 title 参数）。
您可以在设置页面中启用选项以显示头部中的图标。当此选项设置为` If Header Shown `时，如果代码块中指定的语言具有图标并且显示了代码块头部（即设置了 `title` 参数），则会显示图标。当此选项设置为 `Always` 时，如果代码块中指定的语言具有图标，则始终显示带有图标的头部。图标还可以在设置中设置为灰度或调整大小。目前有大约 170 个不同语言的图标可用。

语言标签文本和标题文本也可以设置为粗体和/或斜体，以及特定字体。此外，头部文本的字体大小可以更改。
