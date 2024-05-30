# WEB
#enum 
```
nikto -h [ip]
```

#URI_enum
```
feroxbuster --url [url]
dirbuster
ffuf
gobuster
wpscan
```
#sub-domain_enum

```
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://[hostname] -H "HOST:FUZZ.[hostname]"
```

#whatweb
```
whatweb http://[ip/host]:[port]
```

#gobuster_detail
```
gobuster dir -u http://[ip/host] -w /usr/share/wordlists/dirb/common.txt -o mailsrv1/gobuster -x txt,pdf,config

-u url
-w wordlist
-o output file
-x filetype to enumerate
```

#wpscan_detail
```
#aggressive scan without token

wpscan --url http://[ip/host] --enumerate p --plugins-detection aggressive -o websrv1/wpscan
```