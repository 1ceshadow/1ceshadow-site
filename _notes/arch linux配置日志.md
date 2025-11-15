---
title: arch linux配置日志
date: 2025-06-21 14:26:10
feed: show
---
用了几天arch linux越发喜欢，系统是如此流畅，如此舒服。上手也经过一个短暂的痛苦期
现在使用的是
```lua
 OS Garuda Linux x86_64  
├ Kernel Linux 6.14.7-zen2-1-zen  
├󰏖 Packages 2002 (pacman)[stable]  
├ Shell fish 4.0.2  
└ Age 2 days  
  
 DE KDE Plasma 6.3.5  
├󰧨 Window Manager KWin (X11)  
├󰧨 Login Manager sddm 0.21.0 (X11)  
├󰉼 WM Theme CatppuccinMocha-Classic  
├󰉼 Color Themes Mokka (Mokka) [Qt]  
├󰀻 System Icons Tela-circle-dracula-dark [Qt]  
├ System Fonts Inter (10pt) [Qt]  
└ Terminal konsole 25.4.1  
  
󰌢 PC Notebook  
├󰻠 CPU AMD Ryzen 7 8845H (16) @ 5.14 GHz  
├󰍛 GPU NVIDIA GeForce RTX 4060 Max-Q / Mobile [Discrete]  
├󰍛 GPU AMD Phoenix3 [Integrated]  
├󰍛 Vulkan 1.4.311 - radv [Mesa 25.1.1-arch1.1]  
└󰍹 Display(s) 2560x1600 @ 240 Hz in 15" [Built-in]
```
整体都采用这个catppuccin, Mokka的风格
![[Pasted image 20250527002455.png]]
(obsidian不是聚焦窗口所以自动变暗)
第一次接触arch linux，那个系统采用的是平铺式窗口，实在用不来。
至于现在安装下arch是，装debian中遇到了nvidia驱动问题。各种显示问题实在难绷，然后看到arch如此beautify。就来试一试。

### 第一次安装的坎
arch采用的pacman包管理工具。
我第一次先后遇到两次问题
1. 要合并一个文件
(第二次安装现在也留着这个问题)
![[附件/处理pacdiff.png]]
它说不熟悉，要了解它，我当时就直接合并了。然后就显示数据库有问题，镜像站有问题，就用不了pacman了，总是显示镜像站的问题
2. 密钥的问题
在安装过程中，提示我是否要使用公钥。我：是。然后就有各种签名问题。一直安装不上clash-verge。然后当然，以我的聪明才智，很容易就解决了

### 现在的体验
这个garuda系统非常好。
配备的助手对于我这个新手很友好。然后各种设置 鼠标、图像化操作非常丰富。
然后自动安装好了nvidia、风扇控制等等驱动而且这些驱动方面暂时没有问题。

之前遇到一个问题是 [[键位配换]] 一直设置不成功。然后我自己又写了一个脚本文件。放到系统设置的自动启动里面。但他总是出现各种问题。有时接入个设备他就不灵了。

不过现在发现原来他自带的可以设置![[附件/kde键位设置.png]]
### 影响windows显示时间
默认的设置会导致windows的时间不正常显示
取消 自动设置时间 再勾选后，均正常了。
### chrome输入有问题
具体情况是，它并不是完全不能输入，而是非常快速的按一个键，它识别不出来，需要按下一定时间才能识别出来，很影响体验。
然后将`fctix5`禁用后，可以正常输入，但也只能输英文了。
用的是官方的google-chrome，不过google-chrome和chromium都有这个问题

然后上网一搜索，发现大家都是使用的wayland有问题，而我是X11，按照网上的意思应该是很正常的。
按照网上的教程，用这个检查一下。
```
fcitx5-diagnose
```

