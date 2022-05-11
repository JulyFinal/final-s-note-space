# ArchWSL 指南
[github ssource](https://github.com/yuk7/ArchWSL)
```
vi /etc/pacman.conf
// 推荐取消注释 Misc options 中的 Color、CheckSpace 及 VerbosePkgLists 项
// 并添加 DisableDownloadTimeout 及 ParallelDownloads = 2
vi /etc/pacman.d/mirrorlist
// 请使用 https

pacman-key --init
pacman-key --populate
pacman -Syu
pacman -S --needed base-devel git zsh
// 问及安装 fakeroot 时选否
运行 groupadd sudo 以添加 sudo 组
运行 nano /etc/sudoers，取消注释 %wheel ALL=(ALL) NOPASSWD: ALL 行和 %sudo ALL=(ALL) ALL 行
运行 useradd -m -G wheel,sudo -s /bin/zsh $用户名 以建立新管理员用户
运行 passwd final 以为其设置密码
运行 passwd 以设置 root 用户密码
退出 Arch Linux
回到 Windows 中 Arch.exe 所在目录
在此处打开命令提示符并运行 Arch.exe config --default-user final
或
在此处打开 PowerShell 并运行 ./Arch.exe config --default-user final
```

```
wsl2 ping不通windows主机问题速查
New-NetFirewallRule -DisplayName "WSL" -Direction Inbound  -InterfaceAlias "vEthernet (WSL)"  -Action Allow
```


https://blog.csdn.net/Cypher_X/article/details/123011200