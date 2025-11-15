---
title: shell-0x01从句
date: 2025-01-31 14:28:30
feed: show
---
### 条件检测/test

条件检测用 `[ ]`括起来

| 写法  | 含义  |
| --- | --- |
| -eq | ==  |
| -ne | !=  |
| -gt | >   |
| -ge | >=  |
| -lt | <   |
| -le | <=  |
注：用于整数计算比较

布尔操作符：
```shell
&& = -a 
|| = -o
```
注： `-a` `-o`  在 `[]`/`test`中

### if
```shell
if [ $1 -eq 1 ];
then
	echo "hello"
fi

if [ "$1" -ge 0 ];
then
	echo "great than or equal to zero"
elif [ "$1" = "hello world" ];
then
	echo "hello"
else
	echo "i don't know ~~"
```
注1：其中 `$1`和`"$1"`都可以，避免出错，建议加双引号(虽然目前我还不知道什么情况 出错)
注2：加双引号就是把变量解释之后视为一个整体
### for loops

```shell
sheep=("one" "dos" "tre")
for s in $sheep
do
	echo "$s sheep..."
done

> one sheep...
> dos sheep...
> tre sheep...

for s in "$sheep"
do
	echo "$s sheep..."
done

> one dos tre sheep...
```

support range
```n=0
for i in {1..10}
do
	n=$(expr $n + $i)
done

>

echo $n

>55

```
练习😈
复制该目录下txt文件名字（如`1.txt`），新建`new_name.txt`文件
```shell
files=$(ls *.txt)
for file in $files
do
	cp $file new_$file
done
```


### case
```shell
read -p "are you 18?" answer
case "$answer" in
    "yes")
      echo "hoooooo";;
    "ne")
      echo "noooooo";;
    "are you")
      echo "emmmmmm";;
    *)
	  echo "answer"
esac
```
注：`zsh`的read没有-p选项
```shell
# 这样代替
echo/print "xxx"
read x
```
