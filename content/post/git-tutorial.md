---

title: Git 教程
abbrlink: git-tutorial
date: 2021-03-25 23:00:08
tags: [Git]
categories: 

---

简明 Git 教程

<!--more-->

学习过程中，有任何问题建议去 [Google](https://www.google.com/) 搜索，No baidu.

# Git 介绍

## Git 是什么？

[Git]( https://zh.wikipedia.org/wiki/Git) 是目前世界上最先进的分布式版本控制系统(Distributed Version Control System)，是由 Linux 之父 **林纳斯·托瓦兹** (Linus Torvalds) 创作。

什么是版本控制，举个例子，你每天都会新增、编辑、修改许多文档，当修修改改很多次之后，你觉得不满意想回到以前的某个版本，得手动修改添加过的，非常不方便，于是，版本控制系统就可以很好的解决这个问题，Git 就像玩游戏的时候可以存储进度一样，当你修修改改发现被改乱了自己都看不懂的时候，可以回到到以前的任意版本。

## 为什么使用它？

软件工程师们一般不会一次性完成一个项目，他们一般都有一个计划来安排需要完成的工作。如果你的个人项目是在数天或数周内完成的，那么记录你在某一天完成的工作就会变得很有好处，而将修改暂时或不修改的内容回滚到之前的时间点的权力是很有价值的。当与团队中的其他人合作时，这一点变得更加重要--哪些文件是由哪些合作者修改的？当多个合作者想对同一个文件进行修改时怎么办？如前所述，Git 的主要功能是 "版本控制"--组织和跟踪一个项目在一段时间内所做的修改，不管是只有你一个人在做，还是一个团队在做。

# 环境安装

## 安装 Git

### 在 Linux 上安装 Git

在 Linux 下安装 Git 最简单了，只需一行命令：

```bash
$ sudo apt-get install git
```

即可安装成功

### 在 Windows 上安装 Git

在 Git官网 [下载安装程序](https://git-scm.com/downloads) 按默认选项安装即可。

安装完成后，即可看到右键菜单多了 Git Gui Here 和 Git Bash Here 这两个选项，说明 Git 已经安装成功了！

### 在 Mac OS X 上安装 Git

网站：https://git-scm.com/download/mac

只要下载、点开、执行，基本上这样就可以顺利完成安装了！

安装成功后，随便在哪里右键选择 Git Bash Here ，输入以下命令查看 git 版本：

```bash
$ git --version
git version 2.30.2.windows.1
```

# 配置 Git

安装 Git 后首先要做的事情是设置你的用户名称和 Email 地址（用户标识，必要）。

打开终端，输入以下两行命令（#右边的不用输入，# 右边的为注释，不会被执行）：

```bash
$ git config --global user.name "Your Name“ # Your Name 替换为你的名字
```

```bash
$ git config --global user.email "Your Email Address"  # Your Email Address 替换为你的邮箱地址
```

完成之后，可以再检查一下目前的设定：

```bash
$ git config --list
user.name=xxx
user.email=example@gmail.com
```

# Git 的基本知识

Git 本地有三个工作区域：工作目录（Working Directory）、暂存区（Stage/Index）、资源库（Repository 或 Git Directory）。如果再加上远程的 git 仓库（Remote Directory）就可以分为四个工作区域。

**Working Directory**：工作目录，就是你平时存放项目代码的地方，或者是你需要进行版本控制的文件夹目录。

**Repository**：资源库（或本地仓库），工作区有一个隐藏目录 `.git`，这里面有你提交到所有版本的数据，这个不算工作区，而是Git的版本库。

**Index/Stage**：暂存区，或者叫待提交更新区，在提交进入 repo 之前，我们可以把所有的更新放在暂存区。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫 index）的暂存区，还有 Git 为我们自动创建的第一个分支 `master` ，以及指向 `master` 的一个指针叫 `HEAD`。

![repo.jpg](https://i.loli.net/2021/03/26/d7AYu43t5IZTE9s.jpg)

**远程的 git 仓库（Remote Directory）**：这个就是你的 GitHub 上的仓库

文件在这四个区域之间的转换关系如下：

![git-connections.png](https://i.loli.net/2021/03/26/re7YhnO9xNa2cQl.png)

**工作流程**

git 的工作流程一般是这样的：

１、在工作目录中添加、修改文件；

２、将需要进行版本管理的文件放入暂存区域；

３、将暂存区域的文件提交到 git 仓库。

因此，git管理的文件有三种状态：已修改（modified），已暂存（staged），已提交(committed)

Git 工作流程图

![Git工作流程图.png](https://i.loli.net/2021/03/28/N3FveKqtYfxA8zn.png)

平时使用只需记住下图 6 个命令：

![gitflow.png](https://i.loli.net/2021/03/26/3t2x1D4rZThgHuR.png)

> 记住，你可以使用以下命令来了解关于这些命令的更多信息
> 
> `git command --help` i.e., `git checkout --help`

# 一个小例子

这里我们在本地以一个小例子演示 git 的基本使用方法。
一起动手实践吧！

## Local Repository：本地仓库

### 创建工作目录

Git 项目需要一个文件夹，这个文件夹就是工作目录，就叫 `git_test` 吧！

在桌面上右键，Git Bash Here，输入以下命令

```bash
$ mkdir git_test # 新建文件夹
$ cd git_test # 进入 git_test 工作目录
```

上面两行命令，做了以下几件事：
1.使用 `mkdir` 创建名为 `git_test` 的文件夹，这就是我们的 working directory
2.使用 `cd` 切换到 `git_test` 目录

### 创建本地仓库

我们已经创建了工作目录，现在，需要在这里创建我们的 Local Repository，也就是本地仓库，这样才能将本目录纳入版本控制中。

```bash
$ git init # 初始化 Local Repository，让 git 对此目录进行版本控制
Initialized empty Git repository in C:/Users/Turing/Desktop/git_test/.git/
```

使用 `git init` 初始化此目录，这样就可以让 Git 对这个目录进行版本控制。

![0N_V6_RL_PH3X~TJS0QD__W.png](https://i.loli.net/2021/03/26/HAsLb7MUoD3BGYh.png)

我们可以看到执行 `git init` 后，在目录下有个 `.git` 的隐藏文件夹，这就是 local repo，有兴趣可以看看里面的内容 。

> 如果你看不到，请勾选 显示隐藏的项目 。

由于当前项目 `git_test` 只在我们自己电脑上，其他人无法访问，所以我们称这种形式的版本库为 **本地仓库**。

如果有一天你想让这个目录不再被 Git 控制，其实 Git 的版本控制很单纯，全部都是靠那个 `.git` 目录在做事而已，所以如果这个不想被版控，或是只想给客户不含版本控制记录的內容的话，只要把那个 `.git` 目录移除，Git 就对这个目录失去控制权了。

> 也就是说，在这个目录里，你只要没有删除 `.git` 文件夹，其他的随便删都可以找回来，`.git` 被删除了就没有办法了。

## 添加进暂存区（Staging Area）

先介绍下 `git status` 这个命令，这个命令是用来查询当前目录的「状态」，先在刚刚建立的 `git_test` 目录下执行这个指令：

```bash
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

在这个目录里，现在除了 Git 帮你创建的那个 `.git` 隐藏目录外什么都没有，所以上面这段信息就是跟你说「现在没有东西可以提交（nothing to commit）」。
现在，我们创建一个 txt 文本，输入 `Talk is cheap, show me the code.` 并保存， 再使用 `git status` 来查看目录状态：

```bash
$ echo "Talk is cheap, show me the code."> a.txt # 如果不会用命令行创建文件，可以手动创建a.txt 并输入内容保存
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.txt

nothing added to commit but untracked files present (use "git add" to track)
```

现在就和刚才不一样了，可以看到 `a.txt` 文件的状态是 `Untracked files` ，意思是这个文件没有加入到 Git 版本控制系统中，还没有被 Git 追踪，只是刚加到了目录里面。

使用命令 `git add` + 文件名称 来追踪文件，加入到 Stage 暂存区：

```bash
$ git add a.txt
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
```

可以看到 `a.txt` 文件的状态变为了 `new file` 状态了，此时这个文件已被存到暂存区（Staging Area），没有 add 的文件还是再工作区，add 之后才能进行 commit 等操作。

> 如果有很多文件要 add，那么使用 `git add --all` 即可将所有文件添加进暂存区。 
> 
> **`--all` 跟 `.` 参数有什么不一样？**
> 有时候会看到別人说 `git add .` 指令也可以把所有的文件全部加到暂存区喔！」，这样的说法其实不完全正确。
> 
> 区别就是 **执行指令时候的目录位置**：
> `git add .` 这个指令会把目前当下这个目录，以及它的子目录、子子目录、子子子目录...里的异动全部加到暂存区，但在这个目录的以外的就不归它管了。而 `git add --all` 指令就没这个问题，这个指令不管在哪一层目录执行，效果都是一样的，在这个工作目录里所有的异动都会被加至暂存区。
> 
> 还有一种区别就不讨论了，Git 2.x 之后，就只是上面的一种区别了。

## 提交到本地仓库（Local Repository）

如果仅是通过 `git add` 命令把文件加到暂存区是不够的，这样还不算是完成整个流程。要让暂存区的內容永久的存下來的話，使用的是 `git commit -m <message>` 命令：

```bash
$ git commit -m "init commit"
[master (root-commit) 3777d07] init commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt
```

`git commit` 的操作就是相当于把一个文件在 git 的系统中进行存档了，这个 commit 需要一个 `-m` 参数并且需要传入一个 message，就是对本次 commit 的一个简述，说明「你在这次的 Commit 做了什么事情」，只要使用简单、清楚的文字说明就好，中、英文都可，重点是清楚，让不久之后的你或是你的同事能很快的明白就行了，对于 commit message 是有一定的规范的，可参看 [freecodecamp](https://www.freecodecamp.org/news/writing-good-commit-messages-a-practical-guide/)。

当完成了这个动作后，对 Git 来说就是「把暂存区的东西存放到本地仓库（Local Repository）里」，换言之就是「我完成一个存档（或备份）的动作了」，此文件已经纳入到版本控制中了。

到底 Commit 了哪写东西？

> 请先记住一个很重要的概念：「Git 每次的 commit 都只会处理暂存区（Staging Area）里的內容」。也就是说，如果在执行 git commit 指令的時候，那些还没被 add 到暂存区的里的文件，是不会被 commit 到本地仓库的。

那个信息是什么？很重要吗？一定要有吗？

> 是的，很重要！很重要！很重要！（重要的事情说三遍！！！）
> 
> 在 commit 的时候，如果没有输入这个信息，Git 预设是不会让你完成Commit 这件事的。它最主要的目的就是告诉你自己以及其它人「这次的修改做了什么」。

commit 之后，再次输入 `git status` 查看状态：

```bash
$ git status
On branch master
nothing to commit, working tree clean
```

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的（working tree clean）。

## 时光穿梭

我们已经成功地添加并提交了一个 `a.txt` 文件，现在，是时候继续工作了，于是，我们继续修改 `a.txt` 文件，改成如下内容：

```
Talk is not cheap, show me the code.
```

运行 `git status` 命令看看结果：

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

可以看到， `a.txt ` 文件被修改（modified）过了，但还没有准备提交的修改。
虽然Git告诉我们 `a.txt` 被修改了，但如果能看看具体修改了什么内容，自然是很好的。比如你几周前的代码，今天打开看时，已经记不清上次怎么修改的 `a.txt`，所以，可以用 `git diff <file>` 这个命令看看：

```bash
$ git diff a.txt
warning: LF will be replaced by CRLF in a.txt.
The file will have its original line endings in your working directory
diff --git a/a.txt b/a.txt
index 44b4314..4986cc2 100644
--- a/a.txt
+++ b/a.txt
@@ -1 +1 @@
-Talk is cheap, show me the code.
+Talk is not cheap, show me the code.
```

`-` 号开头那行（通常是红色的）是删除的
`+` 号开头那行（通常是绿色的）是新添加的
从上面的命令输出看到，我们在添加了一个 not 单词。

现在我们将其 add 到暂存区并提交：

```bash
$ git add a.txt
$ git commit -m "add not"
[master 39fcc71] add not
 1 file changed, 1 insertion(+), 1 deletion(-)
```

提交后，我们再用 `git status` 命令看看仓库的当前状态：

```bash
$ git status
On branch master
nothing to commit, working tree clean
```

Git告诉我们当前没有需要提交的修改，而且，工作目录是干净（working tree clean）的。

### 版本回退：回到过去

修改 `a.txt` 文件如下：

```
Talk is not cheap, show me the code.
Everything is a file.
```

然后 add，commit：

```bash
$ git add a.txt
$ git commit -m "ADD Everything is a file"
[master 11f7dd8] ADD Everything is a file
 1 file changed, 1 insertion(+)
```

像这样，你对文件进行修修改改，然后提交到版本库中，好比玩游戏时，隔一段时间你存一下档，存档再 Git 中就是 commit 。当你文件改乱了，或者不小心误删了，可以恢复到任意一个 commit，然后继续工作。

现在，我们来看看 `a.txt` 文件一共有几个版本，使用 `git log` 查看：

```bash
$ git log
commit 11f7dd8176bb68c7c4724db94bfbad5d05105d13 (HEAD -> master)
Author: turing0 <turing175@gmail.com>
Date:   Fri Mar 26 13:44:51 2021 +0800

    ADD Everything is a file

commit 39fcc71d1c717b18e306d352e15ab4d8719ec0b1
Author: turing0 <turing175@gmail.com>
Date:   Fri Mar 26 13:28:33 2021 +0800

    add not

commit 170b595f8f698d4412acea23840cca35afe1e7fb
Author: turing0 <turing175@gmail.com>
Date:   Fri Mar 26 13:18:17 2021 +0800

    init commit
```

`git log` 命令显示从最近到最远的提交日志，我们可以看到3次提交，最近的一次是 `ADD Everything is a file` ，上一次是 `add not`，最早的一次是 `init commit`。

如果你觉得输出信息太多，不好看，可以使用 `--pretty=oneline` 参数：

```bash
$ git log --pretty=oneline
11f7dd8176bb68c7c4724db94bfbad5d05105d13 (HEAD -> master) ADD Everything is a file
39fcc71d1c717b18e306d352e15ab4d8719ec0b1 add not
170b595f8f698d4412acea23840cca35afe1e7fb init commit
```

你看到的一大串类似 `11f7dd...`的是 `commit id`（版本号），和 SVN 不一样，Git 的 `commit id` 不是1，2，3…… 递增的数字，而是一个 SHA1 计算出来的一个非常大的数字，用十六进制表示，而且你看到的 `commit id` 和我的肯定不一样，以你自己的为准。为什么 `commit id` 需要用这么一大串数字表示呢？因为 Git 是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用 1，2，3…… 作为版本号，那肯定就冲突了。

现在，比如你想把 `a.txt` 回退到上一个版本，也就是 `add not` 的那个版本，怎么做呢？
首先，Git 必须知道当前版本是哪个版本，在 Git 中，用 `HEAD `表示当前版本，也就是最新的提交 `11f7dd...` （注意我的提交ID和你的肯定不一样），上一个版本就是 `HEAD^`，上上一个版本就是`HEAD^^`，当然往上 100 个版本写 100 个 `^` 比较容易数不过来，所以写成 `HEAD~100`。

现在，我们要把当前版本 `ADD Everything is a file` 回退到上一个版本 `add not`，就可以使用 `git reset` 命令：

```bash
$ git reset --hard HEAD^
HEAD is now at 39fcc71 add not
```

`--hard` 参数后面再讲，现在我们看看 `a.txt` 里面的内容是不是我们想要的样子（你也可以手动打开文件进行查看）。

```bash
$ cat a.txt
Talk is not cheap, show me the code.
```

显然，达到了我们的想要的效果。

你也可以继续回退到第一个版本，不过现在让我们用 `git log` 来看看版本库的状态（有时候信息很多，按回车可以继续往下滚动查看，按 `q` 键退出）：

```bash
$ git log
commit 39fcc71d1c717b18e306d352e15ab4d8719ec0b1 (HEAD -> master)
Author: turing0 <turing175@gmail.com>
Date:   Fri Mar 26 13:28:33 2021 +0800

    add not

commit 170b595f8f698d4412acea23840cca35afe1e7fb
Author: turing0 <turing175@gmail.com>
Date:   Fri Mar 26 13:18:17 2021 +0800

    init commit
```

会看到：之前 `ADD Everything is a file` 的版本不在了，我们还能回到那个版本吗，可以的，前提是你没有关闭当前的命令行窗口，你可以往回翻，找到 `ADD Everything is a file` 对应的 `commit id` 是 `11f7dd...`，于是我们可以指定回到这个版本：

```bash
$ git reset --hard 11f7dd
HEAD is now at 11f7dd8 ADD Everything is a file
```

版本号可以不用写全，只需写前几位就可以了，Git 会自动去找。当然也不能只写前一两位，因为 Git 可能会找到多个版本号，就无法确定是哪一个了。

你可以查看 `a.txt` 的内容，会发现又回来了。

**Reset 的模式**

`git reset` 指令可以搭配参数使用，常見到的三种参数，分別是` --mixed` 、 `--soft` 以及 `--hard` ，不同的参数执行之后会有稍微不太一样的结果

**mixed 模式**

`--mixed` 是预设的参数，如果沒有特別加参数， `git reset` 命令将默认使用 `--mixed` 模式。这个模式会把暂存区的文件丟掉，但不会改动工作目录的文件，也就是说 Commit 拆出来的文件会留在工作目录，但不会留在暂存区。

**soft 模式**

这个模式下的 reset，工作目录跟暂存区的文件都不会被丟掉，所以看起来就只有 HEAD 的移动而已。也因此，Commit 拆出來的文件会直接放在暂存区。

**hard 模式**

在这个模式下，不管是工作目录以及暂存区的文件都会丟掉。

**技巧：**
 只要记住执行 soft 模式后（回到 stage 暂存区状态），如果再次将原来的文件添加到仓库的话，需要 git commit **一个命令**就可以了。而 mixed 模式（回到 workspace 状态）需要执行 git add 和 git commit **两个命令**。对于 hard 模式来说是一种硬恢复，导致部分数据丢失，尽量不要用(可以使用 git reflog 来恢复)。

你只要记住些不同的模式，将会决定「Commit 拆出来的那些文件何去何从」，让我再用另一个表格来解释：

| 模式            | mixed 模式（预设） | soft 模式 | hard 模式 |
|:-------------:|:------------:|:-------:|:-------:|
| Commit 拆出来的文件 | 丟回工作目录       | 丟回暂存区   | 直接丟掉    |

# 分支（Branch）管理

## 分支（Branch）是什么？

分支的概念就有点像「分身术」，当你做出一只新的分身（分支），这个分身会去执行任务或是打倒敌人，如果执行失败了，最多就是那个分身消失，就再做一只新的分身就行了，本体不会因此受到影响。

## 为什么要使用分支？

在开发的过程中，一路往前 Commit 也没什么问题，但当开始越来越多同伴一起在同一个专案工作的时候，可能就不能这么随兴的想 Commit 就 Commit，这时候分支就很好用。例如想要增加新功能，或是修正 Bug，或是想实验看看某些新的做法，都可以另外做一个分支来进行，待做完确认没问题之后再合并回来，不会影响正在运行的产品线。

在多人团队共同开发的时候，甚至也可引入像 Git Flow / GitHub Flow / GitLab Flow 之类的开发流程，让同一个团队的人都可以用相同的方式进行开发，减少不必要的沟通成本。

## 分支的使用

分支就是一条独立的时间线，既有分支，必有主干，正如一棵树谈到树枝，必有树干一样的道理。我们先前对`git` 的全部操作默认都是在主干上进行的，这个主干也是一种特殊的分支，名为 `master` 分支。

无论是穿越历史还是撤销更改,我们都或多或少接触过时间线，`git` 管理的版本串在一起就组成了这个时间线，其中 `master` 分支是当前分支，`HEAD` 指向 `master` ，因此 `HEAD`  相当于指向了最新的版本。

![git-commit.gif](https://i.loli.net/2021/03/28/jY1qtNwG8SIK53k.gif)

基于分支上的操作，每一次 `commit` 都会提交一个新版本，并且新的 `commit` 指向原来的 `commit`，这来最新的 `commit` 就可以往前找,直到找到最初的 `commit`。这就是 `git` 的时间线.

在 Git 使用分支很简单，只要使用 `git branch` 命令就行了：

```bash
$ git branch
* master
```

如果 `git branch` 后面没接任何参数，它会打印出目前在这个方案有哪些分支。Git 预设会帮你设定一个名为 `master` 的分支，前面的星号 `*` 表示现在正在这个分支上。

### 新增分支

要增加一个分支，就是在执行 ` git branch` 指令的時候，在后面加上想要的分支的名字：

```bash
$ git branch cat
```

这样就新增了一个 `cat` 分支，再检查一下：

```bash
$ git branch  
  cat
* master
```

的确是多了一个分支，但现在分支还是在 `master` 上。

### 修改分支

如果你觉得名字不好听，你可以随时修改分支的名字，且不会有任何影响，比如我想把 `cat` 分支改成 `dog` 分支，使用 `-m` 参数：

```bash
$ git branch -m cat dog
```

看一下现在的分支情况：

```bash
$ git branch
  dog
* master
```

### 删除分支

检查一下目前的分支：

```bash
$ git branch
  dog
* master
```

如果你不想要 `dog` 分支了，使用 `-d` 参数来删除分支：

```bash
$ git branch -d dog
Deleted branch dog (was 11f7dd8).
$ git branch
* master
```

这样，`dog` 分支就被删除了

### 切换分支

我们还是先新建 `cat` 分支

```bash
$ git branch cat
$ git branch
  cat
* master
```

如果要切换到 `cat` 分支，只需使用 `git checkout <branch name>` 命令即可：

```bash
$ git checkout cat
Switched to branch 'cat'
```

查看分支状态：

```bash
$ git branch
* cat
  master
```

前面的那个星号已经移到 `cat` 分支上了。

其实，你也可以加上 `-b` 参数，可以直接创建新分支并切换过去，若是已有的分支，则会直接切换过去:

```bash
$ git checkout -b dog # 新建dog分支并切换到dog分支
Switched to a new branch 'dog'
$ git branch
  cat
* dog
  master
```

搞定！

## 进一步理解分支

你可以把分支想像成一张贴纸，它是贴在某一个 Commit 上面，像这样：

![~_0YW5TBBAGOWE5R_5_UE1V.png](https://i.loli.net/2021/03/28/au3LDxJiM5YkB4q.png)

当你做了一次新的 Commit 之后，这个新的 Commit 会指向它的前一个 Commit：

![KQ5___HH4_G95B@MKYSTMY9.png](https://i.loli.net/2021/03/28/pRA1hkQVfZTEISL.png)

而接下来「目前的分支」，也就是 HEAD 所指的这个分支，会跟着贴到刚刚做的那个 Commit 上，同时 HEAD 也跟着前进：

![4KG___P3TYT~YR5G_~8V6_0.png](https://i.loli.net/2021/03/28/UY2NWgT6jzcyxQs.png)

当你通过命令 `git branch cat` 创建了一个新的分支，就会像下面这样：

![1@LXZ~_I@3YSWT__S_0_XI5.png](https://i.loli.net/2021/03/28/RLkNtTK2Im1ry9x.png)

cat 和 master 在同一个地方。

当你执行 `git checkout cat` 指令切换到 `cat` 分支，那么，HEAD 便会换成指向 `cat` 分支，表示它是「目前的分支」：

![_EA@_`89_IGFSCQ_UOV2PM8.png](https://i.loli.net/2021/03/28/BRiqOxNw19VPvMD.png)

假如你又做了一次新的 Commit，这个新的 Commit 会指向前一次 Commit，然后， cat 分支会指向最新的那个 Commit 上了，当然 HEAD 也是跟着去：

![E4EAFA`_1LB5BYW0_LFY_7R.png](https://i.loli.net/2021/03/28/IUvh5tpzCZjiusr.png)

 Git 的分支大概就是这么一回事。

## 合并分支

现在我们删除其他没用的分支，留下 `master` 分支，并创建 `dev` 分支：

```bash
$ git checkout master # 切换到 master 分支
Switched to branch 'master'
$ git branch -d cat dog # 删除分支
Deleted branch cat (was 11f7dd8).
Deleted branch dog (was 11f7dd8).
$ git checkout -b dev
Switched to a new branch 'dev'
$ git branch
* dev
  master
```

现在，我们就可以在 `dev `分支上正常提交，比如对 `a.txt` 做个修改，加上一行：

```
Life is short, you need Python.
```

提交：

```bash
$ git add a.txt 
$ git commit -m "branch test"
[dev 9063364] branch test
 1 file changed, 2 insertions(+), 1 deletion(-)
```

现在，`dev` 分支的工作完成，我们就可以切换回 `master` 分支：

```bash
$ git checkout master
Switched to branch 'master'
```

切换回 `master` 分支后，再查看一个 `a.txt` 文件，会发现没有刚刚新添加的句子！因为那个提交是在 `dev` 分支上，而 `master` 分支此刻的提交点并没有变。
现在，我们把 `dev` 分支的工作成果合并到 `master` 分支上：

```bash
$ git merge dev # 将 dev 分支 合并到 master 分支
Updating 11f7dd8..8fb2f3a
Fast-forward
 a.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```

`git merge` 命令用于合并指定分支到当前分支。合并后，再查看 `a.txt` 的内容，就可以看到，和 `dev` 分支的最新提交是完全一样的。

> git rebase 与 git merge的区别
> 
> git merge是会产生一个树状的历史，如果我们输入git log — all — decorate — oneline —  graph的话，我们可能会看到一个有很多分支的树状结构，但是如果我们用git  rebase，就不再是树状的结构，git会利用其自身的算法，形成一个线性的历史。git rebase的好处可以参看 [*这篇文章*](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)。

# 共同协作 - 使用 GitHub

## GitHub 是什么？

在开始介绍 [GitHub](https://github.com/) 之前，请记得它的 G 跟 H 是大写，其它字母小写。它是一个商业网站，是目前全球最大的 Git Server。GitHub 上有很多开源（Open Source）项目，有很多开源的组织在上面贡献代码，例如 Mozilla，LinuxFoundation，Apache等等。

![K_G6__~AW_Z04__@WZVA089.png](https://i.loli.net/2021/03/26/gw9YbHpRcLatMOJ.png)
学生还可以获得 GitHub Education 提供的 [Student Developer Pack](https://education.github.com/pack) 。

若你还没有 GitHub 账号，请先去 [GitHub](https://github.com/) 注册账号吧~

> **Git 与 GitHub 的区别**
> 
> Git 是版本控制系统，GitHub 是在线的基于 Git 的代码托管平台。

**远程仓库：**
**远程仓库**其实并不复杂，实际上只是**本地电脑**上的本地仓库在另一台**远程电脑**的备份而已。
相对本地仓库来说**远程电脑上的版本库**自然就是**远程仓库**，远程仓库使得我们的版本库更加安全，毕竟远程电脑可不是一般的电脑，出错的概率比我们平时工作所使用的电脑概率要小得多，这样一来即使不小心丢失了本地仓库的全部数据,只要远程仓库没有丢失，那我们就可以通过远程仓库重新取回最新数据！
还有一点，远程仓库让**代码社交化**，因为大家有了**一致途径**来访问远程仓库，团队也好或者陌生人也罢，只有你愿意，他们就可以获取远程仓库的最新代码并参与开发，这也是 `GitHub` 的一大亮点！

**远程分支：**
当前你正在工作的电脑上存储的是**本地仓库**，如果没有**远程仓库**的支持，只能一个人鼓捣，别人无法共享你的工作成果，现在加入了团队开发流程，自然不再一个人独自开发，需要和团队其他人协同开发，共享开发成果。
所以本地仓库必然保存着远程仓库的基本信息，只有区分好**自己的工作成果**和**公共成果**,才能不乱套，又能做到信息及时共享。
实际上，在项目初期刚刚拷贝远程仓库(`git clone`)时，`git` 已经默认在本地仓库创建一个远程分支(`origin/master`)，本地修改提交首先都是在本地仓库完成的,比如 `git add`,`git commit` 等命令，如果需要发布你的工作成果，那么就需要使用 `git push origin <branch>` 命令推送到远程仓库，这里的 `origin` 指的就是远程仓库名称(因为最初大家都是先从远程仓库克隆下来的，所以远程仓库存储的项目相当于原始项目,故而叫`origin`)。

## 在 Github 上新建 Repository

要上文件案到 GitHub，需要有 repository，这里我新建 repository 来进行演示。请先在 GitHub 网站的右上角点选「+」号，并选择「New repository」：

![UGVMLR_I488G@EW4IU_F8GP.png](https://i.loli.net/2021/03/28/QE2oXkdxgGwuPJs.png)

然后填写仓库名字，Repository name 可填写任意名称，只要不重复即可：

![_C`V0FBK__3_OB9W_PKP11D.png](https://i.loli.net/2021/04/05/hnisJZGNVxQdayC.png)

同时勾选上 `Add a README file` 。
点击「Create repository」即可新增一新的 Repository。

这个`README.md` 是 `GitHub` 的预设说明页面， `.md` 表示它是一个 `Markdown` 格式，`Markdown` 语法可以很轻松的把纯文字格式转换成HTML 的网页格式，如果这是你第一次接触这个语法，非常推荐花一点时间学习它。

接下来，会看到这样的界面：

![5H___J19VN6_DTUM5TNYBY5.png](https://i.loli.net/2021/04/05/IYD8oJetbzlajZv.png)

## Clone：克隆仓库到本地

当你有了仓库之后，我们就可以将仓库(不一定得是你自己的仓库，别人的也可以) `clone` 到我们的电脑上。

使用 `git clone <URL>` 命令将仓库下载（克隆）到当前目录中，URL 在哪看呢， 

![BV_5@G~9NE46XU0YK_1Z_1F.png](https://i.loli.net/2021/04/05/vyIdgWb3Lsx2mcE.png)

细心的你会发现，就是当前仓库的 url 地址 + .git 组成的。

现在我们将这个仓库克隆到我们的电脑上，桌面上右键 -> Git Bash Here，输入命令：

```bash
$ git clone https://github.com/turing0/myrepo.git
Cloning into 'myrepo'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

桌面上就多了一个名为 `myrepo` 的文件夹，到这里就克隆好仓库了。

我们 cd 到文件夹里去：

```bash
$ cd myrepo/
```

你可以看看 status、log 等，使用`git remote` 或 `git remote -v` 查看远程仓库信息：

```bash
# 查看远程仓库名称
$ git remote
origin

# 查看远程仓库详情 : 拉取和推送链接
$ git remote -v
origin  https://github.com/turing0/myrepo.git (fetch)
origin  https://github.com/turing0/myrepo.git (push)
```

## Push 推送更新

现在，假如我在这里更改了 `readme.md` 文件，打开它，添加：尝试 git push，然后保存。

使用 `git push origin <branch>` 命令将代码上传到远程存储库。 
本地仓库和远程仓库的分支理论上应该一一对应，本地仓库的主干分支叫做 `main` ，而远程仓库也有相应的分支叫做 `main` ，这种映射关系是使用 `git clone` 命令时默认生成的，也是推荐的做法。

一般来说，本地仓库的分支推送到远程仓库指的就是推送到远程仓库同名的分支上，例如 `git push origin main` 意思是: 推将本地仓库的 `main` 分支推送到远程仓库的 `master` 分支。

```bash
# Make your changes to the codebase
# ...

# Stage all of your changes
$ git add .

# Make the commit
$ git commit -m "update readme file"
[main f9e634d] update readme file
 1 file changed, 3 insertions(+), 1 deletion(-)

# Push to GitHub (assuming the master branch)
$ git push origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 266 bytes | 266.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/turing0/myrepo.git
   a60d93f..f9e634d  main -> main
```

*注意: 你也可以把其他分支（不一定得是 `main`）推送到 GitHub上。*

![A_3K1_~A_LK_RD0WF__T7_Q.png](https://i.loli.net/2021/04/05/LDyPvbAirujMESx.png)

刷新仓库页面，会看到我们的修改已经显示出来，文件名旁边的字就是我们最近一次commit的内容。

## Pull 下载更新

请注意，团队多人协作开发时，大家都会定期或不定期往 `main` 或 `dev` 等分支上推送各自的更改，克隆下来的仓库将不会自动收到对本地项目所做的更改，相应的我们就需要下载别人的最新工作成果。如果 GitHub 上的项目已添加了新的提交， 为了将更新拉入本地仓库，使用 `git pull` 并提供远程和分支名称以从中拉出更新（例如`git pull origin master`将对远程 `master` 分支的最新更改下拉到当前分支中）。

现在模拟其他伙伴正在往 `master` 分支上推送更改，最好在另一个电脑另一个账户，当然模拟的话也可以是同一个电脑下其他目录，或者最简单的方式，直接登录 `github` 更改 `main` 分支上某个文件内容，简单起见，我们采用最后一种方式。

![W24BGY__ZSI9Q5ZJ_DGKT_E.png](https://i.loli.net/2021/04/05/cAY9tGKpRqNV5XH.png)

在网页上创建新文件：

![_1YORWZFPYZT_R@__~RF_76.png](https://i.loli.net/2021/04/05/ynzSNom7pOPH3De.png)

填写 commit 信息：

![OY_K__X__P4_DPG_B___4G7.png](https://i.loli.net/2021/04/05/NHDXtwnVqgdWiru.png)

你也可以默认，直接点击 Commit new file。

现在我们想要下载其他人的最新工作成果，只需使用 `git pull` 命令即可。跟 `Push` 指令相反，`Pull` 指令是拉取远程更新。

```bash
# 拉取最新版本
$ git pull
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 649 bytes | 81.00 KiB/s, done.
From https://github.com/turing0/myrepo
   f9e634d..d0c2b8b  main       -> origin/main
Updating f9e634d..d0c2b8b
Fast-forward
 a.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 a.txt
```

> git pull 和 git fetch 有点类似，这两个都是针对 remote repo 的一些操作，但是其实是有区别的，git pull 可以理解为融合了 fetch 和 merge 的两个操作。fetch，顾名思义，就是从服务器上把数据拿回来，但是注意，此时的数据很可能是已经和本地的 git  repo 不一样了，想象一个团队环境，你 push 了一个代码，可能一会其他团队成员又push 了一个，所以你的本地库可能和远程库有不同，所以这个时候git fetch一下，就紧接着要 merge 一下，把自己 master 和远程的 master 融合一下，这样就更好。
> 
> 但是 git pull 的情况就是直接下载远程 repo 并且 update 本地的库，很有可能本地有未保存的部分，git  pull 之后这部分就被 replace 了，而且无迹可查，所以其实更加稳健的方法是使用 git fetch 和 git  merge 共同操作来解决远程库在本地更新的问题。
> 
> 如果对于这两者还是有不明白可以参看 [这篇文章](https://blog.csdn.net/weixin_43670802/article/details/105581652?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param)。

## 解决冲突

当其他团队成员 clone 仓库之后，要在 `dev` 分支上开发，就必须创建远程 `origin` 的 `dev` 分支到本地，于是他用这个命令创建本地 `dev` 分支：

```bash
$ git checkout -b dev origin/dev
```

现在，他可以在 `dev` 上继续修改，然后，时不时地把 `dev` 分支 `push` 到远程。

假设有个 `index.js` 文件，团队其他成员添加了一个函数：

```js
function add(x, y) {
  return x + y;
}
```

保存并提交：

```bash
$ git add index.js

$ git commit -m "Implement add function"
[dev 7a5e5dd] add index.js
 1 file changed, 1 insertion(+)
 create mode 100644 index.js

$ git push origin dev
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 308 bytes | 308.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:turing0/git_test.git
   f52c633..7a5e5dd  dev -> dev
```

当团队其他成员已向 `origin/dev` 分支推送了他的提交，而碰巧你也对同样的文件作了修改，假如在 `index.js` 中添加一个叫 `multiply` 的函数：

```js
function multiply(x, y) {
  return x * y;
}
```

并试图推送：

```bash
$ git add index.js

$ git commit -m "Implement multiply function"
[dev 7bd91f1] add index.js
 1 file changed, 1 insertion(+)
 create mode 100644 index.js

$ git push origin dev
To github.com:turing0/git_test.git
 ! [rejected]        dev -> dev (non-fast-forward)
error: failed to push some refs to 'git@github.com:turing0/git_test.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

推送失败，因为其他人的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git 已经提示我们，先用 `git pull` 把最新的提交从 `origin/dev` 抓下来，然后，在本地合并，解决冲突，再推送：

```bash
$ git pull
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
```

`git pull` 也失败了，原因是没有指定本地 `dev` 分支与远程 `origin/dev` 分支的链接，根据提示，设置 `dev` 和 `origin/dev` 的链接：

```bash
$ git branch --set-upstream-to=origin/dev dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
```

再次 pull：

```bash
$ git pull
Auto-merging b.txt
CONFLICT (add/add): Merge conflict in index.js
Automatic merge failed; fix conflicts and then commit the result.
```

 `git pull` 成功，提示 `b.txt` 在合并时发生冲突，请处理冲突然后提交。

我们查看 `index.js` 的内容，会发现这样的内容（在命令行中用 cat 查看）：

```
<<<<<<< HEAD
function multiply(x, y) {
  return x * y;
=======
function add(x, y) {
  return x + y;
>>>>>>> main
}
```

<<<<<<< HEAD 部分到 ======= 之间的内容是当前分支下此文件的内容（Current Change），======= 到 >>>>>>> main 之间的内容是其他人修改的内容（Incoming Change），根据需求改成你希望的样子，这里的情况肯定想保留两者，经过修正，将 `index.js` 改为如下：

```js
function add(x, y) {
  return x + y;
}

function multiply(x, y) {
  return x * y;
}
```

然后提交我们用于处理冲突的 commit，再push：

```bash
$ git add .
$ git commit -m "fix index.js conflict"
$ git push origin dev
```

冲突处理完成。

## PullRequest（PR）

"Pull Request 是一种通知机制。你修改了他人的代码，将你的修改通知原来的作者，希望他合并你的修改，这就是 Pull Request。"

在 GitHub 上有个有趣的机制：

1. 先复制（Fork）一份原作的专案到你自己的 GitHub 帐号底下。
2. 为这个复制回来的专案已经在你自己的 GitHub 帐号下，所以你就有完整的权限，想怎么改就怎么改。
3. 改完后，先推回（Push）你自己帐号的仓库。
4. 然后发个通知，让原作者知道你有帮忙做了一些事情，请他看一下。 
5. 原作者看完后说「我觉得可以」，然后就决定把你做的这些修改合并（Merge）到他的仓库里。

其中，第 4 步的那个「通知」，就是发一个请原作来拉回去（Pull）的请求（Request），称之 Pull Request，简称 PR。

更多请看：https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests

> Fork 这个字在这边翻译成「复制」并不是这个字的原意，Fork 的中文翻译是「分叉」、「叉子」，在技术圈来说这个词使用的情境是「原作的做的不够好，其它人觉得可以做得更好或是想加入一些个人喜好的功能而修改出另外的版本」，不过为了让大家比较容易理解，这里还是会使用「复制」做为 Fork 的翻译。

# Git 使用速查

![_5PSF4EOS8R_J_@_CXSCH~L.png](https://i.loli.net/2021/04/05/lV6dQqRSPKugmL3.png)

# References

关于 Git 的相关知识也可以看以下的视频：
https://youtu.be/FyAAIHHClqI

猴子都能懂的 GIT 入门：https://backlog.com/git-tutorial/cn/

StackOverflow 上整理的一个资料大合集：https://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide

 Visual and interactive way to learn Git  on the web：https://git.mo.mk/

Learn Git Branching：https://learngitbranching.js.org/index.html

Pro Git - http://git-scm.com/book    https://git-scm.com/book/zh/v2
Pro Git 简体中文版 - http://iissnan.com/progit/

[Git权威指南 | 国内一位大牛写的介绍 Git 用法的开源书籍，很详实](http://www.worldhello.net/gotgit/index.html)

[Git tutorial — A Beginner’s Guide to the most Frequently used Git Commands](https://codeburst.io/git-tutorial-a-beginners-guide-to-most-frequently-used-git-commands-2ab92bd22787)

http://marklodato.github.io/visual-git-guide/index-zh-cn.html