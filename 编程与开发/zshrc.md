# zshrc
```shell
sudo pacman -S zsh-autosuggestions zsh-syntax-highlighting zsh-theme-powerlevel10k zsh-completions


source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme

alias es='emacs'
alias alias pc4="proxychains4"
## 设置全部代理走sock5 后面的链接换成自己的配置
alias setproxy="export ALL_PROXY=socks5://172.31.144.1:7890"
### 取消全部代理设置
alias unsetproxy="unset ALL_PROXY"
```
