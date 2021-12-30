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

在Git中有四个概念：「远程仓库、工作区、暂存区、版本库」。其中：「工作区、暂存区、版本库」都在本地。

远程仓库：
   远程仓库就是我们Git的服务器，用于存储已经管理团队的代码。

工作区：
    使用 `git init [目录]` 初始化的目录

暂存区：
    在.git目录下index文件(.git/index)，这就是「暂存区」，叫做stage或者index，index和我们的数据库的index类似，所以我们有时候也叫它为「索引」。

版本库：
    本地的仓库

git 命令操作图解
    可以参考这一篇文章：https://www.cnblogs.com/cb0327/p/5066685.html
    
    .. image:: /images/workflow.png


