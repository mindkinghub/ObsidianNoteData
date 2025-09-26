---
date: 2025-09-25
tags:
  - help
---

# 介绍
 Dataview 插件为 Obsidian 提供了更高级的数据查询和可视化功能，可帮助用户更好地组织和分析笔记内容。
 用途主要有三个方面。
- 首先，Dataview 插件可以用于创建复杂的数据查询和筛选。用户可以使用类似于 SQL 的语法，通过在笔记中标记和注释特定的数据字段或属性，然后利用 Dataview 插件进行搜索、过滤和排序。这样能够很方便地查找特定信息、生成特定条件下的数据集合，或者执行一些统计和计算操作。这对于处理大量信息的复杂项目、管理项目清单或进行定量分析非常有用。
- 其次，Dataview 插件还可以用于创建和展示笔记内容的动态视图。用户可以基于数据的不同维度和属性，使用 Dataview 插件生成列表，表格，日历和任务列表，以便以更直观的方式展示笔记中的内容和关系，并加强对整体知识结构的把握。
- 最后，Dataview 插件还支持自定义模板和样式，使用户能够根据自己的需要进行个性化的数据展示和排版。用户可以使用 Markdown 语法结合强大的 Dataview 指令，根据自己的喜好和需求，定义不同的模板和样式。这使得用户能够更好地控制和定制输出内容的格式和布局，使其更符合个人审美和展示要求。

