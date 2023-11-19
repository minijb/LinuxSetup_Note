# manjaro set up

## 驱动安装

设置 -> 硬件设备 -> auto install proprietary driver

## 换源

```sh
sudo pacman-mirrors -c China -i -m rank
sudo pacman -Syyu
```

### 加入archlinuxcn源

```sh
sudo kate kate /etc/pacman.conf
```

```txt
[archlinuxcn]
Server = https://mirrors.bfsu.edu.cn/archlinuxcn/$arch
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
Server = https://mirrors.sjtug.sjtu.edu.cn/manjaro/stable/$repo/$arch
```

更新

```sh
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring
```

## 安装yay

```sh
sudo pacman -S yay
yay -Syyu && yay -Sys
```

## 输入法

**安装fcitx5**:

```sh
sudo pacman -S fcitx5 
sudo pacman -S fcitx5-configtool  
sudo pacman -S fcitx5-qt
sudo pacman -S fcitx5-gtk
sudo pacman -S fcitx5-chinese-addons
sudo pacman -S fcitx5-material-color
sudo pacman -S kcm-fcitx5
sudo pacman -S fcitx5-lua
```

**配置环境**:

```sh
kate /etc/environment
```

```txt
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
INPUT_METHOD=fcitx
SDL_IM_MODULE=fcitx
```

**配置小图标**:

```sh
kate ~/.xprofile
```

```txt
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```

### 谷歌拼音

```sh
sudo pacman -S fcitx-im
yay -S fcitx-configtool
yay -S fcitx-googlepinyin
```

## qq

```sh
yay -S linuxqq
```

## qq音乐

```sh
yay -S qqmusic-bin
```

## vscode 

```sh
yay -S visual-studio-code-bin‍
```

## 代理

### clash

```sh
yay -S clash clash-for-windows-bin
```

### v2ray

```sh
yay -S v2ray v2raya
```

#### 运行v2raya的服务，否则无法使用

```sh
sudo systemctl start v2raya.service #启动 v2rayA
sudo systemctl enable v2raya.service #设置开机自动启动
```

**默认网页端口** : `http://localhost:2017/`

**使用教程**： [v2ray](https://v2raya.org/docs/prologue/quick-start/)

## 开机自启动

[zhihu](https://zhuanlan.zhihu.com/p/656733028)
[csdn](https://blog.csdn.net/leigelaile1/article/details/105475105)