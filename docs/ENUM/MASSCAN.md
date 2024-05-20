# MASSCAN

scan all TCP and UDP ports
```
masscan -p1-65535,U:1-65535 10.10.10.x --rate=1000 -e tun0
```