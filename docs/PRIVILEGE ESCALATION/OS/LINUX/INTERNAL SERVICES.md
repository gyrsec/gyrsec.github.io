# INTERNAL SERVICES
#ifconfig

#chisel

```
chisel server -p [port] --socks5 --reverse

./chisel_1.7.7_linux_amd64 client [server ip]:[server port] R:socks

sudo vi /etc/proxychains.conf

proxychains nmap -A -p[port to scan] [ip to scan]