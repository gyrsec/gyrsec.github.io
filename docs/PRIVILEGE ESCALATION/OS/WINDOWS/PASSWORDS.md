# PASSWORDS
#file_search
```powershell
Get-ChildItem -Path "C:\Users" -Include *.txt,*.ini -File -Recurse -ErrorAction SilentlyContinue
#interesting file types
# PASSWORDS


Get-Childitem -Recurse | findstr -i "directory config txt aspx ps1 bat xml pass user"
```

#powershell_history 
```powershell
(Get-PSReadlineOption).HistorySavePath
check for transcript files
search in eventviewer for powershell script block logging with passwords
```

[[MIMIKATZ]] 