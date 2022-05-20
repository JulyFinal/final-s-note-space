# Arch 安装指南

## 安装时
### 系统
```bash
# set time
timedatectl set-ntp true

# 分区
fdisk -l
fdisk /dev/nvme0n1

GPT分区
挂载点 空间
/mnt/boot 300MiB
/mnt 剩余空间

mkfs.fat -F 32 boot分区
mkfs.ext4 根分区
# mount
mount /dev/根分区g /mnt
mount /dev/boot分区 /mnt/boot
# 设置镜像地址
/etc/pacman.d/mirrorlist

# 预放入包程序
pacstrap /mnt base linux linux-firmware base-devel sudo neovim vi dhcpcd linux-headers wpa_supplicant networkmanager dolphin bluez bluez-utils# xf86-video-intel
# plasma-meta sddm

# 写入卷标
genfstab -U /mnt >> /mnt/etc/fstab

# 进入系统
arch-chroot /mnt

# edit sudo
visudo
# 开启%wheel ALL=(ALL) ALL
useradd -m -G wheel -s /bin/zsh final
# set passwd
passwd final

# 设置服务
systemctl enable dhcpcd
systemctl enable wpa_supplicant
systemctl enable NetworkManager
systemctl enable bluetooth
systemctl enable --now bluetooth
# systemctl enable sddm

# 设置时区
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
hwclock --systohc
# locale
/etc/locale.gen
# 取消en_US.UTF-8 UTF-8 注释
locale-gen

/etc/locale.conf
# 设置 LANG=en_US.UTF-8

# hostname
/etc/hostname
# 设置主机名 finalarch
vim /etc/hosts
127.0.0.1 localhost 
::1 localhost 
127.0.1.1 finalarch

mkinitcpio -P
# 设置root密码
passwd root

# 安装微码
pacman -S intel-ucode

# 设置grub
pacman -S grub efibootmgr
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
# 接下来编辑/etc/default/grub 文件，去掉`GRUB_CMDLINE_LINUX_DEFAULT`一行中最后的 quiet 参数，同时把 log level 的数值从 3 改成 5。这样是为了后续如果出现系统错误，方便排错。同时在同一行加入 nowatchdog 参数，这可以显著提高开关机速度。
grub-mkconfig -o /boot/grub/grub.cfg
#exit
# 退出
umount -R /mnt


## SSD btrfs

# 格式化目标分区为BtrFS
mkfs.btrfs /dev/sda1

# 挂载目标分区，并打开SSD优化
mount -t btrfs -o ssd /dev/sda1 /mnt
```

## 安装后
### 源配置

```
sudo pacman-mirrors -c China -m rank
```

### 一般安装
```shell
sudo pacman -S ranger plasma-meta dolphin sddm
systemctl enable sddm
```


### YAY
```
# yay 配置
git clone https://aur.archlinux.org/yay
cd yay
makepkg -si

# go换源
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
# 临时生效
export GO111MODULE=on
export GOPROXY=https://goproxy.cn
# 永久生效
echo "export GO111MODULE=on" >> ~/.profile
echo "export GOPROXY=https://goproxy.cn" >> ~/.profile
source ~/.profile

# 替换yay 为yay-bin
yay -S yay-bin
# 问及移除 yay 时选是
yay
rm -rf yay

```

### Proxy

```shell
yay -S proxychains-ng
```

### GIT
```
sudo pacman -S lazygit
```

```text
$ git config --global user.name <用户名>
$ git config --global user.email <邮箱地址>
$ git config --global http.proxy socks5://127.0.0.1:7890
$ git config --global https.proxy socks5://127.0.0.1:7890
```

### 输入法

```shell
sudo pacman -S fcitx5-im 
sudo pacman -S fcitx5-chinese-addons  # fcitx5-rime fcitx-configtool可选 

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

### GFW
```shell
yay -S clash-for-windows-bin
```

### ZSH
```shell
sudo pacman -S zsh-autosuggestions zsh-syntax-highlighting zsh-theme-powerlevel10k zsh-completions
```

```shell
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme

alias es='emacs'
alias alias pc4="proxychains4"
alias setproxy="export ALL_PROXY=socks5://127.0.0.1:7890; echo 'SET PROXY SUCCESS!!!'"
alias unsetproxy="unset ALL_PROXY; echo 'UNSET PROXY SUCCESS!!!'"
```
### SSH
```
systemctl start sshd
systemctl enable sshd
```


### 虚拟机
需要提前了解linux的核心版本
```shell
uname -r
# 5.15.38-1-MANJARO
```
则下方的linux为linux515
```shell
sudo pacman -S virtualbox linux515-virtualbox-host-modules # virtualbox-host-dkms

# 查看 Virtualbox 版本
$ vboxmanage --version
6.1.30r148432
​
# 安装拓展包，选择跟 Virtualbox 版本号一致的
$ yay virtualbox-ext-oracle

sudo gpasswd -a $USER vboxusers
```

### 编程环境
#### Neovim
```
sudo pacman -S xsel
```

### WPS
```text
yay -S wps-office wps-office-mui-zh-cn ttf-wps-fonts
```

### UniVPN
```shell
sudo -i

# seco client 依赖 ubuntu 的 arch 命令， 模拟 arch 命令返回 x86_64
echo "echo x86_64" > /usr/bin/arch
chmod u+x /usr/bin/arch

# install seco client
sh ./univpn-linux-64-10781.2.550.0329.run

# 启动后台服务
cd /usr/local/UniVPN/promote
./UniVPNPromoteService -d

# 界面就可以启动UniVPN了
```
