title: GitHub pages 搭建记录
tags: git GitHub
---

<!-- more -->
## GitHub 与 git 关联

首先安装好 Git Bash ，按步骤将 git 与 GitHub 关联起来

1. 检查 SSH keys 设置

  > $ cd ~/. ssh

  检查本机的ssh密钥，提示 " No such file or directory " 则需要生成新的 SSH keys

2.  生成新的 SSH Key

  > $ ssh-keygen -t rsa -C "xxx@xxxmail.com"

  一路回车，看到下面的界面，就表明生成成功了

  ```
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

3.  将 SSH keys 添加到 GitHub

  根据上面窗口提示找到 id_rsa.pub 文件，内容复制到 GitHub.com > Personal settings > SSH keys (_New SSH key_)，保存即可。

4. 测试关联是否成功

  > $ ssh -T git@github.com

  对话输入 yes 后，提示如下界面就成功了

  ```
  Hi xx! You've successfully authenticated, but GitHub does not provide shell access.
  ```

5. 设置账号信息

  > $ git config --global user.name "your_name" $ git config --global user.email "your_email@youremail.com"

  > $ git config --list // 查看git配置信息

## 使用 GitHub Pages 搭建博客

[参见官方介绍](https://pages.github.com/)

1. 创建一个与用户名一致的仓库，如 00mu.github.com 。一个 GitHub 账户只有一个，此仓库也将是你的主页地址
2. 将仓库 clone 到本地
3. 跟目录编辑 index.html ，此页面将作为主页
4. push 到远程仓库
5. 随后访你的主页即可呈现。
