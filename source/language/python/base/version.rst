python 版本管理
===============

python 版本管理可以使用pyenv，项目地址：https://github.com/pyenv/pyenv
 https://gitee.com/mirrors/pyenv

这里我找到了一篇关于 pyenv
介绍的比较好的文章：https://blog.51cto.com/u_14320361/2488888
文章中介绍了 pyenv
的安装，基本使用和卸载，大家可以去看看这篇文章尝试安装。

这里我主要解决两个问题：

1. pyenv 下载 python 速度慢的问题
2. 不同 python 版本的介绍

加速 pyenv 下载
---------------

pyenv 没有国内源，所以下载经常超时，解决这个问题的方式是：在 ``.bashrc``
或 ``.zshrc`` 中写入如下内容：

.. code:: shell

   # Mirror image for pyenv

   function pyinstall() {
       v=$1
       echo '准备安装 Python' $v
       FILE_PATH="~/.pyenv/cache"
       PYTHON_TEMP="~/.pyenv/cache/Python-$v.tar.xz"
       if [ ! -f "$FILE_PATH" ]; then
       mkdir "~/.pyenv/cache"
       fi
       if [ ! -f "$PYTHON_TEMP" ]; then
       curl -L https://npm.taobao.org/mirrors/python/$v/Python-$v.tar.xz -o ~/.pyenv/cache/Python-$v.tar.xz
       fi
       pyenv install $v
   }

然后 source 文件之后在命令行中使用 ``pyinstall [virsion]``
安装，这种方式也有缺陷，不能安装其他版本如 anaconda 的 python 版本

不同版本的python介绍
--------------------

-  python

   CPython 是 Python 社区的标准

-  pypy

   PyPy 是一个 Python
   解释器和即时编译（JIT）工具，它专注与速度、效率，以及和 CPython
   完全的兼容性。
   运行速度比CPython要快，以及可以安全的运行一些不被信任的代码。PyPy还有一个单独的支持微线程的版本。
   https://zhuanlan.zhihu.com/p/428215180

-  micropython

   MicroPython是Python 3编程语言的精简高效实现
   ，包括Python标准库的一小部分，并且经过优化，可在微控制器和受限环境中运行。

-  anaconda

   Anaconda is the birthplace of Python data science. We are a movement
   of data scientists, data-driven enterprises, and open source
   communities. Anaconda 是 Python
   数据科学的发源地。我们是一个由数据科学家、数据驱动型企业和开源社区组成的组织。
   Anaconda是一个可用于科学计算的Python发行版。
   Anaconda集成了大部分需要用到的Python包，尤其是数据科学类的包，在数据处理方面，你几乎可以在安装后直接进行使用。
   conda 是 Anaconda 的包管理工具

-  miniconda

   Miniconda是一款小巧的python环境管理工具，安装包大约只有50M多点，其安装程序中包含conda软件包管理器和Python。

-  activepython

   ActivePython是由 ActiveState 公司推出的专用的 Python 编程和调试工具。
   　　ActiveState 包含了一个完整的 Python 内核，直接就是调用 Python
   官方的开源内核，还有就是 Python 编程需要用到的 IDE，并附加了一些
   Python的 Windows扩展，同时还提供了全部的访问 Windows APIs
   的服务。ActiveState 虽然不像纯 Python
   那样是开源的，但是也可以免费下载使用。

-  graalpython

   Python 的 GraalVM 实现

-  ironpython

   IronPython 是一种在 NET 和 Mono 上实现的 Python 语言

-  jython

   Jython 是一个将Python代码编译成Java字节码的实现， 运行在JVM (Java
   Virtual Machine)
   上。另外，它可以像使用Python模块一样，导入并使用任何Java类。

   如果你需要与现有的Java代码库对接或者基于其他原因需要为JVM编写Python代码，那么
   Jython是最好的选择。

-  mambaforge

   这是 conda-forge 社区的一个社区项目。

-  miniforge3

   相当于 miniconda

-  pyston

   Pyston 最初是由 Dropbox 推出的基于 JIT 的 Python 实现。Pyston 解析
   Python 代码，并转换到 LLVM 中间表示（IR），然后 IR 通过 LLVM 优化器和
   LLVM JIT 引擎，得到可执行的机器码。

-  stackless

   stackless python从字面上理解就是没有栈的python。
   一般将函数的调用推进栈里面，后入栈单元计算完之后，先入栈的才能够完成


