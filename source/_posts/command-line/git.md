---
title: Git命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Git,Tool]
---
Git 是一个分布式版本控制系统，用于跟踪在软件开发过程中对文件的修改。它能够让你回溯到之前的版本，协作开发项目，并管理不同的开发分支。以下是一些常用的 Git 命令，可以帮助你进行日常的版本控制操作：

### 基础命令

- **初始化仓库**
  - `git init`：在一个新的或现有的目录中创建一个新的 Git 仓库。

- **克隆仓库**
  - `git clone [url]`：克隆一个远程仓库到本地。

### 配置命令

- **设置用户名和邮箱**
  - `git config --global user.name "Your Name"`：设置全局用户名。
  - `git config --global user.email "your.email@example.com"`：设置全局邮箱地址。

- **查看配置**
  - `git config --list`：查看当前所有的配置。

### 工作区与暂存区

- **查看状态**
  - `git status`：查看工作区的状态，了解哪些文件被修改过。

- **添加文件到暂存区**
  - `git add [file]`：将文件添加到暂存区。
  - `git add .`：将所有更改过的文件添加到暂存区。

- **提交更改**
  - `git commit -m "commit message"`：将暂存区的所有更改提交到仓库。
  - `git commit -am "commit message"`：直接提交所有已经跟踪过的文件，跳过暂存区。

### 分支管理

- **查看分支**
  - `git branch`：列出所有本地分支。
  - `git branch -r`：列出所有远程分支。
  - `git branch -a`：列出所有本地和远程分支。

- **创建分支**
  - `git branch [branch-name]`：创建新分支。
  - `git checkout -b [branch-name]`：创建并切换到新分支。

- **切换分支**
  - `git checkout [branch-name]`：切换到指定的分支。
  - `git switch [branch-name]`：（Git 2.23+）切换到指定的分支。

- **合并分支**
  - `git merge [branch-name]`：将指定分支合并到当前分支。

- **删除分支**
  - `git branch -d [branch-name]`：删除指定的本地分支。
  - `git push origin --delete [branch-name]`：删除远程分支。

### 远程仓库

- **查看远程仓库**
  - `git remote -v`：查看当前配置的远程仓库信息。

- **添加远程仓库**
  - `git remote add [shortname] [url]`：添加一个新的远程仓库。

- **拉取更新**
  - `git pull [remote] [branch]`：从远程仓库拉取最新的更改并合并到当前分支。

- **推送更改**
  - `git push [remote] [branch]`：将本地分支的更改推送到远程仓库。
  - `git push --set-upstream [remote] [branch]`：首次推送时设置上游分支。

### 版本回退

- **查看提交历史**
  - `git log`：查看提交历史记录。
  - `git log --oneline`：简要地查看提交历史记录。

- **撤销更改**
  - `git reset [commit]`：将当前分支的 HEAD 指针重置到指定的提交。
  - `git revert [commit]`：撤销指定的提交，创建一个新的提交来撤销更改。

- **恢复工作区文件**
  - `git checkout -- [file]`：放弃工作区的更改，恢复到最近一次提交的状态。

### 标签管理

- **查看标签**
  - `git tag`：列出所有标签。

- **创建标签**
  - `git tag [tagname]`：创建轻量级标签。
  - `git tag -a [tagname] -m "tag message"`：创建带注释的标签。

- **推送标签**
  - `git push origin [tagname]`：推送单个标签到远程仓库。
  - `git push origin --tags`：推送所有标签到远程仓库。

- **删除标签**
  - `git tag -d [tagname]`：删除本地标签。
  - `git push origin :refs/tags/[tagname]`：删除远程标签。

这些命令是 Git 中最常用的，掌握它们可以帮助你高效地进行版本控制。