参考网站：
- [Dataview](https://blacksmithgu.github.io/obsidian-dataview/)
- [PKMer_Obsidian 插件：Dataview](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/dataview/dataview/)

# 基本语法
## 查询
### Metadata元数据
**元数据（Metadata）** 又称中介数据、中继数据，为描述数据的数据（data about data），主要是关于数据的组织、数据域及其关系的信息，简言之，元数据就是关于数据的数据。
一个元属性包含两个部分：Key 和 Value（其实就是一个键值对）
对于 Dataview 来说，它无法直接查询文档中的内容，只能查询有索引的内容。文件中只有元数据和隐式字段是具有索引的：
- 文件中的元数据：在文件中，有两种东西可以有元数据，分别是文件本身和文件中的列表。其中文件本身的元数据分别来自文件的文档属性和文中的内联字段，文件中列表的元数据一般放在该列表的末尾（列表包括无序列表、有序列表和任务）。这些元数据与这篇文件绑定，可以被 Dataview 检索作为分类的依据或者作为展示的内容。
- 文件的隐式字段：文件中还有一些已经自动有索引的内容，比如文件的名字，文件的创建时间、修改时间等，称之为文件的隐式字段。他们也是能够被 Dataview 检索到的。

#### 向文件添加元数据
有两种方式为一个 markdown 文件添加元数据
- 添加到 `Properties` 文档属性部分；
- 添加到 `Inline Fields` 行内字段中；
##### 文档属性
文档属性可帮助你组织有关笔记的信息。将属性添加到笔记中可以帮助你跟踪结构化数据，如文本、链接、日期和数字。
添加文档属性方法：
- 快捷键法：`ctrl+;`
- 命令面板法：ctrl + p，搜索添加文档属性 (add file property)；
- 鼠标右键文件标题：选择增加文档属性 (add file property)；
- 标签页标题栏的竖着的三个点：选择增加文档属性 (add file property)；
- 手动输入 `---` ；

**YAML 语法规则**
- 大小写敏感，可以使用中文；
- 冒号后要跟一个空格；
- 使用缩进来代表层级关系；
- 缩进时只能用空格，不能用 `Tab`；
- 缩进的空格数不重要，但是同一级元素必须左对齐；
- 用井号标识注释，从 `#` 到当前行的末尾是注释；
**注意**：
- 如果YAML 格式正确，则阅读模式下会自动隐藏，否则会标红报错；
- 占位符里的冒号后有空格，如`{{time: HH:mm}}`，留意占位符里的 `time`,或者 `date` 冒号后面也是要添加一个空格的；
- 可以使用所有字符作为键 or 值（包括 `emoji` 在内），但若放在键的位置，则仍需要放入中括号中，除了 `task` 的情况；
- `dv` 检索时，原关键字的值的格式必须正确，否则` dv` 会报错，但这种情况下不是代码写错了，而是代码检索的对象有问题；

##### Inline Fields 行内字段
内联字段插入元数据的语法就是 `Key::Value`
插入内联字段分为两类
- **行内字段单独成行**
`Key::Value`
前面不能有其他内容，否则会被当成 Key 中的内容。`::` 之后的所有内容都是 Value 的值
- **行内字段插入某一行**
```md
读完这本的感受：[feel:: ...]；
读完这本的感受：(feelisthewordafter:: ...)；
```
用方括号或者圆括号把 `Key::Value `括起来，区别在于用圆括号括起来后，在阅读模式下不会显示 Key。

### 完整查询语法
无论 `dataview` 也好，`dataviewjs` 也罢，都必须遵循一个逻辑流程：
- 查询
- 呈现（通过渲染）
- 条件（过滤器Filter）
- 排序（整理）

```md title:"dataview"
list
from "Help/ObsidianHelp/插件" and #help
sort file.ctime desc
```
```dataview
list
from "Help/ObsidianHelp/插件" and #help
sort file.ctime desc
```
- `list`，表示呈现的样式，有4种，`table`、`list`、`task`、`CALENDAR`。按需选择，大小写无所谓
- `from`，字面意思，就是从哪里查询。比如从指定的文件夹，标签、文件等
- `sort`，字面意思排序，按`file.ctime`这个字段，desc排序方式。
- 其他规范：英文单词之间用**一个空格间隔**，每行一个语句，**标点符号一定要用英文符号**

- from：指定查询的地方：
    - 如果是文件夹，格式固定为 `"文件夹"`，英文双引号里面是文件夹名字，双引号一定要有。
        - 注意：文件夹的**路径必须要写完整**，比如 `mywork/question`，表示是`mywork`文件夹下面的子文件夹`question`，有3层就把3层写全。
        - 注意：这里的文件夹是指的Obsidian内部的路径，**不要**写操作系统的路径
    - 如果是标签，格式固定为`#标签名`，英文的`#`号加上标签名字，英文的`#`号一定要有。
    - 如果同时查询两个条件，可以用`and`连接起来，表示同时具备。
    - 如果从两个条件中任一匹配一个，可以用`or`连接起来，表示或者，选择其中一个。
- sort：排序
    - 可替换`file.ctime`文件创建时间这里，`file.mtime`文件修改时间，`file.name`文件名。
    - 排序方式两种，`DESC`降序排列和`ASC`升序排列。
### 查询结果显示样式
查询结果可以有四种样式：
1. **TABLE**：表格样式，传统的视图类型；每个数据点有一行，有几列的字段数据。
2. **LIST**：列表样式，匹配查询的页面的列表。可以为每个页面输出一个单一的关联值。
3. **TASK**：任务列表，页面符合给定查询的任务列表。
4. **CALENDAR**：一个日历视图，通过其相关日期上的一个点来显示每一个命中率。
### 可供查询的字段
主要是两种：
- 自带`隐式字段`，由 `dataview` 自动添加给`md`文件，
- 添加的自定义字段，可在页面顶部和正文自行添加。然后去调用。比如`书名:: obsidian文档`，通过查询`书名`，可以得到`obsidian文档`这个值

隐式字段是`dataview`自动为`md`文件插入的字段，是为了增加更多的查询项目。掌握了隐式字段，也能够熟练的使用`dataview`的查询条件了，主要是两种：
- 一是页面文件的隐式字段
- 二是`task`和`list`的隐式字段
可以通过查询隐式字段，查询`md`文件的更多属性，比如创建时间、文件标题、修改时间等等
#### file.文件隐式字段
- `file.name`: 文件标题（一个字符串）
- `file.folder`: 这个文件所属的文件夹的路径
- `file.path`: 完整的文件路径（一个字符串）
- `file.ext`: 文件类型的扩展名；一般为`.md`（字符串）
- `file.link`: 通往该文件的链接（一个链接）
- `file.size`: 文件的大小（以字节为单位）（一个数字）
- `file.ctime`: 该文件的创建日期（一个日期+时间）
- `file.cday`: 文件创建的日期（只是一个日期）
- `file.mtime`: 文件最后被修改的日期（一个日期+时间）。
- `file.mday`: 文件最后被修改的日期（只是一个日期）。
- `file.tags`: 笔记中所有独特标签的一个数组. 小标签按每个级别进行细分, `#Tag/1/A` 将被存储在数组中，作为 `[#Tag, #Tag/1, #Tag/1/A]`
- `file.etags`: 注释中所有显式标签的数组; unlike `file.tags`, 不包括子标签
- `file.inlinks`: 该文件的所有传入链接的数组
- `file.outlinks`: 该文件中所有外链的数组
- `file.aliases`: 笔记中所有别名的一个数组
- `file.tasks`: 一个包含所有任务的数组 (I.e., `- [ ] blah blah blah`) 在这个文件中。
- `file.lists`: 文件中所有列表元素的数组（包括任务）；这些元素是有效的任务，可以在任务视图中呈现。
- `file.frontmatter`: 包含所有frontmatter的原始值；主要用于检查frontmatter的原始值或动态地列出前题的 keys 键值(字段)。

如果文件的标题内有一个日期（形式为 `yyyy-mm-dd` 或 `yyyymmdd`），或有一个Date字段/`inline`字段，它也有以下属性。
- `file.day`: 与文件标题相关的明确日期. 如果你使用`obsidian`核心插件 `"Starred Files"`，以下元数据也是可用的。
- `file.starred`: 如果这个文件已经被 `"stars "` obsidian插件加了星号。

#### task.待办隐式字段
- `status`: 该任务的完成状态，由`[]`括号内的字符决定。一般来说，空格`" "`表示未完成的任务，X`"X"`表示完成的任务，但允许支持其他任务状态的插件。
- `checked`: 该任务是否以任何方式被检查过（即它的状态不是未完成/空的）。
- `completed`: 这个具体的任务是否已经完成；这不考虑任何子任务的完成/未完成情况。如果一项任务被标记为 "X"，则明确视为 "完成"。
- `fullyCompleted`: Whether or not this task and **all** of its subtasks are completed
- `text`: 这项任务的文本
- `line`: 该任务显示的行
- `lineCount`: 这项任务所占的 `markdown `行数
- `path`: 该任务所在文件的完整路径
- `section`: 该任务包含的章节链接
- `tags`: 文本任务内的任何标签。
- `outlinks`: 本任务中定义的任何链接
- `link`: 通往该任务附近最近的可链接区块的链接；对于建立通往该任务的链接很有用。
- `children`: 该任务的任何子任务或子清单
- `task`: 如果为真，这是一个任务；否则，它是一个普通的列表元素
- `completion`: 一项任务完成的日期; set by `completion...` 
- `due`: 任务到期的日期，如果它有一个。. set by `due...` 
- `created`: 一个任务的创建日期; set by `created...`
- `start`: 一个任务可以开始的日期; set by `start...` 
- `scheduled`: The date a task is scheduled to work on; set by `scheduled...`
- `annotated`: 如果任务有任何自定义注解，则为真，否则为假.
- `parent`: 这个任务上面的任务的行号，如果存在的话；如果这是一个根级任务，则为空。.
- `blockId`: 该任务/列表元素的块ID, if one has been defined with the `^blockId` syntax; otherwise null.

###  自定义Frontmatter前言
`Frontmatte`r 是一个常见的 `Markdown` 扩展，它允许将 `YAML` 元数据添加到页面顶部。 **注意：必须在页面的最顶部**
`YAML` 符合规范的一种数据格式，都是成对存在，`key: value` 键和值。通过查询键，可以得到对应的值。
典型的`frontmatter YAML`定义：
```yaml
---
    alias: "document"
    last-reviewed: 2021-08-17
    thoughts:
      rating: 8
      reviewable: false
---
```

- `alias`是一个文本，因为它被包装在` “”` 中
- `last-reviewed`是一个日期，因为它遵循 ISO 日期格式
- `thoughts`是一个对象字段，因为它使用 `YAML` 前置对象语法
字段也可以是中文，也可以直接用中文作为值
标点符号必须是英文
- 特别注意，在查询和定义是时候，`:`、`""`、`.` 这些符号必须是英文符号
- 单词之间用空格间隔
### 自定义inline 内联字段
就是可以在正文中插入的字段，也可以被 `dataview` 所查询。但是一般情况下，应该尽量避免使用，因为太零散了不容易管理。
定义内联字段：
```md
key:: value
book:: obsidian
```

### dataview常用命令
#### from
1. **标签**：从一个或多个标签范围内查询，语法是 `#标签名`。
2. **文件夹**：从文件夹（及其所有子文件夹）中选择，语法是`"文件夹名"`。
3. **单个文件**：查询指定的单个文件，语法是：`文件路径/文件名字.md`
4. **链接**：可以查询链接，指向文件的链接，也可以选择来自文件的所有链接
    1. 要获取链接到 `[[笔记名]]` 的所有页面，请使用 `FROM [[笔记名]]`
    2. 要获取从 `[[笔记名]]` 链接的所有页面（即该文件中的所有链接），请使用 `FROM outgoing([[笔记名]])`
#####  在from里过滤filters
可以使用几个条件进行筛选（注意英文符号，前后有一个空格）：
- `and` ：和，同时满足
- `or` ：或者，任选其一
- `-`： 减去，排除掉这个条件
```sql
# 查询 文件夹名1 下同时有 #标签名 的数据
from "文件夹名1" and #标签名

# 查询 文件夹名1 和 文件夹名2 ，同时查两个文件夹
from "文件夹名1" and "文件夹2"

# 查询 #标签名1 或者 #标签名1 ，任选其中一个
from #标签名1 or #标签名2

# 查询 文件:文件名1 或者 文件:文件名2 中的内容，任选其一
from [[文件名1]] or [[文件名2]]

# 查询 文件夹:文件夹名1，并且排除其中带有标签 #标签名1 的文件
from "文件夹名1" and -#标签名1

# 查询 文件夹:文件夹名1，并且排除其中的文件:文件名1
from "文件夹名1" and -[[文件名1]]

# 查询 文件夹，并排除另一个文件夹
FROM "tasks" and -"tasks/Archived"
FROM "tasks" and !"tasks/Archived"
```

#### where
作用就是过滤掉符合要求条件的内容。
##### contains()包含函数
- 对于对象，检查该对象是否有具有给定名称的键
- 对于列表，检查是否有任何数组元素等于给定值
- 对于字符串，检查给定值是否为子字符串
```sql
contains(file.name, "咖啡豆") = true
# 检查对象 file.name ，包含“咖啡豆”，就返回结果为 真
```
实战：
```sql
where contains(file.name, "咖啡豆") = true
# 检查对象 file.name ，包含“咖啡豆”，就返回结果为 真

# 1. file.name 是dataview的隐式字段，前面讲到过，还有很多可以拿来查询
# 2. "咖啡豆"  是查询的文字，必须用英文的双引""号包裹

# 完整查询语句table
table 
	file.mtime as "修改时间"
from ""
where contains(file.name, "咖啡豆") = true
sort file.name desc

# 用表格显示结果，表头是文件修改时间。
# 从所有的文件里查询
# 过滤条件是：文件名中包含咖啡豆的结果
# 按照文件名排序
# 1. file.name 是dataview的隐式字段，前面讲到过，还有很多可以拿来查询
# 2. "咖啡豆"  是查询的文字，必须用英文的双引""号包裹

# 完整查询语句list
list
from ""
where contains(file.name, "咖啡豆") = true
sort file.name desc

# 用列表显示结果
# 从所有的文件里查询
# 过滤条件是：文件名中包含咖啡豆的结果
# 按照文件名排序
# 1. file.name 是dataview的隐式字段，前面讲到过，还有很多可以拿来查询
# 2. "咖啡豆"  是查询的文字，必须用英文的双引""号包裹
```
`file.name`、`file.tags`、`file.path`、`file.folder` 等等众多的隐式字段都可以使用。但是注意有些字段是时间格式，不能错误。
##### date(any) 日期函数
从提供的字符串、日期或链接对象中分析日期（如果可能），否则返回null：
```sql
date("2020-04-18") 
# 日期对象代表 2020年4月18日

date([[2021-04-16]])
# 给定页面的日期对象，参考file.day
```

##### dur(any) 从字符串解析时间
从提供的字符串或持续时间分析**持续时间**，失败时返回null：
```sql
dur(8 minutes)
# 8分钟

dur("8 minutes, 4 seconds")
# 8分4秒

dur(dur(8 minutes))
# dur(8 minutes) = <8 minutes>

```
实战：
```sql
list
from ""
WHERE file.mtime >= date(today) - dur(7 day)
sort file.mtime desc

# table查询
table without id
	file.link as "文件名",
	file.folder as "文件夹",
	file.mtime as "修改时间"
from "" and -#obsidian
WHERE file.mtime >= date(today) - dur(7 day)
sort file.mtime desc
limit 20
```
也可以查询自定义字段，也就是 `frontmatter` 和 `inline 内联字段`

#### sort 排序
按一个或多个字段对所有结果进行排序。
`SORT date [ASCENDING/DESCENDING/ASC/DESC]`
```sql
sort file.mtime desc
```
- ASC：升序
- DESC：降序
#### FLATTEN 数据扁平化
就是将一组数据变成多行数据，每个数据一行，展开方便阅读。
基本语法：
```md
TABLE 作者 
FROM #书籍 
FLATTEN 作者
```
#### GROUP BY 数据分组
在 list 视图下面，
- 将结果按照不同的日期分组显示
- 将结果按照不同的文件夹展示
- 将结果按照不同的文件路径展示
- 其他的参数
    - `file.name` 文件名称
    - `file.cday` 文件创建日期
    - `file.mday` 文件修改日期
```sql
list rows.file.link
from "Longform"
where file.name != "Index"
GROUP BY file.folder

# 按照 list 展示，并加上参数 row.file.link 文件链接
# 从 Longform 文件夹查询
# where 限制条件：不允许文件名中包含 Index 的文件
# 分组展示，按照 file.folder 文件夹
```
#### limit 限制显示数量
可以控制显示数据的数量，比如只显示10个。
```sql
limit 10
```
