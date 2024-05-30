# ENUM
#enum 
```sh
tty #always verify it is a tty
cat /etc/passwd
hostname
cat /etc/issue
cat /etc/*release
uname -a
```

#enum_network 
```sh
ip a
ifconfig
route
routel
netstat -anp
ss -anp

cat /etc/iptables/rules.v4
ls -la /etc/iptables

ip addr
ip route
```

#cron 
```sh
ls -lah /etc/cron*
crontab -l
sudo crontab -l
cat /etc/crontab
grep "CRON" /var/log/syslog
```

#installed_programs
```sh
dpkg -l
```

#file_perms
```sh
find / -writable -type d 2>/dev/null
```

#partitions
```sh
cat /etc/fstab
lsblk
mount unmounted partitions and enum
```

#kernel_modules
```sh
lsmod
/sbin/modinfo [module]
```

#SUID/GUID
```sh
find / -perm -u=s -type f 2>/dev/null
```
[[SUID]]

#sudo
```sh
sudo su # its worth a shot!
sudo -l
```

#passwd/shadow
```
ls -la /etc/passwd
ls -la /etc/shadow
```
[[PASSWD]]
[[SHADOW]]
[[CAPABILITIES]]

lse.sh
linuxprivchecker
linpeas