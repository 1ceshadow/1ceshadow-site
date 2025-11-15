---
title: shell-0x02streams
date: 2025-01-31 14:28:29
feed: show
---
+ `>` 将一个返回值输出到某个地方
```shell
$ echo "abc" > 1.txt

$ cat 1.txt
abc
$ echo "a" > 1.txt

$ cat 1.txt
a
```
+ `>>` 将一个返回值附加到某个地方
```shell
# 接着上面
$ echo "bbcc" >> 1.txt

$ cat 1.txt
a
bbcc
```
