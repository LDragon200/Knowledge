termux
================
 Termux 是一款基于 Android 平台的开源 Linux 终端模拟器，使用 pkg(apt) 进行软件包的管理。 最重要的是，它无需 root 权限，因此，绝大多数 Android 都可以运行。

参考`官方 Wiki <https://wiki.termux.com/wiki/Main_Page>`_ 

基本步骤
################

1. 安装

2. 获取系统存储权限

    | 使用命令 ``termux-setup-storage`` 在弹出的窗口上授予访问存储空间的权限

3. 安装 ssh

    | turmux 使用 pkg 作为包管理器，使用命令 ``pkg install openssh`` 安装sshd

安装软件
################

使用命令 ``pkg [options] [package]`` 管理软件 

部署code-server
################
参考官方文档：https://github.com/coder/code-server/blob/main/docs/termux.md

https://coder.com/docs/code-server/latest/npm#nodejs-version

这里记录下大概的步骤和中间遇到的问题：

1. 安装 Debian::

    pkg update -y && pkg install wget curl proot tar -y && wget https://raw.githubusercontent.com/AndronixApp/AndronixOrigin/master/Installer/Debian/debian.sh -O debian.sh && chmod +x debian.sh && bash debian.sh

2. 安装必要插件::

    apt update
    apt upgrade -y
    apt-get install nano vim sudo curl wget git -y

3. 安装 nvm::

    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    或者
    wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

5. 设置nvm::

    export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm

    # 设置完成后确保 nvm 命令能够直接使用

6. nvm 下载 14.* 版本
7. 使用命令安装::

    测试安装(不会真正安装)::

        curl -fsSL https://code-server.dev/install.sh | sh -s -- --dry-run

    安装::

        curl -fsSL https://code-server.dev/install.sh | sh

8. 配置，运行
    使用命令 ``code server`` 就可以运行了，可以在配置文件中更改认证选项和密码

9. 升级
    1. 需要先删除之前安装的版本::

        rm -rf ~/.local/lib/code-server-*

    2. 再次运行安装脚本::

        curl -fsSL https://code-server.dev/install.sh | sh
    
10. 使用 
使用命令之后就可以使用IP地址+端口的访问使用。

