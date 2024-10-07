# user enum

#kerbrute
```
~/tools/kerbrute_linux_amd64 userenum --dc 10.10.11.35 -d cicada.htb /usr/share/seclists/Usernames/Honeypot-Captures/multiplesources-users-fabian-fingerle.de.txt
```

#RID-cycle
```
enum4linux-ng -u guest 10.10.11.35 -r 500-50000

-u user try guest and null
-r rid range, defaults to 500-550,1000-1050
```