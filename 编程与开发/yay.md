# yay 安装
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
% yay -S yay-bin
# 问及移除 yay 时选是
% yay
% rm -rf yay
```