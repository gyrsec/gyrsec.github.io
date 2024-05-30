# VULNERABILITIES
#nmap 
```
sudo nmap -sV --script "vuln" [ip]
-sV is very important, service detection allows nmap to scan relevant vulns
```

#add_custom_nse
```
search google: CVE... nse
download nse to /usr/share/nmap/scripts/ and rename to follow nmap naming convention
sudo nmap --script-updatedb
ready to use!
```