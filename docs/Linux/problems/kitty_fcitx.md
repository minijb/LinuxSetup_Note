# In kitty, fcitx is useless

add following txt in `~/.xprofile` and `/etc/environment`

```sh
# /etc/environment
GLFW_IM_MODULE=ibus kitty

# ~/.xprofile
export GLFW_IM_MODULE=ibus kitty
```
