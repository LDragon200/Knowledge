Sphinx 快速入门
================================

本文档是以 Sphinx 为工具，使用 reST 编写的。项目托管在 github 上、文档托管于Read the Docs。

Sphinx
################
Sphinx 是一种文档工具，它可以令人轻松的撰写出清晰且优美的文档, 由 Georg Brandl 在BSD 许可证下开发. 新版的Python文档就是由Sphinx生成的， 并且它已成为Python项目首选的文档工具,同时它对 C/C++ 项目也有很好的支持; 并计划对其它开发语言添加特殊支持. 本站当然也是使用 Sphinx 生成的，它采用reStructuredText! Sphinx还在继续开发. 下面列出了其良好特性,这些特性在Python官方文档中均有体现。

* 丰富的输出格式: 支持 HTML (包括 Windows 帮助文档), LaTeX (可以打印PDF版本), manual pages（man 文档）, 纯文本
* 完备的交叉引用: 语义化的标签,并可以自动化链接函数,类,引文,术语及相似的片段信息
* 明晰的分层结构: 可以轻松的定义文档树,并自动化链接同级/父级/下级文章
* 美观的自动索引: 可自动生成美观的模块索引
* 精确的语法高亮: 基于 Pygments 自动生成语法高亮
* 开放的扩展: 支持代码块的自动测试,并包含Python模块的自述文档(API docs)等

Sphinx 使用 reStructuredText 作为标记语言, 可以享有 Docutils 为reStructuredText提供的分析，转换等多种工具.

sphinx 教程可参展：https://www.sphinx.org.cn/

Sphinx 安装
++++++++++++++++
Sphinx为Python语言的一个第三方库。所以我们首先要确认好电脑配置好了python环境。然后然后使用pip安装是Sphinx::

    pip install sphinx

建议使用国内源下载，速度会更快。

| 安装好之后使用 `sphinx-quickstart --version` 命令验证是否安装完成。
| 如果出现命令没有找到的错误，请检查环境变量的配置。是否将Python下的 `Scripts` 文件夹设置在了环境变量之中，以及文件夹中是否有 `sphinx-quickstart.exe` 文件。(Windows c操作系统)

Sphinx 创建项目
++++++++++++++++
::

    sphinx-quickstart [项目文件夹，默认当前文件夹]

接下来会让你选择一些配置，中文项目语种为zh_CN配置完成后就可以在文件夹下看到这个项目。

关于文档编写请参考 reStructuredText

生成文档
++++++++++++++++

在项目的根目录下输入命令::
    
    make [文档类型]
    make html        # 生成html文件
    make latexpdf    # 生成PDF文件

会在 build 相应目录下成相应的文档，不输入文档类型时会显示所有的可用类型。

    生成PDF文档时，需要计算机上有 LaTeX to PDF 的环境。

文档写好后，可以通过托管在 github 上，最后发布到 read the docs。

本地预览
++++++++++++++++

使用 `sphinx-autobuild` 插件 需要使用 `pip` 命令进行安装。

主题设置
++++++++++++++++

自带的主题可用在以下网站上找到 https://sphinx-themes.org/ 

::

    $ pip install sphinx-press-theme

然后在 `Conf.py` 添加主题：

::

    html_theme = 'press'

当然，你也可以自己写一个主题，参照: https://www.sphinx.org.cn/theming.html

如果在 Read the Docs 上托管是构建出错，可以查看报错，检查 conf.py 文件，使用 Python 第三方包以后需要在根目录下新建 requirements.txt 写入第三方包。
