---
title: getline的隐式声明
date: 2025-04-16 15:54:49
feed: hide
---
当我用到getline，gcc编译时显示：
```bash
gcc -o kano kano.c -Wall -Wextra -pedantic -std=c11
kano.c: In function ‘editorOpen’:
kano.c:202:13: warning: implicit declaration of function ‘getline’ [-Wimplicit-function-declaration]
  202 |   linelen = getline(&line, &linecap, fp);
```
显示为警告

`getline`并不是C的标准函数，需要定义[功能测试宏](https://www.gnu.org/software/libc/manual/html_node/Feature-Test-Macros.html)

### 解决
可以直接加上宏
```C
#define _GUN_SOURCE
```
这个宏是所有内容：ISO C89、ISO C99、POSIX.1、POSIX.2、BSD、SVID、X/Open、LFS 和 GNU 扩展。在 POSIX.1 与 BSD 冲突的情况下，POSIX 定义优先。

或者
```C
#define _DEFAULT_SOURCE
#define _BSD_SOURCE
#define _GNU_SOURCE
```

*_DEFAULT_SOURCE* : 除了 X/Open、LFS 和 GNU 扩展之外，还包括大多数功能：其效果是启用 POSIX 2008 版中的功能，以及某些 BSD 和 SVID 功能，而无需单独的功能测试宏来控制它们。