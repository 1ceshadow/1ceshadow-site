---
title: C语言-工具
date: 2025-05-19 20:19:56
feed: show
---
+ gcc
+ GNU Make和CMake
+ gdb
+ valgrind
+ vim/emacs
## gcc
gcc 是GNU的C编译器，编译共4步（[[编译涉及的主要步骤]]）
**选项**
*-x language filename* 指定文件使用的语言，当你不使用这个参数，gcc将根据文件后缀来判断。
```C
gcc -x c hello.pig
```
*-E* 只激活预处理，这个不生成文件，要观察可以把它重定向到一个文件中
```C
gcc -E hello.c > poanpapan.txt
```
*-S* 只激活预处理和编译，把文件编译成汇编代码
```C
gcc -S hello.c
```
*-c*只激活预处理，编译，汇编，生成obj文件
```C
gcc -c hello.c
```
*-o*指定目标名称
```C
gcc -o hello.asm -S hello.c
```
*-g*生成调试信息 *-ggdb*生成gdb可用的编译信息
*-Wall*生成警告
*-pedantic* 使用了扩展语法的地方产生警告
*-Werror* 将警告当作错误处理
*-std=standard* 指定使用的语言标准，如`-std=c99` 使用C99标准

**多文件**
方法一：
```C
gcc file1.c file2.c -o test
```
方法二：
```C
gcc -c file1.c
gcc -c file2.c
gcc -o test file1.o file2.o
```
相比较：当文件发生改变时，方法一需要对所有文件重新编译，方法二只需要重新编译改变的文件。
**链接库** 
*-llib* 
```C
gcc hello.c -o hello -lmath //链接math库
```
*-I* 指定头文件搜索路径
```C
gcc -I /home/linux/include hello.c -o hello
```
*-L*指定库文件搜索路径

## GNU Make和CMake
make是用脚本告诉编译器如何编译（如面对大型项目，多个文件），并优化编译过程（只需要重新编译改变的文件）
这里有一篇写得深入浅出的[文档](https://seisman.github.io/how-to-write-makefile/overview.html)供大家参考
而CMake是比CUN Make更高层次的系统构建器，跨平台，CMake会根据`CMakeLists.txt` 生成使用特定平台，编译器的构建文件，如在Unix系统上生成`Makefile` ,window系统上生成VS项目文件。
## gdb
调试工具，使用时，在gcc上加上-g参数
```C
gcc -g -o test test.c
```
`gdb test`进入gdb调试bugging界面
显示：
+ *list 行号*  ：打印给定行号周围的源代码
+ *print 表达式* ：（如果表达式有副作用，则会影响程序，如：`print x = 3）
	+ *print* 后加上 */x* 则以十六进制打印结果 `p/x` 
	+ 打印数组中的多个元素，可以在值后面加上 *@数字* ，如：`a[0]@5` ，则打印其前五个变量。
+ *display 表达式* ：每次gdb停止时，显示表达式的值，可缩写为  `disp i` 
+ *backtrace* ：查看所有堆栈帧
	+ *up* 和 *down* 选择不同的framestack frames
+ *info* ：
+ -------------------------------------------------------------------------------------
+ *break 函数名*/*行号* ：在给定函数或行号处设断点
	+ 在一个for的某个情况停`break 7 if i==100` 
	+ 给已存在的断点添加条件`cond 1 i==2500` ，如果`cond` 没有表达式，则创造一个没有条件的断点
	+ *enable* 和 *disable* 启用or禁用断点
+ *star* ：运行程序，做好处理，当进入main函数停止，等待输入。
+ *run* ：运行程序，直到遇到使他停止的条件
+ *step* ：使程序前进一步：执行该行，当代码跳转到其他行时停止。
+ *next* ：使程序前进一行：如果该行是调用函数，则运行整个函数。
+ *until* ：循环执行完成停止
+ *finish* ：完成当前函数
+ --------------------------------------------------------------------------------------
+ *watch* ：观察表达式的值，当其值改变时，停止。