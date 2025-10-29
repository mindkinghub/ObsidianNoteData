---
date: 2025-09-26
tags:
  - help
---

# 介绍
Templater是一种模板语言，允许您在笔记中插入变量和函数结果。它还允许您执行JavaScript代码来操作这些变量和函数。

# templater基础语法
调用templater模板的流程：
- 设置templater模板
	- 插入模板
	- 从模板新建
**通常的调用语法格式**
- 注意一定是固定的格式，`<%`和 `%>` 开头和结尾的。
- 注意templater的调用，使用 `tp.` 开头。
```js
	<% tp.tp.date.now("YYYY-MM-DD") %>
```

## 常用语法
### 日期相关
有四个相关函数：
- now
- tomorrow
- weekday
- yesterday
#### 日期格式化
```js
YYYY-MM-DD
# 第二种形式
YYYYMMDD
```
#### 常用日期
```js
	<% tp.date.now() %> 

# 获取当天日期并格式化
	<% tp.date.now("YYYY-MM-DD") %>

# 昨天日期
	<% tp.date.yesterday("YYYY-MM-DD") %>
	<% tp.date.now("YYYY-MM-DD", -1) %>

# 明天日期
	<% tp.date.tomorrow("YYYY-MM-DD") %>
	<% tp.date.now("YYYY-MM-DD", +1) %>

# 本周星期一
	<% tp.date.weekday("YYYY-MM-DD", 0) %>

# 昨天+今天+明天
[[<% tp.date.now("YYYY-MM-DD", -1) %>]] | [[<% tp.date.now() %>]] | [[<% tp.date.now("YYYY-MM-DD", +1) %>]]

# 上周+今天+下周
[[<% tp.date.now("YYYY-MM-DD", -7) %>]] | [[<% tp.date.now() %>]] | [[<% tp.date.now("YYYY-MM-DD", +7) %>]]
```
#### 获取间隔日期
```js
# 获取7天前的日期
	<% tp.date.now("YYYY-MM-DD", -7) %>
# 获取7天后的日期
	<% tp.date.now("YYYY-MM-DD", +7) %>
# 获取下个月的日期
	<% tp.date.now("YYYY-MM-DD", "P-1M") %>
# 获取明年的日期
	<% tp.date.now("YYYY-MM-DD", "P1Y") %>
```

### 文件相关
#### 获取笔记常用信息
```js
# 笔记的标题title
	<% tp.file.title %>

# 笔记的标签tags
	<% tp.file.tags %>

# 笔记的绝对路径
	<% tp.file.path() %>

# 笔记的相对路径（相对于Obsidian库根目录）
	<% tp.file.path(true) %>

# 笔记正文
	<% tp.file.content %>

# 笔记创建时间
	<% tp.file.creation_date() %>

# 笔记最后修改时间
	<% tp.file.last_modified_date() %>

# 移动文件
	<% await tp.file.move("/A/B/" + tp.file.title) %>
	<% await tp.file.move("/A/B/NewTitle") %>

# 重命名文件
	<% await tp.file.rename("MyNewName") %>
```

用来获取顶部属性区域的函数，可以直接获取对应属性的值，也就是以前的YAML区域。
假设顶部属性定义：
```
---
aliases: myfile
note type: seedling
---
```

```js
	<% tp.frontmatter.alias %>
```
### 每日一句/一图
每天随意调用一句话或者一张图片：
```js
# 每日一句
	<%+ tp.web.daily_quote() %>
# 每日一图
	<%+ tp.web.random_picture() %>

# 每日一图，控制图片尺寸
	<% tp.web.random_picture("200x200") %>

# 每日一图，控制图片尺寸+关键字
	<% tp.web.random_picture("200x200", "landscape,water") %>
```

### 光标位置
插入模板后将光标设置到此位置：
```js
	<% tp.file.cursor(1) %>
	<% tp.file.cursor(2) %>
	<% tp.file.cursor(3) %>
```

### tp的动态语法
动态语法就是在普通语法的 `%` 号后面加上 `+`。就会变成实时获取的模板语法：
```js
	<% tp.date.now("YYYY-MM-DD") %>
# 动态语法
	<%+ tp.date.now("YYYY-MM-DD") %>
```
