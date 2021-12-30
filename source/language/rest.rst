reStructuredText
=========================

可以进入网址 http://rst.ninjs.org/ 在线进行测试

reStructuredText 每一个部分上下都需要一个空行将内容分隔开来。

标题
################################

根据我实际使用的测试，标题分为三个级别，从 h1-h3 分别是::

    h1
    ========================

    h2
    ########################

    h3
    ++++++++++++++++++++++++

文本
################################

普通文本：
    普通文本没有特殊格式::

        普通文本

引用文本：
    引用文本添加缩进即可::

        普通文本

            引用文本

其他文本：
    ::
        一个星号: ``*text*`` 用于强调( 斜体 )，
        两个星号: ``**text**`` 用于强调( 粗体 )
        反引号:  ``text`` 代码示例。

链接
########################

外部链接：
    外部链接有两种方式::

        `链接文本 <https://domain.invalid/>`_ 

        或者使用

        This is a paragraph that contains `a link`_.

        .. _a link: https://domain.invalid/

        将标记与链接分开

内部链接：
    内部链接是通过Sphinx提供的特殊reST角色完成的。使用交叉引用对象。
    
    引用任意位置::

        .. 唯一标签名:

        详情
        --------------------------

        这里是内容

        如果要了解，请查看 :ref:`唯一标签名`.

    引用图表::

        .. _my-reference-label支持中文:

        .. figure: URL/to/img
        :alt: 野火logo
        :align: center

        引用方式 :ref:`my-reference-label支持中文` 

        .. _拨码开关启动配置表:

        .. table:: 拨码开关启动配置表

            ==== ====== ========== ==== == ===
            编号 名称   NAND FLASH eMMC SD USB
            ==== ====== ========== ==== == ===
            1    MODE0  0          0    0  1
            2    MODE1  1          1    1  0
            3    CFG1-4 1          0    0  X
            4    CFG1-5 0          1    0  X
            5    CFG1-6 0          1    1  X
            6    CFG1-7 1          0    0  X
            7    CFG2-3 0          1    0  X
            8    CFG2-5 0          0    1  X
            ==== ====== ========== ==== == ===

        引用示例 :ref:`拨码开关启动配置表` 。
        自定义名称引用 :ref:`自定义名称 <拨码开关启动配置表>` 

    对于没有在标题之前的引用，需要在引用之后自己定义文字内容::
        
        .. _标签名:

            内容

            其他内容

        :ref: `引用 <标签名>`

文档引用：
    链接到指定的文件;文档名称可以绝对或相对方式指定::
        
        自定义引用文字

        :doc:`引用本地的其它rst文档,rst后缀要省略，如about_us <../about_us>`

        使用标题文字
        :doc:`../about_us`

下载文件引用::
    See :download:`this example script <../example.py>`.
    
    
    .. only:: builder_html

    See :download:`this example script <../example.py>`.


图片
################

::

    .. image:: picture.jpeg
        :height: 100px
        :width: 200 px
        :scale: 50 %
        :alt: alternate text
        :align: right


    .. figure:: picture.png
        :scale: 50 %
        :alt: map to buried treasure
        :align:"left", "center", or "right"
        :figwidth:"image", length, or percentage of current line width
        :figclass:text

