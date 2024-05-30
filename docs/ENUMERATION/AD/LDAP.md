# LDAP
#nmap 

```
nmap -n -sV --script "ldap* and not brute" [IP]
```

#ldapsearch

```
ldapsearch -H ldaps://[host]:636/ -x -s base -b '' "(objectClass=*)" "*" +
```