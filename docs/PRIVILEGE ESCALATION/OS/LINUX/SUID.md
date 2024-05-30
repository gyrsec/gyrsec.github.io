# SUID
#enum
```
find /* -user root -perm -4000 -print 2>/dev/null

#SUID
find / -perm -u=s -type f 2>/dev/null

#GUID
find / -perm -g=s -type f 2>/dev/null
```

https://gtfobins.github.io/

#exploitable
```
Nmap
Vim
find
Bash
More
Less
Nano
cp
```


#nonexploitable
```
ping
ping6
passwd
sudo
chfn
apring
gpasswd
chsh
chfn
mount
sudo
su
umount
mount
newgrp
pppd
```