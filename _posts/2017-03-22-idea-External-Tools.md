---
layout: post
title:  在 IDEA 中添加使用外部工具打开所选文件
categories: 工具
tags:  IDEA
author: lassove
---

* content
{:toc}

很多时候，我们需要使用一些外部程序打开 `IDEA` 项目里的某些文件。比如使用` ps` 打开图片修图，或者像我一样使用 `typora` 来编辑 `markdown` 文件。下面就来分享如果配置`IDEA` ，可以直接在文件上右键，选择·`External Tools` --> 你的工具 打开选中文件。






## 痛点

最近开始重新写博客，使用的是` github page` 功能，为了方便，直接用` IDEA` 来管理` page` 项目，只需要创建 `markdown` 文件，写写写，然后 `commit&push` 即可。但是使用 `IDEA` 自带的 `markdown` 编辑器书写体验很不好，多番比较之后，在`windows`下选择了 `typora` 作为` markdown` 编辑器。于是就萌生了如果在 `IDEA` 里集成 `typora` 使其可以直接打开创建的 `markdown` 文件编辑。几番摸索，终于差不多达到我想要的效果。

## 操作步骤
1. 在 `IDEA` 点击 `setting` 在 `tools`选项下选择 `External Tools`。
2. 在右侧点击 `+` ，弹出新建`External Tools` 框。
3. `Name` 和 `Description` 随便填写。
4. 关键是`Program` ，这里需要填写你想要使用的外部程序的路径，或者你可以配置环境变量后直接填写程序名。
5. 在`Parameters` 里，填写 `$FilePath$`。
6. ​然后 `Apply` 确认。
7. 回到`Project` 下面，选中你要打开的文件，右键，就会发现多出一个`External Tools`菜单，指向后会弹出子菜单就是你之前配置的外部程序的`name`，点击即可利用外部工具打开该文件。

## 感悟

大概看了一下，`External Tools`其实可以帮我们做更多的事情，可以说是`IDEA` 自带功能的一个自定义的扩展功能。希望大家有什么好的玩法，不要吝啬，分享出来。