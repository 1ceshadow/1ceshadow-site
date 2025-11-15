---
title: shell-0x00
date: 2025-01-31 14:28:31
feed: show
---
#shell #linux 

[一篇文章让你彻底掌握Shell](https://mp.weixin.qq.com/s/GmSqHJiBToncvcpFAJUZbw)

### 常用命令
+ **wget** : web get
+ **pwd** : Present working directory
+ **cd** : change directory
+ **ls** : list directory
+ **cat** : concatenate(连接) and print files
+ **head** : read the first 10 lines
+ **less** : read larger files
+ **mv** : move  
+ **cp** : copy  
+ **rm** : remove, delete a file   %% move 重在移动；remove重在脱离原来位置 %%
+ **grep** : global search regular expression and print out the line
注：Linux命令是调用可执行程序，调用`/bin` 或`/usr/bin` `/usr/local/bin`等下的程序，shell命令是bash, zsh等直接解释执行的命令。

---
[bash官方手册](https://www.gnu.org/software/bash/manual/bash.html) [中文译本](E:\learn_resource\计算机\linux\Bash4.0参考文档.pdf)
**正式开始**

## 解释器

`#!` ：shebang (or Hashbnag) ，告诉系统 其后路径所指定的程序 就是解释此脚本文件的程序  
常见的有sh, python, php等.  
```shell
# 两种皆可，第二种更好
#!/bin/bash
#!/usr/bin/env bash
```

## 注释

上面的shebang是一种特殊的注释。  

+ 单行注释： `#` 开头
+ 多行：`:<<EOF` 开头，`EOF` 结束 
## 变量

+ bash中没有数据类型，任何都是字符串。
+ 变量赋值语句为 `foo=2` 
	+ 不能有空格，会让bash以空格分隔，将部分语句误认为是命令
	+ 这个2是 ’字符串‘
```shell
$ foo = 2
Command 'foo' not found, did you mean:
  command 'goo' from deb goo
  command 'fio' from deb fio
  command 'fop' from deb fop
  command 'foot' from deb foot
Try: sudo apt install <deb name>

$ foo= 2
2: command not found

```
+ 访问变量可以用`$var` 或`${var}`，`{ }` 花括号加不加都可以，起到识别变量边界的作用，建议加上。
+ 计算表达式用 `expr`
```shell
$ foo=2

$ expr $foo + 2
4

```
+ `readonly var` 将变量定义为只可读，再对该变量赋值则报错
+ `unset vat` 删除变量

| 变量    | 描述                           |
| ----- | ---------------------------- |
| $HOME | 当前用户的用户目录                    |
| $PATH | 用分号分隔的目录列表，shell 会到这些目录中查找命令 |
| $PWD  | 当前目录                         |
| $     |                              |
## echo

基本用法：
```shell
$ echo "hello world"
hello world

$ eho "hello, \"zp\""
hello, "zp"
```
输出变量：
```shell
$ name=zp
$ echo "hello, ${name}"
hello, zp

# 字符串
$ echo "yes\nno"
yes\nno

$ echo -e "yes\nno"  # -e 开启转义
yes
no
echo -e "yes\c"
```
## 字符串
#### 引号
+ bash的字符串可以用双引号、单引号也可以不加引号。
+ 区别在于：
	+ 单引号，不识别变量，不能单独出现单引号，用转义也不行
	+ 双引号，识别变量
	+ 建议使用双引号
+ 字符串的长度： `${#str}` 

## 条件
