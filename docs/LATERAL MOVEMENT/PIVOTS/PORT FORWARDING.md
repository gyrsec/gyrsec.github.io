# PORT FORWARDING
https://github.com/nicocha30/ligolo-ng#how-is-this-different-from-ligolochiselmeterpreter-

nmap needs -sT flag for proxychains
note to self: my proxychains config has been modified for short timeouts

#socat
```
#target system
socat -ddd TCP-LISTEN:[port],fork TCP:[ip]:[port]

-ddd                   verbose
TCP-LISTEN:1234        define listening port
fork                   do not die after single connection
TCP:192.168.50.111:1234   forward all traffic to 192.168.50.111:1234
```

#ssh 
```
#single port
ssh -N -L 0.0.0.0:[local port]:[remote host]:[remote port] [user]@[remote host]

#dynamic
ssh -N -D 0.0.0.0:[local port] [user]@[remote host]
```

#proxychains
```
modify /etc/proxychains.conf
use chisel if desired
proxychains [some command]
```

#chisel
```
chisel server -p [chisel server port] --reverse

.\chisel.exe client [chisel server ip]:[chisel server port] R:socks
```

#proxychain
```
chisel server -p [chisel server port] --socks5 --reverse

./chisel_1.7.7_linux_amd64 client [chisel server ip]:[chisel server port] R:socks

sudo vi /etc/proxychains.conf

proxychains nmap -A -p[remote port] [remote host ip]
```

#ssh_windows
```
ssh -N -R [port] [attacker username(probably kali)]@[attacker ip]
```

#netsh
```
netsh interface portproxy add v4tov4 listenport=[port] listenaddress=0.0.0.0 connectport=[port] connectaddress=[remote ip]

netsh advfirewall firewall add rule name="[some_logical_name]" protocol=[TCP/UDP] dir=in localip=[local ip] localport=[some port] action=allow
````