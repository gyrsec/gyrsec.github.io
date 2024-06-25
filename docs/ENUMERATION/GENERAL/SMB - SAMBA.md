# SMB - SAMBA
#nmap

```sh
nmap --script "smb* and not brute" -p 445 [ip]
```

#enum4linux

```sh
enum4linux -a [ip]
```

#smbclient

```sh
smbclient -L \\[ip]
smbclient \\[ip]\share
```

#nbtscan

``` bash
valid NetBIOS names
sudo nbtscan -r 192.168.50.0/24
```

#windows_enum

``` bash
list all shares
net view \\[hostname] /all
```