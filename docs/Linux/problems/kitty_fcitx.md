# kitty不能使用fcitx输入法

在 `~/.xprofile` 中加入 

```txt
export GLFW_IM_MODULE=ibus kitty
```

在 `/etc/environment` 中加入

```txt
GLFW_IM_MODULE=ibus kitty
```
