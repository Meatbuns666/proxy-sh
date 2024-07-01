#!/bin/bash

# 更新包列表并安装 Squid
sudo apt update
sudo apt install -y squid

# 备份原有的配置文件
sudo cp /etc/squid/squid.conf /etc/squid/squid.conf.bak

# 创建新的配置文件
sudo bash -c 'cat << EOF > /etc/squid/squid.conf
# 允许所有 IP 地址访问代理服务器
acl all src all
http_access allow all

# 设置代理服务器监听的端口为 62907
http_port 62907
EOF'

# 重启 Squid 服务
sudo systemctl restart squid

# 配置防火墙以允许 Squid 端口（如果有 ufw 防火墙）
if command -v ufw > /dev/null; then
    sudo ufw allow 62907/tcp
    sudo ufw reload
fi

echo "Squid HTTP 代理服务器已成功安装和配置，监听端口为 62907。"
