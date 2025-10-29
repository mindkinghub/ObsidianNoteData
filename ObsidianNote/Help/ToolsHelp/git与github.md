# 介绍
## git
[Git](https://git-scm.com/)属于分散型版本管理系统，是为版本管理而设计的软件。版本管理就是管理更新的历史记录。
## GitHub
- [GitHub](https://github.com)是为开发者提供Git仓库的托管服务
# 学习参考网站
## git
-  [Git tutorial](https://missing.csail.mit.edu/2020/version-control/)
- [如何写好 Commit Message](https://chris.beams.io/posts/git-commit/)
- [实现自己git的tutorial](https://wyag.thb.lt/)
- [Learn Git Branching](https://learngitbranching.js.org/)
## GitHub
-  [GitHub的官方教程](https://docs.github.com/cn/get-started)

# git教程
官网：[Git](https://git-scm.com/)
安装教程：[Git 详细安装教程（详解 Git 安装过程的每一个步骤）_git安装-CSDN博客](https://blog.csdn.net/mukes/article/details/115693833)

### windows系统配置SSH密钥验证
#### 步骤 1：在 Windows 系统上生成 SSH 密钥
1. 打开 PowerShell 或 CMD
	在 Windows 上使用 PowerShell 或 CMD 生成 SSH 密钥。可以在 “开始” 菜单中搜索 PowerShell 或 CMD 并打开。

2. 生成密钥对
	输入以下命令生成 SSH 密钥对：`ssh-keygen -t rsa -b 4096 -C "snn_adversial"`
	- `-t rsa`：指定密钥类型为 RSA。
	- `-b 4096`：设置密钥长度为 4096 位，以增加安全性。
	- `-C "snn_adversial"`：注释信息，可用于标识密钥，如使用者名称或用途。

3. **保存密钥**  
    系统会提示输入文件的保存路径，建议按默认路径 `C:\Users\Leo\.ssh\id_rsa` 保存，直接按回车键即可。
4. **设置密码短语（可选）**  
	系统接着会询问是否设置密码短语，添加密码短语会增加安全性，但为了自动化连接，可以直接按回车跳过。

生成完成后，密钥对会保存在 `C:\Users\Leo\.ssh` 目录下，包括以下两个文件：
- `id_rsa`：私钥文件，请务必妥善保管。
- `id_rsa.pub`：公钥文件，用于在服务器上配置。

#### 步骤 2：将公钥上传到服务器

1. **查看公钥内容**  
    在 Windows 上，查看公钥文件 `id_rsa.pub` 的内容。通常以 `ssh-rsa` 开头并包含一长串字符。
	**复制整个公钥内容**

2. **通过密码登录到服务器**  
	通过以下命令登录服务器（首次登录需要输入密码）：`ssh -p 端口号 root@i-2.gpushare.com`
3. **在服务器上配置公钥**  
	登录服务器后，将公钥添加到 `~/.ssh/authorized_keys` 文件中。
	- 首先，创建 `.ssh` 目录（若已存在则跳过）：
		- `mkdir -p ~/.ssh`
		- `chmod 700 ~/.ssh`
	- 使用文本编辑器（例如 `nano`）编辑或创建 `authorized_keys` 文件：
		- `nano ~/.ssh/authorized_keys`
	- 将公钥内容粘贴到 `authorized_keys` 文件中并保存。
	- 设置 `authorized_keys` 的权限，确保仅用户自己可以访问：
		- `chmod 600 ~/.ssh/authorized_keys`
#### 步骤 3：在 Windows 上配置 SSH 客户端使用密钥连接

1. **编辑 SSH `config` 文件**  
    打开 `C:\Users\Leo\.ssh` 目录，在其中创建或编辑 `config` 文件（无文件后缀）。在文件中添加以下内容以配置 SSH 连接：
```
Host snn-adversial
  HostName i-2.gpushare.com
  Port 33804
  User root
  IdentityFile C:\Users\Leo\.ssh\id_rsa
```
- `Host snn-adversial`：这是一个连接的别名。
- `HostName`：服务器地址。
- `Port`：服务器的端口号。
- `User`：登录用户名。
- `IdentityFile`：私钥的本地路径，指向刚才生成的 `id_rsa` 文件。
2. **测试连接** 
	配置完成后，可以通过以下命令来测试 SSH 连接，无需输入密码：`ssh snn-adversial`
	若配置正确，将直接连接到服务器。

#### 步骤 4：可选 - 使用 SSH Agent 缓存密码短语（如果设置了密码短语）
如果生成密钥时设置了密码短语，可以使用 SSH Agent 来缓存，从而避免每次连接都输入密码短语。

1. 启动 SSH Agent
	在 PowerShell 或 CMD 中输入以下命令启动 SSH Agent：`Start-Service ssh-agent`

2. **将私钥添加到 SSH Agent**  
	使用以下命令将私钥添加到 SSH Agent：`ssh-add C:\Users\Leo\.ssh\id_rsa`

3. **输入密码短语**  
    添加私钥时会提示输入密码短语，SSH Agent 会缓存此短语，之后的连接无需再次输入。

#### 验证连接
现在，可以通过以下命令验证连接：`ssh snn-adversial`
如果一切配置正确，将直接连接到服务器而无需输入密码或密码短语。

## git 相关操作
### git bash中的快捷键
- **复制: `ctrl + insert`**
- **粘贴: `shift + insert`**

### git 相关操作
```bash
git clone +仓库路径

//创建一个目录
mkdir git-tutorial
//进入目录
cd git-tutorial
//初始化仓库
git init
//查看仓库状态
git status
//touch修改文件或者目录的时间属性，包括存取时间和更改时间。若文件不存在，系统会建立一个新的文件
touch README.md
//向暂存区中添加文件
git add README.md
//保存仓库的历史记录
git commit
git commit -m "First commit" //-m 参数后面的"First commit"称作提交信息，是对这个提交的概述

//中止提交
//将提交信息留空并直接关闭编辑器，随后提交就会被中止

//查看提交日志
git log
//只显示提交信息的第一行
git log --pretty=short
//只显示指定目录、文件的日志（在git log 后加上目录名,如果加的是文件名，就只会显示与该文件相关的日志）
git log README.md
//显示文件的改动
git log -p
git log -p README.md//只查看README.md文件的提交日志以及提交前后的差别

//查看更改前后的差别
git diff
git diff HEAD//这里的HEAD是指向当前分支中最新一次提交的指针

//显示分支一览表
git branch//master分支是Git默认创建的分支，*表示当前所在的分支

//创建、切换分支
git checkout -b feature-A//创建名为feature-A的分支
(git branch feature-A  git checkout feature-A)这两条命令也可创建feature-A分支
git checkout master//切换到master分支
git checkout -//"-"代替分支名，就可以切换至上一个分支

//合并分支(在master主分支下合并)
git merge --no-ff feature-A//在合并时加上--no-ff参数，随后编辑器会启动，将编辑器中显示内容保存，关闭编辑器
git merge main//将当前分支合并到main分支
git merge bugFix//若是在main分支下操作,则将产生新节点与bugFix关联
//以图表形式查看分支
git log --graph//可以按q退出

//回溯历史版本
git reset --hard //让仓库的HEAD、暂存区、当前工作树回溯到指定状态，需要提供目标时间点的哈希值
git reset --hard //加上哈希值，Git历史版本识别是通过一个SHA-1哈希码实现的，最少提供4个字符，一般提供8个字符
git reset HEAD~1//回溯到前一节点
git revert HEAD//往后创建一个节点,同时移动到创建的节点

git log//查看当前时间节点以前的所有历史提交
git reflog//查看当前时间节点以前所有历史提交，以及当前时间节点之后所有提交
//只要不进行Git的GC（Garbage Collection,垃圾回收），就可以通过日志随意调取近期的历史状态

//修改提交信息
git commit --amend

//压缩历史
git rebase -i
git commit -am//-am合并add与commit命令（对已经提交过一次的文件可以直接一步执行）
//错字漏字等失误称作typo
git rebase -i HEAD~2//可以选定当前分支中包含HEAD（最新提交）在内的两个最新历史记录为对象，并在编辑器中打开
//在编辑器中将Fix typo前的pick改为fixup，保存编辑器内容，关闭编辑器
git rebase main //将当前分支移动到main下
git rebase bugFix//将当前分支移动到bugFix下

//删除分支
//删除本地分支
git branch -d <local_branch>//例：git branch -d dev
git branch -D <local_brnach>//强制删除此分支
//删除远程分支
git push origin --delete 分支名

git branch -f main HEAD~3//将main分支向前移动3个单位

//删除.git仓库
rm -rf .git

```

# GitHub教程
## 为GitHub账户设置SSH key
git使用rsa，rsa要解决的一个核心问题是，如何使用一对特定的数字，使其中一个数字可以用来加密，而另外一个数字可以用来解密。这两个数字便是public key也就是公钥以及private key私钥。

### **生成ssh key**
首先检查是否已生成密钥 `cd ~/.ssh`，ls如果有2个文件，则密钥已经生成，id_rsa.pub就是公钥
如果没有生成，那么通过$ ssh-keygen -t rsa -C “邮箱地址”来生成。
1. 是路径确认，直接按回车存默认路径即可
2. 直接回车键，这里不推荐使用密码进行登录;
3. 直接回车键
生成成功后，去对应目录C:\Users\Y\ .ssh里（Y为电脑用户名，每个人不同）。打开id_rsa.pub，得到ssh key公钥
### **为github账号配置ssh key**
切换到github，点击settings。
然后打开SSH keys菜单， 点击Add SSH key新增密钥，填上标题，跟仓库保持一致。
接着将id_rsa.pub文件中key粘贴到此，最后Add key生成密钥。
## 推送至远程仓库
### 初始流程
先在GitHub上新建一个仓库

```cpp
echo "# git-tutorial" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:mindkinghub/git-tutorial.git
git push -u origin main//create a new repository on the command line

git remote add origin git@github.com:mindkinghub/git-tutorial.git
git branch -M main
git push -u origin main//push an existing repository from the command line

git push -u origin feature-D//将feature-D push给远程仓库并保持分支名称不变
git push//直接在克隆时制定本地分支和远程跟踪分支的关联关系，可以直接push

//获取远程仓库
git clone+仓库路径
git branch -a//查看当前分支的相关信息，添加-a参数可以同时显示本地仓库和远程仓库的分支信息

git checkout -b feature-D //-b参数后面是本地仓库中新建分支的名称
```

如何将已有文件夹（本来是github上的仓库内容，但是删除了.git，且内容做了更新）和github上的同样的仓库同步
```c++
git init
git remote add origin https://github.com/your-username/your-repository.git

git pull origin main --allow-unrelated-histories //从远程仓库拉取最新的内容，看看是否有更新 `--allow-unrelated-histories` 允许合并两个没有共同历史的 Git 仓库。

git config --global user.email "you@example.com"
git config --global user.name "Your Name"


git add .
git commit -m "Your commit message"

git push origin main

```

### 可选操作
#### 添加`.gitignore`文件
`.gitignore`文件用于忽略不需要上传的文件，比如`.pyc`缓存文件、虚拟环境、依赖包等。
```git
# .gitignore 示例
__pycache__/
*.pyc
*.pyo
*.pyd
.env
.vscode/
.idea/
.DS_Store
```

创建`.gitignore`文件：`echo "__pycache__/" >> .gitignore`
## GitHub功能
### 键盘快捷键

在各个页面按下`shift+/`都可以打开键盘快捷键一览表
### 查看差别
1. **查看分支间的差别**
	- 比如我们想查看4-0-stable分支与3-2-stable分支之间的差别，可以像下面这样将分支名加到URL里。`https://github.com/rails/rails/compare/4-0-stable…3-2-stable`
2. **查看与几天前的差别**
	- 假如我们想查看master分支在最近7天内的差别，可以像这样将时间加入URL：`https://github.com/rails/rails/compare/master@{7.day.ago}…master`
	- `{day,week,month,year}`指定期间可以使用以上四个时间单位。如果差别过大则不会列出所有提交，只显示最近的一部分
3. **查看与指定日期之间的差别**
	- 假设我们想查看master分支2013年1月1日与现在的区别，可以将日期加入URL`https://github.com/rails/rails/compare/master@{2013-01-01}…master`
### Pull Request
是用户修改代码后向对方仓库发送采纳请求的功能
#### 以diff和patch格式文件的形式来处理Pull Request
假设Pull Request的URL如下所示：`htpps://github.com/用户名/仓库名/pull/28`

如果想获取diff格式文件，在URL末尾添加.diff即可：`https://github.com/用户名/仓库名/pull/28.diff`

如果想获取patch格式文件，在URL末尾添加.patch即可：`htpps://github.com/用户名/仓库名/pull/28.patch`

在Conversation中，选中想引用的评论然后按**R**键，被选择的部分就会自动以评论语法写入评论文本框。在评论中输入“：”便会启动表情自动补全功能。
在URL的末尾添加“？w=1”就可以不显示空格的差别。
### Wiki
是一个使用简单的语法就能编写文档的功能
### Pulse
是体现该仓库软件开发活跃度的功能
### Issue
是将一个任务或问题分配给一个Issue进行追踪和管理的功能。每一个功能更改或修正都对应一个Issue，讨论或修正都以这个Issue为中心进行。
### 下载项目
利用gitclone.com加速：在仓库url中增加`gitclone.com`的前缀 即`https://github.com/`修改为`https://gitclone.com/github.com/`。
这种加速目前只支持`git clone` 和`git pull` 命令，所以适用于拉取别人代码进行本地查看的应用场景。

# problem
## 大文件上传失败
**GitHub 的推荐解决方案**：
- GitHub 推荐使用 [Git Large File Storage (LFS)](https://git-lfs.github.com/) 来管理这些大文件，以避免它们影响 Git 操作和存储。
- Git LFS 是专为大文件设计的 Git 扩展，它将大文件存储在专门的服务器上，而 Git 仓库中仅保留这些文件的指针，从而减少 Git 的存储压力。
```git
git lfs install
git lfs track "*.pdf"  # 或者其他大文件类型
git add .gitattributes
git add .
git commit -m "Add large files with Git LFS"
git push
```
### 1. 安装 Git LFS
如果你尚未安装 Git LFS，可以通过以下命令进行安装：
- **Windows**: 直接下载并安装 Git LFS：[Git LFS 下载链接](https://git-lfs.github.com/)
### 2. 初始化 Git LFS
安装完成后，运行以下命令初始化 Git LFS：`git lfs install`
### 3. 跟踪大文件
然后，使用 `git lfs track` 命令指定要通过 Git LFS 跟踪的文件类型。例如，针对 PDF 文件，你可以运行以下命令：`git lfs track "*.pdf"`
这会将所有 `.pdf` 文件标记为由 Git LFS 管理。
### 4. 提交 `.gitattributes` 文件
Git LFS 会在你的仓库中生成一个 `.gitattributes` 文件，它用于存储文件跟踪信息。你需要将这个文件提交到仓库中：
```bash
git add .gitattributes
git commit -m "Track PDF files with Git LFS"
```
### 5. 移除现有的大文件并重新提交
例子：由于你之前已经提交了较大的 PDF 文件，Git LFS 并不会自动管理这些已经提交的文件。因此，你需要移除它们并重新提交。
- 首先，撤销提交并移除大文件：
```bash
git rm --cached media/books/pdfs/*.pdf
git commit -m "Remove large PDF files for LFS tracking"
```
- 然后，重新将这些文件添加到 Git LFS，并提交：
```bash
git add media/books/pdfs/*.pdf
git commit -m "Add large PDF files to LFS"
```
### 6. 推送更改
最后，推送更改到远程仓库：`git push origin main`

## fatal: refusing to merge unrelated histories
原因：本地和远程仓库历史不同
解决：使用强制合并`git pull origin main --allow-unrelated-histories`

## LF will be replaced by CRLF the next time Git touches it
Git 可以在你提交时自动地把回车（CR）和换行（LF）转换成换行（LF），而在检出代码时把换行（LF）转换成回车（CR）和换行（LF）。 可以用 `git config --global core.autocrlf true `来打开此项功能。