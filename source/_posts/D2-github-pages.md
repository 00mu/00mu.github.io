---
title: GitHub pages 搭建记录
tags:
  - GitHub pages
  - git
---

大二的时候开始摆置WordPress搭建Blog，写的都是一些流水账，并没有坚持写来下，毕业后渐渐不再维护了。就是那时的摸索把玩对 Html + CSS 产生了兴趣，从此成了一名切图仔。现在算重拾乐趣，何况 GitHub 提供福利，无需域名服务器便可拥有个人站点。「GitHub pages」+「Hexo」搭建博客，用到的资料和步骤整理如下。

<!-- more -->

## 1. git 环境配置  - GitHub 与 git 关联

首先安装好 Git Bash ，按步骤将 git 与 GitHub 关联起来

### 1.1. 检查 SSH keys 设置

  > $ cd ~/. ssh

  检查本机的ssh密钥，提示 " No such file or directory " 则需要生成新的 SSH keys

### 1.2. 生成新的 SSH Key

  > $ ssh-keygen -t rsa -C "xxx@xxxmail.com"

  一路回车，看到下面的界面，就表明生成成功了

  ```bash
  The key fingerprint is:
  SHA256:deq65ahsK3kXY7xuTo5eIplsJLnKlwJTlHPcxb9v/GQ xxx@xxx.com
  The key's randomart image is:
  +---[RSA 2048]----+
  |   o . o.        |
  |  + o . .        |
  | . o     .. .    |
  |  ..     ..o     |
  | .o .  .S ..     |
  |o  = o  =..      |
  |... B...o+oo  E  |
  |.o +ooo*+=  +o   |
  |..o  =*BB... ..  |
  +----[SHA256]-----+
  ```

### 1.3. 将 SSH keys 添加到 GitHub

  根据上面窗口提示找到 id_rsa.pub 文件，内容复制到 GitHub.com > Personal settings > SSH keys (_New SSH key_)，保存即可。

### 1.4. 测试关联是否成功

  > $ ssh -T git@github.com

  对话输入 yes 后，提示如下界面就成功了

  ```
  Hi xx! You've successfully authenticated, but GitHub does not provide shell access.
  ```

### 1.5. 设置账号信息

  > $ git config --global user.name "your_name" $ git config --global user.email "your_email@youremail.com"

  > $ git config --list // 查看git配置信息



## 2. 博客系统用 HEXO
  [参照笑来老师的博客](http://xiaolai.li/2016/06/22/makecs-build-a-blog-with-hexo-on-github/#more)，有详细明了的步骤，非常好用，祝成功


## 3. 修改主题

  [NexT.Pisces下载](https://github.com/iissnan/hexo-theme-next)
  [NexT.Pisces使用文档](http://theme-next.iissnan.com/getting-started.html)


### 3.1. 一些调整

  - 添加「标签」页面
    [http://theme-next.iissnan.com/theme-settings.html#tags-page]

  - 侧边栏文章目录改成无序列表
    [https://github.com/iissnan/hexo-theme-next/issues/857]


### 3.2. 直接使用本站主题

  [NexT.Pisces-个人版](https://github.com/00mu/00mu.github.io/tree/source)，位于00mu.github.io库source分支下


## 4. 熟记几个命令

  - ` hexo generate ` 编译
  - ` hexo server ` 启动本地服务器，localhost:4000 可见
  - ` hexo deploy` 编译文件部署到 Github ，https://00mu.github.io/ 可见


## 其他

  另外介绍下 GitHub Pages 搭建静态页面，直接把资源push上即可

  [参见官方介绍](https://pages.github.com/)

  1. 创建一个与用户名一致的仓库，如 00mu.github.com 。
        一个 GitHub 账户只有一个，此仓库也将是你的主页地址
  2. 将仓库 clone 到本地
  3. 跟目录编辑 index.html ，此页面将作为主页
  4. push 到远程仓库
  5. 随后访你的主页即可呈现。
