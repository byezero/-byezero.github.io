---
layout: post
title:  $TITLE$
categories: JavaScript
tags:  $TAGS$
author: lassove
---

* content
{:toc}

本节主要讲述最常见的一些操作,包括初始化现有项目,暂存,提交等.



## 创建版本库

版本库,英文名叫`repository`,你可以把它理解为一个目录,这个目录里的所有文件都可以被git管理起来,每个文件的修改,删除,git都能够跟踪记录,以便任何时候都可以追踪历史,或者在某个时候进行回退.

创建版本库的命令非常简单,打开终端,输入以下命令:

```bash
mkdir git-demo
cd git-demo
git init
```
不出意外的话,你应该得到如下输出:
```bash
Initialized empty Git repository in your-path/git-demo/.git/
```
**命令`git init` 作用: 把当前目录变成Git可以管理的仓库.**
## 暂存文件到git
此时,git-demo 文件夹即受git进行版本控制,现在我们来添加一些文件.

```bash
echo "This is a html" > index.html
```
我们通过`git status`来看看当前版本库的状态:
```bash
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        index.html

nothing added to commit but untracked files present (use "git add" to track)
```
不难看出,`git`给出了当前的状态,有未跟踪的文件出现.在版本库里,文件有几种状态:
- 未跟踪
- 已跟踪,暂存
- 已经提交
  根据上面给出的提示,我们应该使用`git add <file>`命令来跟踪文件:
```bash
git add index.html
```
没有输出,不要紧张,Unix设计哲学告诉我们**没有消息就是好消息**,我们不妨再来看看状态:
```bash
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   index.html

```
此时,文件就进入暂存区,你可以理解为git会把你对文件的改动暂存起来,等待你的提交.
**命令`git status` 作用: 查看当前仓库的文件状态.**
**命令`git add <file>/<path>` 作用: 将指定的文件/路径 进行暂存**
特别的:
命令 `git add .`会将当前目录所有文件暂存.

> 注意:git命令体系里,给出的提示 参数用 <> 包裹的表示必须, [] 包裹的表示可选.

## 提交

现在我们将我们的暂存区进行一次提交:
```bash
$ git commit -m "first commit"
[master (root-commit) 1a48a72] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 index.html
```
简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。
现在再来看看版本库的状态:
```bash
$ git status
On branch master
nothing to commit, working tree clean
```
可以看出,当前版本库没有可以提交的,整个工作区是干净的.

现在我们修改一下`index.html`,看看会有什么变化:
```bash
vim index.html
```

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```
可以明显看出,你的文件被修改了.现在我们来一次提交:
```bash
 git commit -m "add html tag"
On branch master
Changes not staged for commit:
        modified:   index.html

no changes added to commit
```
WHAT?! 不能够提交,原因是`Changes not staged for commit`.
```bash
$ git add index.html
$ git commit -m "add html tag"
[master a824e23] add html tag
 1 file changed, 2 insertions(+)
```
切记,命令操作时,修改文件后一定要用`git add <file>`命令将修改移至暂存区才可提交.
现在我们再来一次修改:
OK,老板大发善心,放你一个月长假,你环球旅游三十日后前来上班,先看看工作区状态:
```bash
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```
哦豁,文件被修改了,但是你已经忘记了修改了什么,别怕,`git diff`来帮忙:
```bash
$ git diff
diff --git a/index.html b/index.html
index fc06035..42aaf0a 100644
--- a/index.html
+++ b/index.html
@@ -1,3 +1,5 @@
 <html>
+       <body>
 this is a html
+       </body>
 </html>
```

**命令`git diif` 作用: 查看当前仓库文件的修改信息.**

同样,我们确认的修改需要提交到本地版本库,提交修改和提交新文件一样分两步:
1. `git add <file>`命令将修改暂存.
2. `git commit -m '提交信息'`进行一次提交.





