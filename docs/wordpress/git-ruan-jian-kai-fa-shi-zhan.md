---
layout: default
title: git软件开发实战
parent: wordpress
---

# 《git软件开发实战》读书笔记

## 目录

- [ch02](#ch02)
- [ch03](#ch03)
- [ch04](#ch04)
- [ch05](#ch05)
  - [5.3 add](#53-add)
    - [暂存范围](#暂存范围)
    - [2.部分暂存")2.部分暂存](#2部分暂存2部分暂存)
    - [3.交互式提交暂存](#3交互式提交暂存)
  - [5.6 高级主题](#56-高级主题)
- [ch06](#ch06)
  - [6.2 git diff](#62-git-diff)
- [ch08](#ch08)
- [ch09](#ch09)
  - [本章生于内容探讨可以适用于常规合并、变基和樱桃拣选的操作。处于简约性考虑，将借由“合并操作”这一通用名称来指代这些操作。](#本章生于内容探讨可以适用于常规合并变基和樱桃拣选的操作处于简约性考虑将借由合并操作这一通用名称来指代这些操作)
    - [ORIG\_HEAD](#ORIG_HEAD)
    - [引用日志](#引用日志)
  - [9.2 处理冲突](#92-处理冲突)
- [ch10](#ch10)
  - [10.1 Git属性文件](#101-Git属性文件)
    - [创建一个自定义过滤器](#创建一个自定义过滤器)
- [ch11](#ch11)
  - [11.1 git stash save 描述](#111-git-stash-save-描述)
  - [11.2.1 Git文件内容搜索](#1121-Git文件内容搜索)
  - [11.2.2 Git日志搜索](#1122-Git日志搜索)
  - [11.3.1 git archive master --format=zip --output=../myrepo.zip打包为zip不带.git](#1131-git-archive-master---formatzip---outputmyrepozip打包为zip不带git)
  - [11.3.2 git bundle create ../myrepo.bundle打包为bundle带有.git](#1132-git-bundle-create-myrepobundle打包为bundle带有git)
  - [11.4.3 notes](#1143-notes)
  - [11.5 高级主题](#115-高级主题)
    - [例11-1：将子目录分隔到单独仓库中git filter-branch -f --subdirectory-filter 目录名 -- --all](#例11-1将子目录分隔到单独仓库中git-filter-branch--f---subdirectory-filter-目录名------all)
    - [例11-2：从所有历史中删除一个文件](#例11-2从所有历史中删除一个文件)
- [ch13](#ch13)
  - [13.1 远端冲突](#131-远端冲突)
  - [13.2 公共托管站点](#132-公共托管站点)
    - [fork-and-pull模型](#fork-and-pull模型)

第十四章和第十五章太难，读不下去

# ch02

2.3.2 文件范围  
处理大型文件：

- 对于图标等较小二进制内容，直接存储
- 对于较大的文件：
  - 在构件仓库中存储它们，包括Artifactory和Nexus
  - 存储在单独的为其设计的Git仓库中，可使用对Git的扩展：
    - git-annex
    - git LFS

# ch03

3.1.1 远程仓库不会对内容进行面向用户的修改，比如解决合并冲突。

# ch04

4.1.1 许多全局选项都没什么意义

4.2.2 `git config --配置范围`

1. 系统：–system
2. 全局：–global
3. 本地：–local （默认）

4.2.4 设置行结束符

core.autocrlf=input会在提交时标准化为LF，适合Unix环境。

存在其他的配置设置有助于改进行结束符的处理方式

无法确保每个人都设置恰当的core.autocrlf值。不过可以用[.gitattributes](http://bj.apsonic-moto.cn/2021/04/27/git-ruan-jian-kai-fa-shi-zhan/#ch10 ".gitattributes")

4.4.4 创建参数化别名

“! f() {do some processing }; f”

# ch05

### 5.3 add

#### 暂存范围

#### 2.部分暂存")2.部分暂存

`git add -p <file>`中最有用的子命令是y和n，其他子命令都是用于对内容块进行批量操作或者围绕一组内容块进行导航的子命令。

#### 3.交互式提交暂存

### 5.6 高级主题

5.6.2 `git commit -t ~/.gitmessage --verbose --verbose`

# ch06

### 6.2 git diff

表6-1 简要选项的Git状态码

6.2.3 仅显示有差异的文件名称：`git diff --name-only`

6.2.4 在单词粒度上进行差异对比：`git diff --word-diff`

6.2.5 忽略非关键变更

1. 空白变更
2. 文件模式变更

6.2.7 可视化对比：`git difftool`

6.2.8 `diff file1 file2` 不同于 `git diff file1 file2`，后者是检查file1与暂存区的差异以及file2与暂存区的差异

# ch08

8.1.8 `HEAD^`表示HEAD的父提交，而`^A`表示非A，例如`git log B ^A`等同于`git log A..B`

# ch09

9.1.4 变基

`git rebase B [TOTAL]`将来自TOTAL的自从它偏离之后的差异增量序列附加到B

9.1.5 樱桃拣选

`git cherry-pick -Xtheirs B^..D`将拣选B,C,D

9.1.7 合并操作

### **本章生于内容探讨可以适用于常规合并、变基和樱桃拣选的操作。处于简约性考虑，将借由“合并操作”这一通用名称来指代这些操作。**

#### ORIG\_HEAD

当Git中发生合并操作时，ORIG\_HEAD会存储最后一次合并操作前的提交的SHA1值。

#### 引用日志

每个引用的引用日志都会记录他们随时间推移而变更的值

### 9.2 处理冲突

9.2.1 合并操作就是Git的状态。这意味着在开始这些操作时，Git会输入一个状态来拒绝变更上下文（例如切换分支）

9.2.2 变基通常涉及采用多个提交的差异增量在另一个分支上重新生成多个变更的历史。

9.2.5 解决选项和策略

Git支持为合并操作使用各种策略和选项。可以通过-s选项选择想要使用的策略，而-X选项会允许将参数传递到所选的策略。

`-s ours`：保留当前分支的所有内容并且不对任何内容进行重写。`-X ours`：仅在有冲突时保留当前内容。

# ch10

### 10.1 Git属性文件

Git具有尝试检测一个文件是否为二进制文件的内置算法，但无法被认为100%准确。

10.1.1 Git属性文件的作用

- 指定二进制文件
- 指定如何处理行结束
- 制定独特的筛选器来关联文件或文件类型，以便执行自定义操作

10.1.4 常见用例

#### 创建一个自定义过滤器

# ch11

### 11.1 `git stash save 描述`

### 11.2.1 Git文件内容搜索

`git grep -e 模式 提交的引用 -- 文件集合`

### 11.2.2 Git日志搜索

- `git log -S string`会搜索变更了string出现次数的提交
- `git log --pickaxe-regex -S string`等同于-S但用正则表达式作模式匹配
- `git log -G string`会搜索在其补丁中添加或移除了包含string的行的提交
- `git log -L`用于追踪文件中行的集合或一个函数的变更的选项

### 11.3.1 `git archive master --format=zip --output=../myrepo.zip`打包为zip不带.git

### 11.3.2 `git bundle create ../myrepo.bundle`打包为bundle带有.git

### 11.4.3 notes

`git notes add 提交的引用`为提交添加注释

`git log --show-notes=*`会显示所有命名空间中的注释

### 11.5 高级主题

11.5.2 rev-list可被用于限定所要针对其进行操作的用于filter-branch的一组内容

#### 例11-1：将子目录分隔到单独仓库中`git filter-branch -f --subdirectory-filter 目录名 -- --all`

#### 例11-2：从所有历史中删除一个文件

如果传递给filter-branch的shell命令的任何估算返回了一个非零退出状态，那么整个操作都将被终止。为了确保不会出现这种情况，需要`git rm --ignore-unmatched`选项。命令如下：

`git filter-branch --index-filter 'git rm --cached --ignore-unmatched 文件路径' 分支名`

# ch13

### 13.1 远端冲突

远端预期要作为你正在尝试推送的内容的祖先。即使你和另一个用户变更了完全不同的文件，你也会面临合并冲突。

pull命令的–merge选项可能更简单，因为在某些情况下仅需要一次合并。不过，它也会将合并提交带入历史中。–rebase选项可能需要更多的合并处理并且需要关注冲突解决，但它也会提供较为干净的历史。

### 13.2 公共托管站点

13.2.1 Git协作模型

#### fork-and-pull模型

