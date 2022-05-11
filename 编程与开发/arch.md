# Arch安装指南
#arch 


[from source](https://wiki.archlinux.org/title/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)

[from source](https://archlinuxstudio.github.io/ArchLinuxTutorial/#/)

# 分区
```shell
fdisk
GPT分区
挂载点 空间
/mnt/boot 300MiB mkfs.fat -F 32
/mnt 剩余空间 mkfs.ext4


/etc/pacman.d/mirrorlist

# 写入卷标
genfstab -U /mnt >> /mnt/etc/fstab
```