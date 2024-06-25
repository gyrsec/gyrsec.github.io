# PORT SCAN

#masscan
``` bash
# scan all TCP / UDP ports
# use with caution; very noisy and can impact performance of site
masscan -p1-65535,U:1-65535 [ip] --rate=1000 -e tun0
```

#nmap 
``` bash
# default scan I generally use
# default scripts, version detection
nmap -sC -sV [ip]

# helpful flags
-t[1-5]: scan faster / slower, defaul = 3
-sT: tcp scan(default)
-sU: udp scan
--top-ports [number]: scans most frequently used [number] of udp/tcp ports
-A: aggressive scan, enables os detection, version scanning, default scripts, and traceroute
```