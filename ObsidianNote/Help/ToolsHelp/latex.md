推荐的学习路线如下：

- LaTeX 的环境配置是个比较头疼的问题。如果你本地配置 LaTeX 环境出现了问题，可以考虑使用 [Overleaf](https://www.overleaf.com/) 这个在线 LaTeX 编辑网站。站内不仅有各种各样的 LaTeX 模版供你选择，还免去了环境配置的难题。
- 阅读下面三篇 Tutorial: [Part-1](https://www.overleaf.com/latex/learn/free-online-introduction-to-latex-part-1), [Part-2](https://www.overleaf.com/latex/learn/free-online-introduction-to-latex-part-2), [Part-3](https://www.overleaf.com/latex/learn/free-online-introduction-to-latex-part-3)。
- 学习 LaTeX 最好的方式当然是写论文，不过从一门数学课入手用 LaTeX 写作业也是一个不错的选择。

其他值得推荐的入门学习资料如下：
- 一份简短的安装 LaTeX 的介绍 [GitHub](https://github.com/OsbertWang/install-latex-guide-zh-cn)或者 TEX Live 指南（texlive-zh-cn）[PDF](https://www.tug.org/texlive/doc/texlive-zh-cn/texlive-zh-cn.pdf) 可以帮助你完成安装和环境配置过程
- 一份（不太）简短的 LaTeX2ε 介绍（lshort-zh-cn）[PDF](https://mirrors.ctan.org/info/lshort/chinese/lshort-zh-cn.pdf) [GitHub](https://github.com/CTeX-org/lshort-zh-cn)是由 CTEX 开发小组翻译的，可以帮助你快速准确地入门，建议通读一遍
- 刘海洋的《LaTeX 入门》，可以当作工具书来阅读，有问题再查找，跳过 CTEX 套装部分


# 符号表
文本/数字模式通用符号：
![[attachments/Pasted image 20251015010536.png]]
希腊字母：
`\Alpha`，`\Beta`等希腊字母符号不存在，因为它们和拉丁字母`A,B`等一模一样；小写字母里也不存在 `\omicron`，直接用拉丁字母`o`代替。
![[attachments/Pasted image 20251015010800.png]]
二元关系符：
所有的二元关系符都可以加`\not`前缀得到相反意义的关系符，例如`\not=`就得到不等号（同`\ne`）
![[attachments/Pasted image 20251015011025.png]]
二元运算符：
![[attachments/Pasted image 20251015011059.png]]
巨算符：
![[attachments/Pasted image 20251015011144.png]]
数学重音符号：
最后一个`\wideparen`依赖`yhmath`宏包。
![[attachments/Pasted image 20251015011229.png]]
箭头：
![[attachments/Pasted image 20251015011303.png]]
作为重音的箭头符号：
![[attachments/Pasted image 20251015011333.png]]
定界符：
`amsmath`还定义了`\lvert、\rvert`和`\lVert、\rVert`，分别作为`\vert`和`\Vert`对应的开符号（左侧） 和闭符号（右侧）的命令。
![[attachments/Pasted image 20251015011414.png]]
用于行间公式的大定界符：
![[attachments/Pasted image 20251015011434.png]]
其他符号：
![[attachments/Pasted image 20251015011452.png]]
## AMS符号
本小节所有符号依赖`amssymb`宏包。
AMS希腊字母和希伯来字母：
![[attachments/Pasted image 20251015011538.png]]
AMS二元关系符：
![[attachments/Pasted image 20251015011613.png]]
AMS二元运算符：
![[attachments/Pasted image 20251015011631.png]]
AMS箭头：
![[attachments/Pasted image 20251015011649.png]]
AMS反义二元关系符和箭头：
![[attachments/Pasted image 20251015011708.png]]
AMS定界符：
![[attachments/Pasted image 20251015011722.png]]
AMS其它符号：
![[attachments/Pasted image 20251015011738.png]]

| 符号名称 | latex表示形式         | 示例                      |
| ---- | ----------------- | ----------------------- |
| 上划线  | \overline{ }      | $$\overline{f}$$        |
| 下划线  | \underline{ }     | $$\underline{f}$$       |
| 向上取整 | \lceil x \rceil   | $\lceil x \rceil$<br>   |
| 向下取整 | \lfloor x \rfloor | $\lfloor x \rfloor$<br> |

