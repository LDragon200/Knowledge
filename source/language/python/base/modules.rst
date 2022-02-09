Python 包管理
=============

Python 包安装
-------------

1. 在线安装

   -  pip

      ::

         pip install + 包名
         pip install + 包名==版本号
         pip install + 包名 -i + 镜像源url

      **pip 的一些源:**

      ::

         阿里云 http://mirrors.aliyun.com/pypi/simple
         豆瓣 http://pypi.douban.com/simple
         中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple
         清华大学 https://pypi.tuna.tsinghua.edu.cn/simple
         中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple

      **pip 源设置:**

      ::

         pip3 config set global.index-url='https://mirrors.aliyun.com/pypi/simple/'
         pip3 config set install.trusted-host='mirrors.aliyun.com'

   -  conda

      https://docs.conda.io/projects/conda/en/latest/commands.html

2. 离线安装

   离线安装通常是下载 .whl 或 .tar.gz 格式的文件，然后进行安装

   whl 格式的文件使用 ``pip install xxx.whl``

   .tar.gz
   或其他可以解压的格式解压后会获得源码，通过从源码安装的方式安装：\ ``python setup.py install``

Python 包卸载
-------------

有些 python 包安装时安装了依赖，直接卸载包会导致依赖包的残留
``pip show <模块名>``
这个命令行命令可以查看一个包的详细信息.通过这个命令我们可以查看并且删除包的依赖项。通过这个原理，我们可以写出一个脚本来卸载包及依赖.

.. code:: python

    import os
     
    def check_dependents(module_name) -> list:
        """
        查看一个模块的依赖
        :param module_name: 模块名
        :return: module_name 所依赖的模块的列表
        """
        with os.popen('pip show %s' % module_name) as p:
            dependents = p.readlines()
            if not len(dependents):
                return None
            dependents = dependents[-1]
            dependents = dependents.split(':')[-1].replace(' ', '').strip()
            if dependents:
                dependents = dependents.split(',')
            else:
                dependents = None
            return dependents
     
     
    def remove(module_name) -> None:
        """
        递归地卸载一个模块
        :param module_name: 模块名称
        :return: None
        """
        dependents = check_dependents(module_name)
        if dependents:
            print("找到如下依赖项: \n"+'\n'.join(dependents))
            confirm = input("确认是否卸载：")
            if confirm.lower() == 'y':
                for package in dependents:
                    remove(package)
            else:
                return None
        os.system('pip uninstall -y %s' % module_name)
     
     
    if __name__ == '__main__':
        pkg_name = input('请输入要卸载的第三方模块包: ')
        remove(pkg_name)


