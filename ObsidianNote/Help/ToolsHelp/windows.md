
### mklink
```
mklink [[/D] | [/H] | [/J]] Link Target
/D      创建目录符号链接。默认为文件符号链接。
/H      创建硬链接而非符号链接。
/J      创建目录联接。
Link    指定新的符号链接名称。
Target  指定新链接引用的路径(相对或绝对)。
```
`mklink /j “链接目录” “目标目录”`

1. 找到要链接的文件或文件夹
2. 将其复制到空间富裕的盘中
3. 以管理员身份打开cmd，输入`mklink /j "<orig path>" "<new path>"`
	-  `<orig path>` 是原来文件夹的完全路径
	- ` <new path> `是复制的新文件夹的完全路径
4. 删除原来的文件夹（先不要清空回收站）
5. 命令行执行刚刚的命令
6. 当看到AppData目录有有链接文件夹生成时，代表成功了。**前面和这里没出现啥警告的话，就可以清空回收站了，C盘就清理出来了。**

[https://github.com/zbezj/HEU_KMS_Activator/tree/61.1.0](https://github.com/zbezj/HEU_KMS_Activator/tree/61.1.0)
### 虚拟化**Hyper-V**

- 打开控制面板
- 点击程序
- 选择打开或关闭Windows功能
- 勾选Hyper-V选项
- 展开它，然后确保选中两个选项
- 重启PC
- 搜索Hyper-V Manager