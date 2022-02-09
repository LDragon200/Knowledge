面向对象编程（Object Oriented Programming，OOP，面向对象程序设计）
==================================================================

举个例子： 要写一个五子棋程序，使用面向过程的方式编写：

1、开始游戏，2、黑子先走，3、绘制画面，4、判断输赢，5、轮到白子，6、绘制画面，7、判断输赢，8、返回步骤2，9、输出最后结果。

如果按照面向对象的方式来编写我们先要抽象出里面的角色：

两个玩家

黑白两子

棋盘

除了这些还需要一个裁判，来判断输赢。

这里面的每一个角色我们可以称之为对象，为对象赋予属性：比如说棋子的黑和白，棋盘的大小。然后再赋予一些动作：如玩家的落子，棋盘的更新。

两个玩家对象我们可以再进行抽象，可以抽象出玩家类，里面有基本上的属性和动作。类可以实例化，也就是根据抽象的类再创造出来一个对象。

下面我们根据这些信息来大致的一个程序

.. code:: python

    class Main: 
        '''
        模拟裁判
        ''' 
                
        def is_win(self):
            result = input("判断输赢")
            if result == "y":
                return True
            return False
                
                
    
    class Player:
        '''
        玩家类
        '''
        def __init__(self, name):
            self.name = name
        def falling(self):
            input(self.name+"落子")
    
    class Chessboard:
        '''
        棋盘类
        '''
        def __init__(self):
            print("初始化棋盘")
        
        def pieces(self):
            return []
    
    class ChessPiece:
        '''
        棋子类
        '''
        pass
    
    
    
    if __name__ == "__main__":
        board = Chessboard()
        p1 = Player("p1")
        p2 = Player("p2")
        referee = Main()
        while True:
            p1.falling()
            if referee.is_win(board.pieces()):
                print(p1.name + " win")
                break
    
            p2.falling()
            if referee.is_win(board.pieces()):
                print(p2.name + " win")
                break
        
        

面相对象的特性
--------------

1. 封装

   封装，就是把客观事物封装成抽象的类，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。

2. 继承

   继承，指可以让某个类型的对象获得另一个类型的对象的属性的方法。它支持按级分类的概念。

3. 多态

   多态，是指一个类实例的相同方法在不同情形有不同表现形式。多态机制使具有不同内部结构的对象可以共享相同的外部接口。

五大基本原则：SPR, OCP, LSP, DIP, ISP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. 单一职责原则SRP(Single Responsibility Principle)

   是指一个类的功能要单一，不能包罗万象。

2. 开放封闭原则OCP(Open－Close Principle)

   扩展性方面开放 更改性方面封闭

3. 里式替换原则LSP(the Liskov Substitution Principle LSP)

   子类应当可以替换父类并出现在父类能够出现的任何地方。

4. 依赖倒置原则DIP(the Dependency Inversion Principle DIP)

   编译A模块时需要直接包含到B模块的cpp文件，而编译B时同样要直接包含到A的cpp文件。

5. 接口分离原则ISP(the Interface Segregation Principle ISP)

   模块间要通过抽象接口隔离开，而不是通过具体的类强耦合起来

.. code:: python

    print(isinstance(print , object)) # 返回Turn  # issubclass() 检查一个类是否是另一个类的子类

.. code:: python

    # 调用类的__mro__方法打印父类及继承关系
    
    print(bool.__mro__)
    print(True.__class__.__mro__)
    import os
    os.__class__.__mro__


