---
title: Git Bash 入门手册
tags:
  - git
  - Git Bash
---

混 Github 同性社区 git 是必备的。公司代码协作也从 SVN 迁移到 git ，趁机把日常用到的一些简单命令做个梳理，以备脑短路时查阅。本文会持续更正更新...

<!-- more -->

## 1. Git Bash 环境配置


### 1.1. 安装 Git Bash

  - windows平台下载安装 [<https://git-for-windows.github.io/>]
  - `git --help git` git帮助文档


### 1.2. 设置提交者识别信息

  - 设置全局Name和Email地址

    > git config --global user.name "Your Name" git config --global user.email "email@example.com"

  - 也可以给指定项目单独设置信息

    > git config user.name "Your Name" git config user.email "email@example.com" git config --list 查看配置信息


### 1.3. 创建工作区域

  - `mkdir HtmlCode` 创建工作区
  - `cd HtmlCode` 进入文件夹
  - `pwd` 显示当前目录


### 1.4. 创建本地仓库

  - `git init` 在工作区创建git管理仓库 *或者clone一个远程库*
  - `git clone [url] D://HtmlCode` 克隆远程版本库并更名


## 2. git 基本操作

### 2.1. 一次简单的提交

  本地仓库由 git 维护的三棵"树"组成。第一个是你的「工作目录」，它持有实际文件；第二个是「缓存区（Index）」，临时保存你的改动；最后是「HEAD」，指向你最近一次提交后的结果。

  - `git status` 查看当前仓库实时状态
  - `git diff` 查看变更内容
  - `git add .` 指明要追踪文件，把目标文件放入暂存区域
  - `git commit -m "说明话术"` 现在，你的改动已经提交到了 HEAD，但是还没到你的远端仓库
  - `git push` 推送到远程服务器


### 2.2. 查看提交记录

- `git log` 查看提交历史
- `git log --oneline`
- `git reflog` 查看命令历史，以便回到未来的版本


### 2.3.  清理untracked文件

  - `git clean -f` 删除所有 untracked 文件
  - `git clean -fd` 连同 untracked 目录一并删除 _建议删除前加上 -n 预览会删除哪些文件，以免误删_ `git clear -nfd`


### 2.4. 回退文件

  ![工作区、版本库、暂存区原理图](/article_images/D1_git-stage.png)

  - `git checkout -- <file1> <file2>` 此命令会使用 HEAD 中的最新内容替换掉你的工作目录中的文件。这个操作很危险，会清除工作区中未添加到暂存区的改动,已添加到缓存区的改动，以及新文件，都不受影响
  - `git checkout -f` 丢弃工作区、缓存区所有修改。清除commit之前的所有修改
  - `git checkout <commitID>` 干净的版本回退，将丢弃工作区、缓存区所有修改
  - `git checkout HEAD <file>` 从最新的版本替换工作区文件
  - `git reset --soft HEAD^` 从最新版本库回退到工作区
  - `git reset --soft <commitID>` 从最新版本库回退到工作区

    ```
    --soft – 缓存区和工作目录都不会被改变
    --mixed – 默认选项。缓存区和你指定的提交同步，但工作目录不受影响
    --hard – 缓存区和工作目录都同步到你指定的提交
    ```

  - `git reset <commit_id>` 在历史版本间回滚，消除commit信息，文件放回工作区
  - `git rm --cached <file1> <file2>` 直接从暂存区删除文件，工作区则不做出改变


## 3. 多分支操作

### 3.1 分支管理

- `git fetch –p` 更新分支列表
- `git branch` 查看当前分支，当前分支前面会标一个「*」
- `git branch -r` 查看远程分支
- `git branch -a` 查看所有分支
- `git branch -va` 查看所有分支+log
- `git branch <branch>` 创建分支
- `git checkout <branch>` 切换分支
- `git checkout -b <branch>` 创建+切换分支
- `git merge <branch>` 合并某分支到当前分支
- `git branch -D <branch>` 删除某分支


### 3.2. 查看远程分支

- `git fetch` 更新远程分支信息
- `git branch -r` 查看远程分支
- `git branch -ar` 查看本地+远程分支及最后一次log


#### 3.2.1. 从远程分支开新分支

  - `git checkout -b <localBranch> <remotes/origin/remoteBranch>` 远程分支映射到本地分支


#### 3.2.2. pull

  - `git pull origin <remoteBranch>:<localBranch>` 将远程某分支与指定的本地分支合并
  - `git pull origin <remoteBranch>` 将远程某分支与当前分支合并


#### 3.2.3. push

  - `git push <origin> <localBranch>:<remoteBranch>` 本地分支推送到远程分支，如果远程不存在此分支则会被新建
  - `git branch --set-upstream-to=origin/<branch>` 本地当前分支与远程分支建立追踪关系
  - `git branch -vv` 查看追踪关系
  - `git push <origin>` 如果当前分支与远程分支存在追踪关系，则可直接push到主机
  - `git push` 如果当前分支有且只有一个追踪分支，那么主机名亦可省略
  - `git push -u origin <branch>` 将本地分支推送到远程分支同时指定默认主机，之后不用加任何参数直接使用 `git push`

  - > git branch -D branch git push origin :remoteBranch

    推送时省略本地分支则会删除指定的远程的分支 *注意不要省略`:`前的空格


## 3. Work Flow

### 3.1. 紧急上线

  1. `git checkout -b bug_xxx remotes/origin/master` 从远程master分支创建bug_分支（切换分支时建议关闭VS）
  2. 本地开发-完成 （新资源通常需要包含进VS项目中）
  3. 无法获取时，请先保存本地代码 `git stash`
  4. `git pull origin master` 拉取最新代码到本地
  5. 将 `stash` 的代码 `git stash pop` 恢复到工作区
  6. `git add .` `git commit -m "话术"` commit 本次更改，不是自己更改的文件不要提交
  7. `git push -u origin bug_xxx` 推送本分支到远程作为一个远程新分支
  8. 发起「pull request」,将 _bug_xxx_ 合并到 _master_
  9. 合并时再次 review 对比代码确认下都是自己提交。如有冲突等，解决冲突后push&pullRequest，敦促版本管理员处理
  11. 测试无误删除服务器bug_xxx分支
  12. PS. 切换分支的时候建议关闭VS

## 3.21 HotFix

  0   接到在vNext上开发feature_1功能的任务
  1   将源代码当前分支切换到vNext上   Git checkout vNext
  2   拉取最新vNext分支 Git pull origin vNext
  3   从本地vNext上创建feature_1分支  Git branch vNext_featue_1 vNext
  4   切换到feature_1分支上 Git checkout vNext_feature_1
  5   本地完成开发，提交到feature_1分支   Git commit
  6   推送本地feature_1分支到服务器 Git push –u origin vNext_feature_1
  7   打开服务器网站，发起pull request请求
  8   选择从feature_1分支合并到vNext分支
  9   管理员审批拉取请求

  10  看到自己的拉取请求已完成
  11  删除远程feature_1分支 Git push origin :vNext_feature_1
  12  到部署网站上申请部署fvt测试
  13  协助测试完成fvt测试
  9->9.1  如果管理员发现合并冲突，拉取请求被拒绝
  10.1    切换到vNext分支  Git checkout vNext
  11.1    获取最新vNext信息 Git pull origin vNext
  12.1    切换到feature_1分支  Git checkout vNext_feature_1
  13.1    本地合并vNext和feature_1 Git merge vNext
  14.1    提交合并结果  Git commit
  15.1    重复6~13步骤
  13->13.2    如测试发现有bug， fvt测试不通过
  14.2    重复1~13步骤

### 解决 pullRequest 冲突

eg. vNext_promotion 合并到 vNext 时冲突

- 首先，你将需要确保 vNext_promotion 和 vNext 分支是最新的: git fetch origin git checkout -b vNext_promotion origin/vNext_promotion
- 接下来，将 vNext 中的更改合并到 vNext_promotion 中，并解决冲突: git checkout vNext_promotion git merge origin/vNext
- 然后，在生成和测试代码后，用最新的更改更新拉取请求: git push origin vNext_promotion 返回此处，以完成拉取请求git

[@咪醤](mailto:zzb0b0@126.com)
