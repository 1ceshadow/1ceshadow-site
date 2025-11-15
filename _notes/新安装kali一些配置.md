---
title: 新安装kali一些配置
date: 2025-04-15 23:28:07
feed: show
---
下载上 kali 20251a版，这次没有下载iso文件，下载了官方提供的专为虚拟机优化的版本，直接下载下来是不用安装版本

所以默认用户名/密码是kali/kali 下面是一些设置微调

# 切换中文
以前一直用英文，但还不是母语，用的还是有点障碍

```bash
locale -a | grep zh_CN
```
查看是否安装了中文

没有显示

编辑locale的配置文件
```bash
sudo dpkg-reconfigure locales
```


使配置生效
```bash
sudo update-locale LANG=zh_CN.UTF-8
source /etc/default/locale
```
# 修改用户名和密码
```bash
sudo passwd 用户名 
```

然后新建一个管理员，来修改当前用户的用户名
这回用的图形化的程序“用户和组”
然后操作就很简单
# apt镜像源

# 算了，不好用，删了


