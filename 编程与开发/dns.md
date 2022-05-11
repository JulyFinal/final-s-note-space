
# DNS 问题

```
# 设置 /etc/resolv.conf  无效后
sudo vim /etc/systemd/resolved.conf 

DNS=114.114.114.114
DNS=8.8.8.8

systemctl restart systemd-resolved.service
systemd-resolve --status
```