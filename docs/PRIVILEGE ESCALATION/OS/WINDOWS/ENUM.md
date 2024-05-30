# ENUM
#basic_enum
```
- Username and hostname
- Group memberships of the current user
- Existing users and groups
- Operating system, version and architecture
- Network information
- Installed applications
- Running processes
```

#basic
```
whoami /all
whoami /priv
```

#results
[[SeImpersonatePrivilege]]
[[SeAssignPrimaryToken]]
[[SeLoadDriverPrivilege]]

#what_shell 
```powershell
(dir 2>&1 *`|echo CMD);&<# rem #>echo PowerShell
```

#commands 
```powershell
whoami - get user name and hostname
systeminfo - system info
Get-LocalGroup - PS
net localgroup - cmd
Get-LocalGroupMember [group]
ipconfig /all
route print - useful to determine possible attack vectors to other systems or networks
netstat -ano

#get all installed software
Get-ItemProperty "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname

Get-ItemProperty "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\*" | select displayname
#above can miss some software, check C:\Program Files and C:\Program Files (x64) and user downloads folder

Get-Process - list running processes in PS
```

#file_search
```powershell
Get-ChildItem -Path C:\xampp -Include *.txt, *.pdf, *.xls, *.xlsx, *.doc, *.docx, *.ini, *.kdbx -File -Recurse -ErrorAction SilentlyContinue
#interesting file types
# ENUM
```

#powershell_history 
```powershell
(Get-PSReadlineOption).HistorySavePath
check for transcript files
search in eventviewer for powershell script block logging with passwords
```

#seatbelt


#file_search 
```powershell
Get-ChildItem -Path C:\ -Filter soffice.ps1 -Recurse -ErrorAction SilentlyContinue -Force
```