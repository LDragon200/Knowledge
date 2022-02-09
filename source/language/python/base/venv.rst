虚拟环境
========

创建虚拟环境的必要性
--------------------

在实际项目开发中，我们通常会根据自己的需求去下载各种相应的框架库，但是可能每个项目使用的框架库并不一样，或使用框架的版本不一样，这样需要我们根据需求不断的更新或卸载相应的库。直接用全局Python环境操作会让我们的开发环境和项目造成很多不必要的麻烦，管理也相当混乱。

虚拟环境的安装和使用
--------------------

使用 virtualenv
~~~~~~~~~~~~~~~

在 python3.3 之前，只能通过 virtualenv 创建虚拟环境，首先需要安装
virtualenv

1. 安装

   ``pip install virtualenv``

2. 创建虚拟环境

   ``virtualenv --no-site-packages myvenv``

使用 venv
~~~~~~~~~

Python3.3 之后，可以用模块 venv ，不用单独安装

创建虚拟环境：\ ``python -m venv myvenv``

--------------

通过 virtualenv 和 模块 venv
创建的虚拟环境，激活方式是一样的，即运行激活脚本：

-  mac:

   ``$ source myvenv/bin/activate``

-  win

   激活脚本路径是 ``<myvenv>\Scripts\activate.bat``\ ，如果是 powershell
   命令行，脚本换成 ``Activate.ps1``

删除虚拟环境：

::

   直接删除目录下的 venv 目录即可

--------------

开发完成后，使用 ``pip freeze > requirements.txt``
命令将项目的库依赖导出

使用 virtualenvwrapper
----------------------

virtualenvwrapper 这一命令行工具就是通过对 virtualenv
进行封装，解决了需要每次使用 source
命令导入虚拟机运行环境的问题,并且将虚拟环境作统一管理

virtualenvwrapper 安装配置（Mac）
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: shell

   $ sudo pip3 install virtualenvwrapper

然后添加两个环境变量

.. code:: shell

   export WORKON_HOME=$HOME/.virtualenvs  # 工作目录
   source /usr/local/bin/virtualenvwrapper.sh # 查找 virtualenvwrapper.sh 所在的路径

常用命令

-  mkvirtualenv

   创建虚拟环境

-  lsvirtualenv

   列出虚拟环境

-  rmvirtualenv

   删除虚拟环境（不能直接删除目录）

-  workon

   切换虚拟环境

pipenv
------

安装
~~~~

::

   pip3 install pipenv

创建虚拟环境
~~~~~~~~~~~~

::

   mkdir project
   cd project
   pipenv install

初始化好虚拟环境后，会在项目目录下生成2个文件Pipfile和Pipfile.lock。为pipenv包的配置文件，代替原来的
requirement.txt。

包管理
~~~~~~

::

   pipenv install requests
   pipenv graph # 查看安装包及依赖关系
   pipenv install --dev requests --three # 通过--dev指明只安装在开发环境中
   pipenv lock -r --dev > requirements.txt
   pipenv install -r requirements.txt

使用环境
~~~~~~~~

1. ``pipenv run python xxx.py`` 命令直接运行
2. ``pipenv shell`` 命令进入虚拟环境,同样使用 ``deactivate``
   退出虚拟环境(退出后仍然在虚拟环境\ ``Shell for UNKNOWN_VIRTUAL_ENVIRONMENT``)中，需要输入exit退出后再使用
   ``pipenv shell`` 中

删除虚拟环境
~~~~~~~~~~~~

``pipenv --rm``

.. code:: shell

   pipenv --where                 列出本地工程路径
   pipenv --venv                  列出虚拟环境路径
   pipenv --py                    列出虚拟环境的Python可执行文件
   pipenv install                 创建虚拟环境
   pipenv isntall [moduel]        安装包
   pipenv install [moduel] --dev  安装包到开发环境
   pipenv uninstall[module]       卸载包
   pipenv uninstall --all         卸载所有包
   pipenv graph                   查看包依赖
   pipenv lock                    生成lockfile
   pipenv run python [pyfile]     运行py文件
   pipenv --rm                    删除虚拟环境


