初识函数
========

函数的定义
----------

函数参数的顺序是:
位置参数、默认参数(默认参数必须指向不变对象)、可变参数、命名关键字参数、关键字参数

.. code:: python

    # “/”之前的变量，只能通过位置方式传递参数
    # “*”之后的参数，只能用关键字参数的方式给出
    
    # @decorator  装饰器
    def func0(x, /, y=0, *, name='', **kwargse) -> None:
        return None
    
    def func1(a: type, /, b, c=None , *,d, **kwargs) -> None:
        return None
    
    def func2(*args) -> None:
        return None
    
    # 匿名函数返回一个可回调对象
    # a = lambda :return 1 报错 SyntaxError
    b = lambda x:print(f"匿名函数,参数{x}")
    c = lambda x, y=2:print(f"匿名函数,参数{x, y}")


python 中的内置函数
-------------------

https://docs.python.org/zh-cn/3/library/functions.html

函数的返回值
------------

函数体中 return 语句的结果就是返回值 返回多个值时的类型是元组 遇到
return 之后的语句不会被执行
