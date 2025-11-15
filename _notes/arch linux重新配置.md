---
title: arch linux重新配置
date: 2025-10-12 00:27:57
feed: show
---
安装好电脑并更新
下载`neovim` [[#配置neovim]] 见下
### 更改系统默认设置
- 例如窗口拖动动画
- user下文件夹为中文，像`下载`设置成`download`，在设置-会话-位置中设置。
### 添加arch中文社区仓库
在 /etc/pacman.conf 文件末尾添加以下两行（或者从[这里](https://github.com/archlinuxcn/mirrorlist-repo)选择一个镜像）：
```
[archlinuxcn]
Server = https://repo.archlinuxcn.org/$arch
```
更新数据库并安装 archlinuxcn-keyring：
 `pacman -Sy archlinuxcn-keyring`
更新系统并安装镜像仓库列表。分为两步是为了让安装的 keyring 生效：
`pacman -Su archlinuxcn-mirrorlist-git`
### 安装上网工具
`sudo pacman -S clash-verge-rev`
然后导入配置文件
从可能的位置 如机场 http://fcweba04.cc/dashboard
安装`chrome` , 好像`Firedragon`同步功能有点问题
### 键位替换
目前使用的是 `xcape`
[Arch Wiki](https://wiki.archlinux.org/title/Xorg/Keyboard_configuration#One-click_key_functions)
首先在设置中 键盘-键盘-键位绑定  将caps和ctrl交换
```
sudo pacman -S xcape
```
添加自启动文件
`sudo nvim ~/.config/autostart/xcape.desktop`
```shell
[Desktop Entry]
Name=Xcape
Exec=/usr/bin/xcape -e 'Control_L=Escape'
Terminal=false
Type=Application
StartupNotify=true
```
### 中文输入
用的软件是fcitx5
较复杂
安装 `fcitx5-im`这是一个捆绑包
然后安装 `fcitx5-chinese-addons`
#### 安装中文词库
在 GitHub 打开[维基百科中文拼音词库](https://github.com/felixonmars/fcitx5-pinyin-zhwiki)的 [Releases](https://github.com/felixonmars/fcitx5-pinyin-zhwiki/releases) 界面，下载最新版的 `.dict` 文件。按照 README 的指导，将其复制到 `~/.local/share/fcitx5/pinyin/dictionaries/` 文件夹下即可。
#### 配置环境变量
注： `fcitx5-diagnose`可以诊断
我们使用的wayland 桌面
设置中 键盘>虚拟键盘 >选择 fcitx5
编辑 `/etc/environment` 并添加
```
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx #让一些使用特定版本 SDL2 库的游戏能正常使用输入法
GLFW_IM_MODULE=ibus
```

### 配置nvim

```shell
git clone https://github.com/1ceshadow/neovim-config.git ~/.config/nvim
```
或者
```
git clone https://github.com/LazyVim/starter ~/.config/nvim      #官方Lazyvim
```

```
rm -rf ~/.config/nvim/.git
```
### 一些软件
**微信**: 有原生的linux版本，也无需从官网下载。统一用pacmna/yay下载，好管理
`wechat-bin`
刚安装完微信，无法使用fctix5,甚至导致无法打开chrome.
单独安装wechat-bin的情况时，在Wayland下fcitx5的支持

建议 在微信的启动方式中设置环境变量
1. 在开始菜单中搜索wechat,找到微信应用程序项目
2. 右键打开 “编辑应用程序”
3. 在弹出的编辑窗口中填入环境变量（下面这一行，多个变量用空格隔开的）
```
        QT_IM_MODULE=fcitx SDL_IM_MODULE=fcitx GLFW_IM_MODULE=ibus
```
4. 保存并重启微信即可
**obsidian**：添加参数
```
--enable-features=UseOzonePlatform --ozone-platform=wayland --enable-wayland-ime %U
```
### 添加别名
```bash
alias -s wechat="/opt/wechat/wechat"
alias -s vim=nvim
```
### 细碎问题

启动电脑时显示`Failed to start Virtual Console Setup`
表示在启动期间加载键盘布局或字体配置存在问题，通常是由于键盘映射或字体不正确或缺失造成的 。
可以通过使用 `localectl list-keymaps` 识别正确的键盘映射，然后在 `/etc/vconsole.conf` 中使用 `KEYMAP=your_keymap` 进行设置来解决此问题。 修改配置后，使用 `sudo dracut-rebuild`等命令重建初始 ramdisk（initramfs/initrd）并重新启动

### windows时间
将windows设置成使用UTC时间
```
reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_DWORD /f
```
### 更改GRUB
`usr/share/grub/themes/***/`
中
```
# Global Property
title-text: ""
desktop-image: "reyna.png"
desktop-image-scale-method: "crop"
desktop-color: "#1E1E2E"
terminal-font: "Sans Bold 16"
terminal-left: "0"
terminal-top: "0"
terminal-width: "100%"
terminal-height: "100%"
terminal-border: "0"

# Logo image
#+ image {
#	left = 50%-50
#	top = 35%-50
#    file = "logo.png"
#}

```