```bash
...

# 前端设置：
此脚本检查的环境变量仅能显示当前命令行的环境。仍有可能您的环境并没有应用于整个桌面。您可以通过使用命令对某个无法正常工作的进程使用命令 `xargs -0 -L1 /proc/$PID/environ` 检查此进程的实际的环境变量。

## Xim:
1.  `${XMODIFIERS}`:

    环境变量 XMODIFIERS 已经正确地设为了“@im=fcitx”。
    从环境变量中获取的 Xim 服务名称为 fcitx.

2.  根窗口上的 XIM_SERVERS：

    Xim 服务的名称与环境变量中设置的相同。

## Qt:
1.  qt4 - `${QT4_IM_MODULE}`:

    环境变量 QT_IM_MODULE 已经正确地设为了“fcitx”。

    **`fcitx5-qt4-immodule-probing` 未找到.**

2.  qt5 - `${QT_IM_MODULE}`:

    环境变量 QT_IM_MODULE 已经正确地设为了“fcitx”。

    使用 fcitx5-qt5-immodule-probing 来检查在当前环境下将被实际使用的输入法模块：

        QT_QPA_PLATFORM=xcb
        QT_IM_MODULE=fcitx
        IM_MODULE_CLASSNAME=fcitx::QFcitxPlatformInputContext

3.  qt6 - `${QT_IM_MODULE}`:

    环境变量 QT_IM_MODULE 已经正确地设为了“fcitx”。

    使用 fcitx5-qt6-immodule-probing 来检查在当前环境下将被实际使用的输入法模块：

        QT_QPA_PLATFORM=xcb
        QT_IM_MODULE=fcitx
        IM_MODULE_CLASSNAME=fcitx::QFcitxPlatformInputContext

4.  Qt 输入法模块文件：

    找到了 fcitx5 的 qt 输入法模块：`/usr/lib/qt/plugins/platforminputcontexts/libfcitx5platforminputcontextplugin.so`。
    找到了未知的 fcitx qt 模块：`/usr/lib/qt6/plugins/plasma/kcms/systemsettings/kcm_fcitx5.so`。
    找到了 fcitx5 的 qt6 输入法模块：`/usr/lib/qt6/plugins/platforminputcontexts/libfcitx5platforminputcontextplugin.so`。
    找到了 fcitx5 qt5 模块：`/usr/lib/fcitx5/qt5/libfcitx-quickphrase-editor5.so`。
    找到了 fcitx5 qt6 模块：`/usr/lib/fcitx5/qt6/libfcitx-quickphrase-editor5.so`。

    下列错误也许并不准确，因为对路径所对应的 Qt 版本的猜测取决于发行版如何打包 Qt。如果您不使用任何对应版本的 Qt 程序，或者在 Wayland 下使用 Qt 的 text-input 支持，下列错误也不是严重问题。
    **无法找到 Qt4 的 fcitx5 输入法模块。**

## Gtk:
1.  gtk - `${GTK_IM_MODULE}`:

    **请使用您发行版提供的工具将环境变量 GTK_IM_MODULE 设为 "fcitx" 或者将 `export GTK_IM_MODULE=fcitx` 添加到您的 `~/.xprofile` 中。参见 [输入法相关的环境变量：GTK_IM_MODULE](http://fcitx-im.org/wiki/Input_method_related_environment_variables/zh-cn#GTK_IM_MODULE)。**

    **如果您的混成器完全支持 gtk 使用的 text-input 协议，您也可以使用 gtk 内置的 Wayland 模块。**

    使用 fcitx5-gtk2-immodule-probing 来检查在当前环境下将被实际使用的输入法模块：

        GTK_IM_MODULE=xim

    使用 fcitx5-gtk3-immodule-probing 来检查在当前环境下将被实际使用的输入法模块：

        GTK_IM_MODULE=xim

    使用 fcitx5-gtk4-immodule-probing 来检查在当前环境下将被实际使用的输入法模块：

        GTK_IM_MODULE=fcitx5

...

```
其中在Gtk中
它提示我缺少 一个环境变量
将 `export GTK_IM_MODULE=fcitx` 添加到   `~/.xprofile` 中解决。(没有这个文件创建一个)

我安装fcitx时，已经按照[wiki](https://wiki.archlinuxcn.org/wiki/Fcitx5)设置环境变量

> 为了告诉程序使用 fcitx5 输入法，需要设置相应的环境变量。编辑 `/etc/environment` 并添加以下几行，然后重新登录[1](https://wiki.archlinuxcn.org/wiki/Fcitx5#cite_note-1)：
	GTK_IM_MODULE=fcitx
	QT_IM_MODULE=fcitx
	XMODIFIERS=@im=fcitx
	SDL_IM_MODULE=fcitx
	GLFW_IM_MODULE=ibus

### Wechat
用的是wechat-bin包^AUR
命令行下可以用
```bash
alias -s wechat='/opt/wechat/wechat'
```
设置别名

`X11`下
配置好后，自动适配输入法
`wayland` 下
一开始是用不了输入法的
在终端中运行以下命令试试：
```bash
QT_IM_MODULE=fcitx XMODIFIERS=@im=fcitx wechat
```
如果可以
则可以修改桌面文件
通常在 ~/.local/share/applications/wechat-bin.desktop
修改exec部分
```bash
Exec=env QT_IM_MODULE=fcitx XMODIFIERS=@im=fcitx /opt/wechat/wechat %U
```

### fcitx5总结
#### X11
只需在`/etc/environment`中加入
```
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx
GLFW_IM_MODULE=ibus
```
然后 将 `export GTK_IM_MODULE=fcitx` 添加到   `~/.xprofile` 中解决。

#### Wayland
相比之下，它对各种输入法的兼容性并不好，但它比X11更安全，所以我选择使用它
首先退出正在运行的 Fcitx 5 进程，前往 _系统设置_ > _输入设备_ > _虚拟键盘_，选择 _Fcitx 5_。
**警告**：勿加 `GTK_IM_MODULE` 和 `QT_IM_MODULE`.  
wiki上说，这个可能会导致屏幕闪烁，但kwin对此兼容性更好一些，虽然我使用的是kwin，不过我并没有尝试，添加这两个变量
##### chrome
```bash
alias -s chrome='google-chrome-stable --enable-features=UseOzonePlatform --ozone-platform=wayland --enable  
-wayland-ime'
```
在菜单中，也编辑应用程序，添加参数。
##### wechat
见上。

### Wayland and X11
wayland更安全，它不像X11有一些代码非常乱
据说wayland性能上要比X11好
但我是nvidia的驱动，似乎现在wayland在nvidia上还是有些糟糕
而且我也确实感觉我的电脑发热不正常。

---

2025.6.21
现在系统更新了，似乎用wayland非常好(系统这次更新好像自主刨除了xorg)

---

### Nvim
用[pwnvim](https://github.com/pwnwriter/pwnvim)他的配置