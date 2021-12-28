git 快速入门
================================

Git 是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

git 下载
++++++++++++++++

官网：https://git-scm.com/

git 基本使用
++++++++++++++++
git 使用前必须配置::

    git config --global user.name 'username'
    git config --global user.email 'mail@mail.com'

创建本地仓库::

    git init
    git add --all
    git commit -m "first commit"
    git branch -M main
    git status     # 查看状态

管理远程仓库:

1. 生成rsa

::

    ssh-keygen -t rsa

2. 添加公钥

3. 创建远程仓库

4. 管理远程仓库
::

    git remote add docs https://github.com/LDragon200/Knowledge.git
    git push -u docs main



git 基本概念
++++++++++++++++


git 维护操作
++++++++++++++++

