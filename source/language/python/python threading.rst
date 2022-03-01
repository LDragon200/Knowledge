Python threading模块
====================

threading模块中包含了关于线程操作的丰富功能，包括：常用线程函数，线程对象，锁对象，递归锁对象，事件对象，条件变量对象，信号量对象，定时器对象，栅栏对象。

threading 模块的使用
--------------------

定义线程
~~~~~~~~

1. 定义一个函数

.. code:: python

    import threading
    
    def func():
        while True:
            pass
    threading.Thread(target=func, args=())

这样就定义了一个运行内容为函数 func() 中代码块的线程对象。

或者使用重写 threading.Thread 类的 run() 方法的方式定义一个线程对象。

.. code:: python

    class myThread (threading.Thread):   #继承父类threading.Thread
        def __init__(self, threadID, name, counter):
            threading.Thread.__init__(self)
            self.threadID = threadID
            self.name = name
            self.counter = counter
        def run(self):                   #把要执行的代码写到run函数里面 线程在创建后会直接运行run函数 
            print("Starting " + self.name)
            print_time(self.name, self.counter, 5)
            print("Exiting " + self.name)

实例化这个类之后就得到了一个线程对象

线程对象管理
~~~~~~~~~~~~

启动线程：start()方法

isAlive()方法测试线程是否是活动

一个线程能调用别的线程的join()方法。这将阻塞调用线程，直到拥有join()方法的线程的调用终止。

线程有名字，默认的是Thread-No形式的，名字能传给构造函数，通过setName()方法设置，用getName()方法获取。

线程能被标识为’daemon
thread’(守护线程).这标志的特点是当剩下的全是守护线程时，则Python程序退出。它的初始值继承于创建线程。标志用setDaemon()方法设置，用isDaemon()获取。

python threading 启动的线程，并没有提供终止线程的方法。
但可以通过threading.Thread._Thread__stop(thread)的方式结束进程。

实验结果如下：python2时，p.isAlive()会报False，但实际进程并未结束。用python3会报错。

或者使用ctypes强行杀掉线程

实验结果如下 python2 可以结束进程，python3未测。

列出线程对象： threading.enumerate() 返回线程列表。

进程同步
~~~~~~~~

使用 threading.Lock 类可以设置进程锁，从而进行进程同步。
使用进程锁有以下2种方式

.. code:: python

    
    some_lock = threading.Lock()
    with some_lock:
        # do something
        pass

相当于

.. code:: python

    some_lock.acquire()
    try:
        # do something
        pass
    finally:
        some_lock.release()

Lock 类有三个方法：

-  acquire() – lock the lock, possibly blocking until it can be obtained
-  release() – unlock of the lock
-  locked() – test whether the lock is currently locked



