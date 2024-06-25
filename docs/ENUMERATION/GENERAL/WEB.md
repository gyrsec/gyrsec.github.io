# WEB
#enum 
``` bash
nikto -h [ip]
```

#URI_enum
``` bash
feroxbuster --url [url]
dirbuster
ffuf
gobuster
wpscan
```
#sub-domain_enum

``` bash
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://[hostname] -H "HOST:FUZZ.[hostname]"
```

#whatweb
``` bash
whatweb http://[ip/host]:[port]
```

#gobuster_detail
``` bash
gobuster dir -u http://[ip/host] -w /usr/share/wordlists/dirb/common.txt -o mailsrv1/gobuster -x txt,pdf,config

-u url
-w wordlist
-o output file
-x filetype to enumerate
```

#wpscan_detail
``` bash
#aggressive scan without token
wpscan --url http://[ip/host] --enumerate p --plugins-detection aggressive -o websrv1/wpscan
```