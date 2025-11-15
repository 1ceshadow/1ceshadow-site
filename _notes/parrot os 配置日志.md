---
title: parrot os 配置日志
date: 2025-05-26 18:58:49
feed: show
---
https://fcsblka.fcsubcn.cc:2096/api/v1/client/subscribe?token=26683a78fc4165d3ed4eae6a597245bf
首先 换键位[[键位配换]]
### apt 换源
[Mirrors | ParrotOS Documentation](https://www.parrotsec.org/docs/mirrors/mirrors-list/)
### 中文输入法
参见[个人博客](https://muzing.top/posts/3fc249cf/)

### 修改时间
发现时间不对
```
$ timedatectl 
               Local time: 一 2025-05-19 06:16:58 CST
           Universal time: 日 2025-05-18 22:16:58 UTC
                 RTC time: 日 2025-05-18 22:16:58
                Time zone: Asia/Shanghai (CST, +0800)
System clock synchronized: no
              NTP service: inactive
          RTC in local TZ: no
```
安装ntp,自动调整好了。

### 听说要优化散热控制
`sudo apt install tlp thermald`,安装这俩
`sudo systemctl enable tlp`

现在的arch linux用performance-tweaks 感觉比上面两个好，风扇声没有那么大

### 显卡驱动

安装官方 NVIDIA 驱动：
`sudo apt install nvidia-driver nvidia-utils nvidia-settings`
如果需要支持 CUDA（用于深度学习或科学计算）：
`sudo apt install nvidia-cuda-toolkit`
验证安装：
`nvidia-smi`
优化：编辑 `/etc/modprobe.d/nvidia.conf`，
启用电源管理以降低功耗：`sudo nano /etc/modprobe.d/nvidia.conf`添加：`options nvidia-drm modeset=1`
注意：若使用 Optimus 技术（NVIDIA+Intel 核显），安装 nvidia-prime 管理双显卡切换：
```
sudo apt install nvidia-prime
prime-select nvidia  # 切换到 NVIDIA 显卡
prime-select intel   # 切换到 Intel 核显
```
安装很顺利，根据指示安装，重启后，CTRL+alt+F1~6进入tty，继续安装，就安装好了
<font color="red">
但体验很差😅
</font>
当我Windows的控制台设置核显输出时，Linux识别不到独立显卡；
设置独显直连，Linux不下驱动，调整不了亮度
设置混合输出，Linux进入不了图形化界面。

设置独显直连，安装完驱动。一看缩放，天塌了，有些部分随着驱动的安装自动缩放。有些部分却缩放不了。一些图标还可能是没有对应比例的图片，还能理解。有些字体为什么也缩放的很小😅

### 卸载显卡驱动
```bash
init 3
```
CTRL+alt+F1
进入文本终端
登录后
1. 禁用桌面管理器
```bash
sudo service lightdm stop
```
2. 移除原生驱动的黑名单
```bash
cd /etc/modprobe.d/
sudo rm blacklist-nouveau.conf
```
3. 卸载nVidia驱动
```bash
sudo nvidia-uninstall
```
4. 删除配置以及依赖包
```bash
sudo apt purge nivdia*
sudo apt autoremove
```
5. 重新安装x服务器和显卡驱动
```bash
sudo apt install --reinstall xserver-xorg
sudo apt install --reinstall xserver-xorg-video-nouveau
```
6. 初始化
```bash
sudo update-initramfs -u
``` 
7. 重启
```bash
reboot
```

#### 目前
用parrot os[官网](https://www.parrotsec.org/docs/configuration/nvidia-drivers)提到的
```bash
sudo apt install nvidia-driver -t lory-backports
```
效果也只能说马马虎虎，

### 触摸板
机械革命笔记本的触摸板通常由 Synaptics 或 Elan 驱动支持。
安装触摸板驱动：（一般就有）
```
sudo apt install xserver-xorg-input-synaptics
```
优化触摸板设置（如多指触控、滚动）：编辑 `/etc/X11/xorg.conf.d/70-synaptics.conf`：
```
sudo mkdir -p /etc/X11/xorg.conf.d`
sudo nano /etc/X11/xorg.conf.d/70-synaptics.conf
```
添加示例配置：
```
Section "InputClass"
    Identifier "touchpad"
    Driver "synaptics"
    MatchIsTouchpad "on"
    Option "TapButton1" "1"
    Option "TapButton2" "3"
    Option "TapButton3" "2"
    Option "VertEdgeScroll" "on"
    Option "HorizEdgeScroll" "on"
EndSection
```
重启 X 会话（或重启系统）生效。

---

简单地配置一下 终端
- 取消 默认在新终端中显示菜单栏
- 设置起始标题，替换原始标题
- 颜色-调色板-内置方案： XTerm
- 禁用滚动条

首选项-关于我
![[Pasted image 20250428190456.png]]
换个头像

换菜单图标

![[Pasted image 20250428190546.png]]
给这个也换一下
因为菜单图标大小是 16px(默认)，所以需要找16x16px的图片，
![[Pasted image 20250428190935.png|400x400]]
也可以用`convert`工具剪切/缩放图片

然后将图片放到`/usr/share/icons/xxx`的相关目录中
这个`xxx`取决于用的是什么主题的icon，
进入该主题目录下，选择图标尺寸，如果屏幕缩放率设置的是200%，则选择带@2x
一般是更改 app/start-here-kde.png文件即可

### 安装rust
### 安装tealdeer


