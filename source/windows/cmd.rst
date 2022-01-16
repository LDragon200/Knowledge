windows 命令行
=======================

文件格式
################

后缀名为 ``.bat`` 或者 ``.cmd``。

词法
################

注释
++++++++++++++++

可以利用 goto 命令来设置区块注释::

    goto start
    = 可以是多行文本，可以是命令
    = 可以包含重定向符号和其他特殊字符
    = 只要不包含 :start 这一行，就都是注释
    :start   

1. :: 注释内容（第一个冒号后也可以跟任何一个非字母数字的字符）
2. rem 注释内容（不能出现重定向符号和管道符号）
3. echo 注释内容（不能出现重定向符号和管道符号）〉nul
4. if not exist nul 注释内容（不能出现重定向符号和管道符号）
5. :注释内容（注释文本不能与已有标签重名）
6. %注释内容%（可以用作行间注释，不能出现重定向符号和管道符号）
7. goto 标签 注释内容（可以用作说明goto的条件和执行内容）
8. :标签 注释内容（可以用作标签下方段的执行内容）   

变量
++++++++++++++++

变量无需声明可直接引用，其值为空字符串，并且大小写不敏感。可使用defined关键字或是否为空字符串""判断变量是否为空::

    rem 将代码保存为bat文件执行
    @echo off
    rem set var2="var2"
    if not defined var2 ( 
        echo var2 is not defined, the value is: %var2%
    ) else ( 
        echo var2 is defined, the value is: %var2%
    )

    if "%var2%"=="" (
        echo var2 is not defined, the value is: %var2%
    ) else (
        echo var2 is defined, the value is: %var2%
    )

变量的作用域::

    默认为全局变量（Global），可使用setlocal命令将变量作用域设置为local:
    
    rem var_scope.bat
    @echo off
    setlocal
    set v=Local Variable
    echo v=%v%

    rem cmd.exe
    D:\cmdtest>set v=Global Variable
    D:\cmdtest>var_scope
    v=Local Variable
    D:\cmdtest>echo v=%v%
    v=Global Variable
    D:\cmdtest>

设置变量::

    @echo off
    set var1=2+2
    set /a var2=2+2
    set /p var3=Please input a number:
    set /p md5=<file_info.md5
    echo var1: %var1%
    echo var2: %var2%
    echo var3: %var3%
    echo md5: %md5%

给变量赋值::

    @echo off
    set var1=2+2  & :: 变量名为字符串 "2+2"
    set /a var2=2+2 & :: 添加 /a  参数会将算数表达式的值做运算，将结果赋给变量
    set /p var3=Please input a number: 
    set /p md5=<file_info.md5
    echo var1: %var1%
    echo var2: %var2%
    echo var3: %var3%
    echo md5: %md5%

读取变量::

    可通过%var%, 读取变量值
    set var，列出var开头的所有变量
    set，列出所有变量，如系统环境变量TEMP、PATH等也会列举出来
    !var!，两个感叹号，延迟读取变量值

系统内置变量::

    %date%，系统日期，类似：2020/02/29 周六
    %time%，获取系统时间，类似：17:13:15.18
    %cd%，获取当前目录
    %RANDOM% 系统 返回 0 到 32767 之间的任意十进制数字
    %NUMBER_OF_PROCESSORS% 系统 指定安装在计算机上的处理器的数目。
    %PROCESSOR_ARCHITECTURE% 系统 返回处理器的芯片体系结构。值：x86 或 IA64 基于Itanium
    %PROCESSOR_IDENTFIER% 系统 返回处理器说明。
    %PROCESSOR_LEVEL% 系统 返回计算机上安装的处理器的型号。
    %PROCESSOR_REVISION% 系统 返回处理器的版本号。
    %COMPUTERNAME% 系统 返回计算机的名称。
    %USERNAME% 本地 返回当前登录的用户的名称。
    %USERPROFILE% 本地 返回当前用户的配置文件的位置。
    %~dp0，bat脚本文件所在目录

特殊变量
################

::

    %*，表示参数列表，比如：var_arg.bat arg1 arg2 arg3，则 %* = arg1 arg2 arg3
    %0，表示脚本文件名，调用时var_arg则%0=var_arg，若调用时var_arg.bat则%0=var_arg.bat
    %1，表示第一个参数
    %~1，第一个参数去引号，如：var_arg.bat “arg1”，%~1得到arg1
    %~f0，脚本文件完整路径名
    %~dp0，脚本文件所在目录

运算符
++++++++++++++++

算术运算符::

    +   Add                set /a "_num=_num+5"
    +=  Add variable       set /a "_num+=5"
    -   Subtract           set /a "_num=_num-5"
    -=  Subtract variable  set /a "_num-=5"
    *   Multiply           set /a "_num=_num*5"
    *=  Multiply variable  set /a "_num*=5"
    /   Divide             set /a "_num=_num/5"
    /=  Divide variable    set /a "_num/=5"
    %%  Modulus            set /a "_num=17%%5"
    %%= Modulus            set /a "_num%%=5"
    !   Logical negation  0 (FALSE) ⇨ 1 (TRUE) and any non-zero value (TRUE) ⇨ 0    (FALSE)
    ~   Bitwise invert
    &   AND                set /a "_num=5&3"    0101 AND 0011 = 0001 (decimal 1)
    &=  AND variable       set /a "_num&=3"
    |   OR                 set /a "_num=5|3"    0101 OR 0011 = 0111 (decimal 7)
    |=  OR variable        set /a "_num|=3"
    ^   XOR                set /a "_num=5^3"    0101 XOR 0011 = 0110 (decimal 6)
    ^=  XOR variable       set /a "_num=^3"
    <<  Left Shift.    (sign bit ⇨ 0) An arithmetic shift.
    >>  Right Shift.   (Fills in the sign bit such that a negative number always remains negative.)    Neither ShiftRight nor ShiftLeft will detect overflow.
    <<= Left Shift variable     set /a "_num<<=2"
    >>= Right Shift variable    set /a "_num>>=2"

    ( )  Parenthesis group expressions  set /a "_num=(2+3)*5"
    ,   Commas separate expressions    set /a "_num=2,_result=_num*5"

数据类型
################
批处理中的变量基本上是万能的,可以储存各种各样的数据,不过用来计算时你会发现变量类型转为了int,数值的极端范围为[-2147483648，2147483647]


流程控制
################

分支语句
::

    if exist d:\test.txt (echo D盘下有test.txt存在) else (echo D盘下不存在test.txt)
　　2、if "abc"=="xyz" (echo 字符串abc等于字符串xyz) else (echo 字符串abc不等于字符串xyz)
　　3、if 1 equ 2 (echo 1等于2) else (echo 1不等于2)
　　4、if defined str (echo 变量str已经被赋值，其值为%str%) else (echo 变量str的值为空)


循环语句
::

    for /参数 %变量 in (集) do 命令
    
    for /d %a in (c:\*.*) do echo %a
    rem /d 参数是指定仅对目录而不是文件执行的for命令
    
    rem /R参数之后还可带盘符及路径

    @echo of
    for /r . %i in (abc.txt) do echo. > %i
    echo on

    for /L %%变量 in (起始值，每次增值，结束时的比较值) do 命令

    参数/f将会打开（集）里的文件，使for命令能处理文本文件的读取和添加删除替换等编辑性的操作

流程跳转 goto
::

    @echo off
    set /p input=请输入字母A或B：
    if "%input%"=="A" goto A
    if "%input%"=="B" goto B
    pause
    exit

    :A
    echo 您输入的字母是A
    pause
    exit

    :B
    echo 您输入的字母是B
    pause
    exit 　　

