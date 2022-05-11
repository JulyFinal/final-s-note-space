# RIME 设置
```
sudo pacman -S fcitx5-im 
sudo pacman -S fcitx5-chinese-addons  # fcitx5-rime 可选

# /etc/environment
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_IM_MODULE=fcitx

# i3w etc.
# fcitx5
exec_always --no-startup-id fcitx5

fcitx5 &
```